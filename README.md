Replicate code for https://dl.acm.org/doi/10.1145/2858036.2858528


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
- Prefilter, filter out the fields corresponding to the normalized subject-verb-object relationship, to the format
- substitute all names with 'he'
  
  he  do  it

  he  ask  her

  ...

- Filter actions, filter to keep everything that has a person as its subject, rename matching subjects as "the person". to the format:
	the person  enter  the room

  NOP 3

  the person  open  the window

  NOP 0

  the person  close  the window

  NOP 4

  ...

- Skip gram, create ngrams, connected by the interleaved NOPs. to the format

  the person open the door  the person open the door

  the person enter the room  the person open the window

  the person open the window  the person close the window

  ...

- Count grams, compute frequencies of ngrams, to the format:

	the person close his eyes	the person open his eyes	421

  the person close her eyes	the person open her eyes	245

  the person shake her head	the person shake his head	106
