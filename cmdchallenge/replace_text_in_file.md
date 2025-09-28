This challenge has text files (with a .txt extension) that contain the phrase "challenges are difficult". Delete this phrase from all text files recursively.

Note that some files are in subdirectories so you will need to search for them.

find . -type f -name "*.txt" -print0 | xargs -0 sed -i 's/challenges are difficult//g'
