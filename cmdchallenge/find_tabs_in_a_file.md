How many lines contain tab characters in the file named file-with-tabs.txt in the current directory.

awk '/\t/{i++} END{print i}' file-with-tabs.txt 