Print all matching lines (without the filename or the file path) in all files under the current directory that start with "access.log", where the next line contains the string "404".

Note that you will need to search recursively.

grep -ih "404" -B1 **/access.log* | egrep -v "404|--" 
