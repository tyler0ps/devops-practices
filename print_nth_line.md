Print the 25th line of the file faces.txt

awk 'NR==25 {print $0;exit}' faces.txt