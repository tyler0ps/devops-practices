The file sum-me.txt has a list of numbers, one per line. Print the sum of these numbers.

awk '{sum+=$0} END{print sum}' sum-me.txt