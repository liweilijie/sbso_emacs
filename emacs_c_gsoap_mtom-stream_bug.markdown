gSOAP has one bug while use it to transfor file by mtom-stream.
==========

**server side**

	SOAP_FMAC1
struct soap_multipart *
SOAP_FMAC2
soap_get_mime_attachment(struct soap *soap, void *handle)
{ 
	register soap_wchar c = 0;
  register size_t i, m = 0;
  register char *s, *t = NULL;
  register struct soap_multipart *content;
  register short flag = 0;
  if (!(soap->mode & SOAP_ENC_MIME))
    return NULL;
  content = soap->mime.last;
  if (!content)
  { if (soap_getmimehdr(soap))
      return NULL;
    content = soap->mime.last;
  }
  else if (content != soap->mime.first)
  { 
		if (soap->fmimewriteopen && ((content->ptr = (char*)soap->fmimewriteopen(soap, (void*)handle, content->id, content->type, content->description, content->encoding)) || soap->error))
    { 
			if (!content->ptr)
        return NULL;
    }
  }

  DBGLOG(TEST, SOAP_MESSAGE(fdebug, "Parsing MIME content id=%s type=%s\n", content->id ? content->id : SOAP_STR_EOS, content->type ? content->type : SOAP_STR_EOS));

  if (!content->ptr && soap_new_block(soap) == NULL)
  { 
		soap->error = SOAP_EOM;
    return NULL;
  }

  for (;;)
  { 
		if (content->ptr)
      s = soap->tmpbuf;
    else if (!(s = (char*)soap_push_block(soap, NULL, sizeof(soap->tmpbuf))))
    { 
			soap->error = SOAP_EOM;
      return NULL;
    }
    for (i = 0; i < sizeof(soap->tmpbuf); i++)
    { if (m > 0)
      { *s++ = *t++;
        m--;
      }
      else
      { if (!flag)
        { c = soap_get1(soap);
          if ((int)c == EOF)
					{ 
						/* XXX:added by liw for the client is graceful suspend.
						 * and this time should call the 'fclose' due to happend error.
						 * or it will be hold the file-descriptor source util this process is exit.
						 * 2012-11-10
						 */
						if (content->ptr && soap->fmimewriteclose)
							soap->fmimewriteclose(soap, (void*)content->ptr);

						soap->error = SOAP_CHK_EOF;
						return NULL;
					}
        }
        if (flag || c == '\r')
        { t = soap->msgbuf;
          memset(t, 0, sizeof(soap->msgbuf));
          strcpy(t, "\n--");
          if (soap->mime.boundary)
            strncat(t, soap->mime.boundary, sizeof(soap->msgbuf)-4);
          do c = soap_getchar(soap);
          while (c == *t++);
          if ((int)c == EOF)
          { 
						/* XXX:added by liw for the client is graceful suspend.
						 * and this time should call the 'fclose' due to happend error.
						 * or it will be hold the file-descriptor source util this process is exit.
						 * 2012-11-10
						 */
						if (content->ptr && soap->fmimewriteclose)
							soap->fmimewriteclose(soap, (void*)content->ptr);

						soap->error = SOAP_CHK_EOF;
            return NULL;
          }
          if (!*--t)
            goto end;
          *t = (char)c;
          flag = (c == '\r');
          m = t - soap->msgbuf + 1 - flag;
          t = soap->msgbuf;
          c = '\r';
        }
        *s++ = (char)c;
      }
    }
    if (content->ptr && soap->fmimewrite)
    { 
			if ((soap->error = soap->fmimewrite(soap, (void*)content->ptr, soap->tmpbuf, i)))
        break;
    }
  }
end:
  *s = '\0'; /* force 0-terminated */
  if (content->ptr)
  { 
		if (!soap->error && soap->fmimewrite)
      soap->error = soap->fmimewrite(soap, (void*)content->ptr, soap->tmpbuf, i);
    if (soap->fmimewriteclose)
      soap->fmimewriteclose(soap, (void*)content->ptr);
    if (soap->error)
      return NULL;
  }
  else
  { content->size = soap_size_block(soap, NULL, i+1)-1;
    content->ptr = soap_save_block(soap, NULL, NULL, 0);
  }
  soap_resolve_attachment(soap, content);
  if (c == '-' && soap_getchar(soap) == '-')
  { soap->mode &= ~SOAP_ENC_MIME;
    if ((soap->mode & SOAP_MIME_POSTCHECK) && soap_end_recv(soap))
    { if (soap->keep_alive < 0)
        soap->keep_alive = 0;
      soap_closesock(soap);
      return NULL;
    }
  }
  else
  { while (c != '\r' && (int)c != EOF && soap_blank(c))
      c = soap_getchar(soap);
    if (c != '\r' || soap_getchar(soap) != '\n')
    { soap->error = SOAP_MIME_ERROR;
      return NULL;
    }
    if (soap_getmimehdr(soap))
      return NULL;
  }
  return content;
}
