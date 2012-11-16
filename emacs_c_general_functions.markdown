自己写的一些函数记录
==========

*有时候自己写了一些有用的函数，然后兴奋一下，再然后记录一下它们吧！*

* * * * *

### 截utf8字符串长度 ###
 在入数据库时，由于长度限制，所以在入库之前将数据进行截取。但是在截取时如果是utf8的，则会出现乱码的情况。所以要根据utf8编码规范来进行截取。
 
      int cut_utf8_mbtolength(unsigned char *out, const unsigned char *s, int s_length, int cut_length)
	  {
	 int i, j;
	 unsigned char c;
	 for (i = 0, j = 0; i < s_length;)
	 {
	 	c = s[i];

	 	/* write_app_log("[%s] c:[0x%x]", __func__, c);*/

	 	/* ascii: 0000 0000 -> 1000 0000 */
	 	if (c < 0x80)
	 	{
	 		if (j+1 >= cut_length)
	 			break;

	 		out[j] = c;
	 		j++; i++;
	 		continue; /* return 1;*/
	 	} 
	 	else if (c < 0xc2) /* element of character: 1000 0000 -> 1100 0000 */
	 	{
	 		i++;
	 		continue; /* return RET_ILSEQ;*/
	 	} 
	 	else if (c < 0xe0) /* two character cscope: 1100 0000 - 1110 0000 */
	 	{
	 		if (s_length - i < 2)
	 		{
	 			i++;
	 			continue;
	 		}
	 		/* if (n < 2)*/
	 			/* return RET_TOOFEW(0);*/

	 		/* if (!((s[1] ^ 0x80) < 0x40))*/
	 		/* {*/
	 			/* i++;*/
	 			/* continue; [>return RET_ILSEQ;<]*/
	 		/* }*/

	 		if (j+2 >= cut_length)
	 			break;

	 		memcpy(out+j, s+i, 2);
	 		j+=2; i+=2;

	 		continue;
	 		/* *pwc = ((ucs4_t) (c & 0x1f) << 6)*/
	 			/* | (ucs4_t) (s[1] ^ 0x80);*/
	 		/* return 2;*/
	 	} 
	 	else if (c < 0xf0) /* three character scope: 1110 0000 - 1111 0000 */
	 	{
	 		if (s_length - i < 3)
	 		{
	 			i++;
	 			continue;
	 		}
	 		/* if (n < 3)*/
	 			/* return RET_TOOFEW(0);*/


	 		/* if (!((s[1] ^ 0x80) < 0x40 && (s[2] ^ 0x80) < 0x40 && (c >= 0xe1 || s[1] >= 0xa0)))*/
	 		/* {*/
	 			/* i++;*/
	 			/* continue; [>return RET_ILSEQ;<]*/
	 		/* }*/

	 		if (j+3 >= cut_length)
	 			break;

	 		memcpy(out+j, s+i, 3); j+=3; i+=3;
	 		continue;
	 		/* *pwc = ((ucs4_t) (c & 0x0f) << 12)*/
	 			/* | ((ucs4_t) (s[1] ^ 0x80) << 6)*/
	 			/* | (ucs4_t) (s[2] ^ 0x80);*/
	 		/* return 3;*/
	 	} 
	 	else if (c < 0xf8 && sizeof(ucs4_t)*8 >= 32) /* four character scope: 1111 0000 - 1111 1000 */
	 	{
	 		if (s_length - i < 4)
	 		{
	 			i++;
	 			continue;
	 		}
	 		/* if (n < 4)*/
	 			/* return RET_TOOFEW(0);*/


	 		/* if (!((s[1] ^ 0x80) < 0x40 && (s[2] ^ 0x80) < 0x40 && (s[3] ^ 0x80) < 0x40 && (c >= 0xf1 || s[1] >= 0x90)))*/
	 		/* {*/
	 			/* i++;*/
	 			/* continue; [>return RET_ILSEQ;<]*/
	 		/* }*/

	 		if (j+4 >= cut_length)
	 			break;

	 		memcpy(out+j, s+i, 4); j+=4; i+=4;
	 		continue;

	 		/* *pwc = ((ucs4_t) (c & 0x07) << 18)*/
	 			/* | ((ucs4_t) (s[1] ^ 0x80) << 12)*/
	 			/* | ((ucs4_t) (s[2] ^ 0x80) << 6)*/
	 			/* | (ucs4_t) (s[3] ^ 0x80);*/
	 		/* return 4;*/
	 	} 
	 	else if (c < 0xfc && sizeof(ucs4_t)*8 >= 32) /* five character scope: 1111 1000 - 1111 1100 */
	 	{
	 		if (s_length - i < 5)
	 		{
	 			i++;
	 			continue;
	 		}
	 		/* if (n < 5)*/
	 			/* return RET_TOOFEW(0);*/

	 		/* if (!((s[1] ^ 0x80) < 0x40 && (s[2] ^ 0x80) < 0x40 && (s[3] ^ 0x80) < 0x40 && (s[4] ^ 0x80) < 0x40 && (c >= 0xf9 || s[1] >= 0x88)))*/
	 		/* {*/
	 			/* i++;*/
	 			/* continue; [>return RET_ILSEQ;<]*/
	 		/* }*/


	 		if (j+5 >= cut_length)
	 			break;

	 		memcpy(out+j, s+i, 5); j+=5; i+=5;
	 		continue;

	 		/* *pwc = ((ucs4_t) (c & 0x03) << 24)*/
	 			/* | ((ucs4_t) (s[1] ^ 0x80) << 18)*/
	 			/* | ((ucs4_t) (s[2] ^ 0x80) << 12)*/
	 			/* | ((ucs4_t) (s[3] ^ 0x80) << 6)*/
	 			/* | (ucs4_t) (s[4] ^ 0x80);*/
	 		/* return 5;*/
	 	} 
	 	else if (c < 0xfe && sizeof(ucs4_t)*8 >= 32) /* six character scope: 1111 1100 - 1111 1110 */
	 	{
	 		if (s_length - i < 6)
	 		{
	 			i++;
	 			continue;
	 		}
	 		/* if (n < 6)*/
	 			/* return RET_TOOFEW(0);*/

	 		/* if (!((s[1] ^ 0x80) < 0x40 && (s[2] ^ 0x80) < 0x40*/
	 					/* && (s[3] ^ 0x80) < 0x40 && (s[4] ^ 0x80) < 0x40*/
	 					/* && (s[5] ^ 0x80) < 0x40*/
	 					/* && (c >= 0xfd || s[1] >= 0x84)))*/
	 		/* {*/
	 			/* i++;*/
	 			/* continue; [>return RET_ILSEQ;<]*/
	 		/* }*/


	 		if (j+6 >= cut_length)
	 			break;

	 		memcpy(out+j, s+i, 6); j+=6; i+=6;
	 		continue;

	 		/* *pwc = ((ucs4_t) (c & 0x01) << 30)*/
	 			/* | ((ucs4_t) (s[1] ^ 0x80) << 24)*/
	 			/* | ((ucs4_t) (s[2] ^ 0x80) << 18)*/
	 			/* | ((ucs4_t) (s[3] ^ 0x80) << 12)*/
	 			/* | ((ucs4_t) (s[4] ^ 0x80) << 6)*/
	 			/* | (ucs4_t) (s[5] ^ 0x80);*/
	 		/* return 6;*/
	 	} 
	 	else
	 	{
	 		i++;
	 		continue;
	 		/* return RET_ILSEQ;*/
	 	}
	 }

	 return j;
	 }

    
