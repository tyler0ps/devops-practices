Print the file faces.txt, but only print the first instance of each duplicate line, even if the duplicates don't appear next to each other.

Note that order matters so don't sort the lines before removing duplicates.

awk 'if(c[$0]==0){c[$0]=1;print;}else{next;}' faces.txt