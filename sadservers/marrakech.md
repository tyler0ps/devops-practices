https://sadservers.com/newserver/marrakech
    
    1  cat /etc/*reelase
    2  clear
    3  cat /etc/*release
    4  ls -ltr
    5  awk '{gsub(/[,.;:]/," "); print}' test.txt
    6  cat test.txt 
    7  awk '{gsub(/[,.;:]/," "); print}' test.txt
    8  awk '{gsub(/[,.;:]/," "); for(i=1;i<=NF;i++){c[tolower($i)]++}} END{for(w in c) print w, c[w]}' test.txt
    9  awk '{gsub(/[,.;:]/," "); for(i=1;i<=NF;i++){c[tolower($i)]++}} END{for(w in c) print w, c[w]}' test.txt | sort -nrk2
   10  awk '{gsub(/[,.;:]/," "); for(i=1;i<=NF;i++){c[tolower($i)]++}} END{for(w in c) print w, c[w]}' test.txt | sort -nrk2 | sed -n '2p' | awk '{print toupper($1)}'
   11  awk '{gsub(/[,.;:]+/," "); for(i=1;i<=NF;i++){c[tolower($i)]++}} END{for(w in c) print w, c[w]}' frankestein.txt | sort -nrk2 | sed -n '2p' | awk '{print toupper($1)}'
   12  awk '{gsub(/[,.;:]+/," "); for(i=1;i<=NF;i++){c[tolower($i)]++}} END{for(w in c) print w, c[w]}' frankestein.txt | sort -nrk2 | sed -n '2p' | awk '{print toupper($1)}' > /home/admin/mysolution
   13  history