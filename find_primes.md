The file random-numbers.txt contains a list of 100 random integers. Print the number of unique prime numbers contained in the file.

sort -u random-numbers.txt | awk '{for(i=2;i<=sqrt($0);i++) if($0%i==0) next; total++} END{prin
t total}'