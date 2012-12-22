vi yank

- `:81, 109y<center>`




If you ever need to cut/copy/delete/paste lines without knowing the actual number of lines, here is what you should do.
In normal mode, go to the beginning of the section that you want to yank.
Type mk to mark this spot as k.
Go to the end of the section you want to yank using whatever movement commands you like.
Type: y'k (<y-yank>, <single quote-go to mark>, k) To yank from the mark to the current location.
You can paste those lines wherever you want with p
Similarly, d'k will cut/delete the lines from the current location to the mark.
