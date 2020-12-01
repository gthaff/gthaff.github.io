# OOA
# Use Cases
Input: java CLI stoplist fun.txt
       stoplist contains "the"
       fun.txt contains "Java is the best coding language"
       query is "Java"
Expected Output: fun.txt
       
Input: java CLI -d stoplist good.txt maybe.txt
       stoplist contains ""
       good.txt contains "good times"
       maybe.txt contains "so call me maybe"
       query is "maybe"
       
Expected Output: maybe.txt
                 so call me maybe          
