There are files in this challenge with different file extensions.

Remove all files without the .txt and .exe extensions recursively in the current working directory.

find . -type f ! -name "*.txt" ! -name "*.exe" -exec rm {} \; 
find . -type f ! -regex ".*\(txt\|exe\)$" -delete