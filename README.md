# Data mining
- data mining.ipynb scrape texts from forum
- folder /docs/ contains text files

# Pre-process files
-extracts an ordered list of subject-verb-object relationships

- use this command:
  
find /docs/ |  grep -e '[4-7][0-9]' | java -Xmx512m -jar reverb.jar -f | tee sample.tsv

# Output ranked affordances 
- inputs: sample.csv + sampleobject.txt
- use following command:

python prefilter.py sample.tsv | python filter-actions.py sampleobject.txt | python skip-gram.py | python count-grams.py

# Explain

- filter out the fields corresponding to the normalized subject-verb-object relationship, to the format

  +he  do  it
  +he  ask  her
  +...


