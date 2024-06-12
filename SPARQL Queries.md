# SPARQL Queries for the Tafsir Project

1. What is the most narrated Topic by Narrator A?
```
PREFIX : <http://www.tafsirtabari.com/ontology#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
select  ?theme (COUNT(?hadith) AS ?numHadiths)
{ 
    ?hadith :hasHadithText/:hasText ?hadithText.
    ?hadith :containsNarratorChain/:hasNarratorSegment/:refersTo ?y .
    ?y :hasName "ابن عباس".
    ?hadith :hasTheme ?theme.
} 

GROUP BY ?theme
ORDER BY DESC(?numHadiths)

```

2.  Find all the hadith narrated from ابن عباس and their topics/themes?
```
PREFIX : <http://www.tafsirtabari.com/ontology#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
select ?hadith ?hadithText ?theme
{ 
    ?hadith :hasHadithText/:hasText ?hadithText.
    ?hadith :containsNarratorChain/:hasNarratorSegment/:refersTo ?y .
    ?y :hasName ?name.
    ?hadith :hasTheme ?theme.
} 
VALUES (?name)
{
    ("ابن عباس")
}
```

3. Question: Which topics are discussed by at least three Hadith narrations?

```
PREFIX : <http://www.tafsirtabari.com/ontology#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>

SELECT DISTINCT ?topic
WHERE {
   ?hadith a :Hadith.
  ?hadith :hasTheme ?topic .
}
GROUP BY ?topic
HAVING (COUNT(?hadith) >= 3)
```

4. How many hadith were narrated by RAWI_A?


# SPARQL Queries for the Quran Explorer Project

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
4. List of verses and Locations mentioned in each verse (English).
```
PREFIX : <http://quranontology.com/Resource/>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX qur: <http://quranontology.com/Resource/>
select distinct ?verse ?verseText ?location where { 
	?verse a :Verse.
    ?verse rdfs:label ?verseText.
    ?loc :MentionedIn ?verse .
    ?loc a qur:Location.
    ?loc rdfs:label ?location.
    
    FILTER ((lang(?location) = 'en') && (lang(?verseText)='en'))
}  
```

4.1 List of verses and Locations mentioned in each verse (Arabic).
```
PREFIX : <http://quranontology.com/Resource/>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX qur: <http://quranontology.com/Resource/>
select distinct ?verse ?verseText ?location where { 
	?verse a :Verse.
    ?verse rdfs:label ?verseText.
    ?loc :MentionedIn ?verse .
    ?loc a qur:Location.
    ?loc rdfs:label ?location.
    
    FILTER ((lang(?location) = 'ar') && (lang(?verseText)='ar'))
} 
```

5. List of similar verses (English).
```
PREFIX : <http://quranontology.com/Resource/>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX qur: <http://quranontology.com/Resource/>
select distinct ?verse ?verseText ?simVerse ?sVerseText where { 
	?verse a :Verse.
    ?verse rdfs:label ?verseText.
    ?simVerse :SimilarVerse ?verse .
    ?simVerse rdfs:label ?sVerseText.
    
    FILTER ((lang(?verseText) = 'en') && (lang(?sVerseText)='en'))
}  
```

5.1 List of similar verses (Arabic).
```
PREFIX : <http://quranontology.com/Resource/>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX qur: <http://quranontology.com/Resource/>
select distinct ?verse ?verseText ?simVerse ?sVerseText where { 
	?verse a :Verse.
    ?verse rdfs:label ?verseText.
    ?simVerse :SimilarVerse ?verse .
    ?simVerse rdfs:label ?sVerseText.
    
    FILTER ((lang(?verseText) = 'ar') && (lang(?sVerseText)='ar'))
} 
```

5.2 List of Strongly similar verses (English).
```
PREFIX : <http://quranontology.com/Resource/>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX qur: <http://quranontology.com/Resource/>
select distinct ?verse ?verseText ?simVerse ?sVerseText where { 
	?verse a :Verse.
    ?verse rdfs:label ?verseText.
    ?simVerse :StronglySimilar ?verse .
    ?simVerse rdfs:label ?sVerseText.
    
    FILTER ((lang(?verseText) = 'en') && (lang(?sVerseText)='en'))
}  
```

5.3 List of Strongly similar verses (Arabic).
```
PREFIX : <http://quranontology.com/Resource/>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX qur: <http://quranontology.com/Resource/>
select distinct ?verse ?verseText ?simVerse ?sVerseText where { 
	?verse a :Verse.
    ?verse rdfs:label ?verseText.
    ?simVerse :StronglySimilar ?verse .
    ?simVerse rdfs:label ?sVerseText.
    
    FILTER ((lang(?verseText) = 'ar') && (lang(?sVerseText)='ar'))
} 
```
5.4 List of Slightly similar verses (English).
```
PREFIX : <http://quranontology.com/Resource/>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX qur: <http://quranontology.com/Resource/>
select distinct ?verse ?verseText ?simVerse ?sVerseText where { 
	?verse a :Verse.
    ?verse rdfs:label ?verseText.
    ?simVerse :SlightlySimilar ?verse .
    ?simVerse rdfs:label ?sVerseText.
    
    FILTER ((lang(?verseText) = 'en') && (lang(?sVerseText)='en'))
}  
```

5.5 List of Slightly similar verses (Arabic).
```
PREFIX : <http://quranontology.com/Resource/>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX qur: <http://quranontology.com/Resource/>
select distinct ?verse ?verseText ?simVerse ?sVerseText where { 
	?verse a :Verse.
    ?verse rdfs:label ?verseText.
    ?simVerse :SlightlySimilar ?verse .
    ?simVerse rdfs:label ?sVerseText.
    
    FILTER ((lang(?verseText) = 'ar') && (lang(?sVerseText)='ar'))
} 
```
6. List of Verses of the Quran and the Events discussed in each verse (English).
```
PREFIX : <http://quranontology.com/Resource/>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX qur: <http://quranontology.com/Resource/>
select distinct ?verse ?verseText ?eventLabel where { 
	?verse a :Verse.
    ?verse rdfs:label ?verseText.
    ?event :MentionedIn ?verse .
    ?event a qur:Event.
    ?event rdfs:label ?eventLabel.
    
    FILTER ((lang(?eventLabel) = 'en') && (lang(?verseText)='en'))
}  
```

6.1 List of Verses of the Quran and the Events discussed in each verse (Arabic).
```
PREFIX : <http://quranontology.com/Resource/>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX qur: <http://quranontology.com/Resource/>
select distinct ?verse ?verseText ?eventLabel where { 
	?verse a :Verse.
    ?verse rdfs:label ?verseText.
    ?event :MentionedIn ?verse .
    ?event a qur:Event.
    ?event rdfs:label ?eventLabel.
    
    FILTER ((lang(?eventLabel) = 'ar') && (lang(?verseText)='ar'))
}  
```
6.2 List of Events of the Quran and the verses they are mentioned in  (Arabic).
(NEEDS INFERENCE ON = (INCLUDE RESULTS FROM INFERRED DATA))
```
PREFIX : <http://quranontology.com/Resource/>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX qur: <http://quranontology.com/Resource/>
select distinct  ?eventLabel ?verse ?verseText where { 
	?event a qur:Event.
    ?event rdfs:label ?eventLabel.
    ?event :MentionedIn ?verse .
    ?verse a :Verse.
    ?verse rdfs:label ?verseText.
   
    FILTER ((lang(?eventLabel) = 'ar') && (lang(?verseText)='ar'))
}  
```

7. List of Surahs in order
```
PREFIX : <http://quranontology.com/Resource/>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>

SELECT ?s ?label
WHERE { 
    ?s a :Chapter .
    ?s rdfs:label ?label.
    FILTER (lang(?label) = 'ar')
    # Extract numeric part from the URI using regex
    BIND(STRAFTER(str(?s), "http://quranontology.com/Resource/quran") AS ?numericPart)
    BIND(xsd:integer(?numericPart) AS ?numericValue)
}
ORDER BY ASC(?numericValue)
```
8. List of Ayahs with Text in order
```
PREFIX : <http://quranontology.com/Resource/>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>

SELECT ?ayah ?ayahText ?surah ?SName
WHERE { 
    ?ayah a :Verse.
    ?ayah :IsPartOf ?surah.
    ?ayah rdfs:label ?ayahText.
    ?surah rdfs:label ?SName.
	FILTER ((lang(?ayahText) = 'ar') && (lang(?SName)='ar'))
    # Extract numeric part from the URI using regex
   BIND(xsd:integer(REPLACE(STRAFTER(str(?ayah), "http://quranontology.com/Resource/quran"), "-", "")) AS ?numericValue)
}
ORDER BY ASC(?numericValue)
```
9. List of Topics
```
PREFIX : <http://quranontology.com/Resource/>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
select ?topic ?Topiclabel ?subTopic ?subTopicLabel where { 
	?topic a :Topic.
    ?topic rdfs:label ?Topiclabel.
    ?topic :HasSubTopic* ?subTopic.
    ?subTopic rdfs:label ?subTopicLabel.
    FILTER ((lang(?Topiclabel) = 'en') && (lang(?subTopicLabel)='en'))
}
```
10. Refereces to Paradise
```
PREFIX : <http://quranontology.com/Resource/>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
select * where
{
    ?s :RefTo ?b. 
    ?b rdfs:label ?a.
     FILTER regex(?a, "paradise", "i")
   
}
```
11. Surah
```
    PREFIX : <http://quranontology.com/Resource/>

PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
SELECT DISTINCT ?Surah ?verse ?topic ?TopicLabel ?person ?entity  WHERE { 
    ?verse a :Verse.
    ?verse :IsPartOf :quran20.
    :quran20 rdfs:label ?Surah.
     OPTIONAL { 
    ?verse :DiscussTopic ?topic.
    ?topic rdfs:label ?TopicLabel.
    }
    OPTIONAL {
        ?verse :ContainsMentionOf ?Person.
        ?Person a :Human.
        ?Person rdfs:label ?person.
    }
        OPTIONAL {
        ?verse :ContainsMentionOf ?Entity.
        ?Entity a :Location.
        ?Entity rdfs:label ?entity.
    }

    FILTER ((lang(?TopicLabel) = 'ar') && (lang(?person)='ar') && (lang(?entity)='ar') && (lang(?Surah)='ar'))
}
```
12. Count of Mentions
    ```
    PREFIX : <http://quranontology.com/Resource/>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX owl: <http://www.w3.org/2002/07/owl#>

SELECT ?mention (COUNT(?mention) AS ?mentionCount)
WHERE {
  ?verse :ContainsMentionOf ?mention.
  ?mention a :Human.
}
GROUP BY ?mention
ORDER BY DESC(?mentionCount)
```


