# SPQRQL Queries for the Quran Explorer Project

The given SPARQL are _examples_ that may be reinterpreted and reused for applications.

1. List of Verses of the Quran and the topics discussed in each verse (English).
```
PREFIX : <http://quranontology.com/Resource/>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
select distinct ?verse ?topic ?label where { 
	  ?verse a :Verse.
    ?verse :DiscussTopic ?topic .
    ?topic rdfs:label ?label.
    
    FILTER (lang(?label) = 'en')
} 
```

1.1 List of Verses of the Quran and the topics discussed in each verse (Arabic).
```
PREFIX : <http://quranontology.com/Resource/>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
select distinct ?verse ?topic ?label where { 
	  ?verse a :Verse.
    ?verse :DiscussTopic ?topic .
    ?topic rdfs:label ?label.
    
    FILTER (lang(?label) = 'ar')
} 
```


2. List of verses and people mentioned in each verse (English).
```
PREFIX : <http://quranontology.com/Resource/>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
select distinct ?verse ?person ?label where { 
	?verse a :Verse.
    ?person :MentionedIn ?verse .
    ?person rdfs:label ?label.
    
    FILTER (lang(?label) = 'en')
} 
```

2.1 List of verses and people mentioned in each verse (Arabic).
```
PREFIX : <http://quranontology.com/Resource/>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
select distinct ?verse ?person ?label where { 
	?verse a :Verse.
    ?person :MentionedIn ?verse .
    ?person rdfs:label ?label.
    
    FILTER (lang(?label) = 'ar')
} 
```
3. List of verses and Prophets mentioned in each verse (English).
```
PREFIX : <http://quranontology.com/Resource/>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX qur: <http://quranontology.com/Resource/>
select distinct ?verse ?prophet ?label where { 
	?verse a :Verse.
    ?prophet :MentionedIn ?verse .
    ?prophet a qur:Prophet.
    ?prophet rdfs:label ?label.
    
    FILTER (lang(?label) = 'en')
} 
```

3.1 List of verses and prophet mentioned in each verse (Arabic).
```
PREFIX : <http://quranontology.com/Resource/>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX qur: <http://quranontology.com/Resource/>
select distinct ?verse ?prophet ?label where { 
	?verse a :Verse.
    ?prophet :MentionedIn ?verse .
    ?prophet a qur:Prophet.
    ?prophet rdfs:label ?label.
    
    FILTER (lang(?label) = 'ar')
} 
```

