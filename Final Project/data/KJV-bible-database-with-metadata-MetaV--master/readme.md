**THIS REPOSITORY IS NO LONGER ACTIVELY MAINTAINED**

*Contact robert@viz.bible to request access to the actively maintained data.*

## What is MetaV?
MetaV is the name given to the underlying database used to build the visual Bible explorer and several other infographics. It links together details on people, places, periods of time, and passages in the Bible at word-level detail. This database is specially structured to simplify complex big picture analysis or visualizing biblical information.

## Tables, fields, descriptions

### BookAliases
Correlates all known book titles and abbreviations to a specific book ID
- BookID - Numerical Id corresponding to the full name and other info in the Books Table
- Alias - Variant spellings and abbreviations of each book.

### Books
Standardizes all Bible book names with a given numerical ID
- BookID - Numerical value 1-66 assigned to each book in canonical order.
- BookName - The full name of the book
- NumOfChapters - The number of chapters in the book.
- BookDiv - Major divisions: Historical, Poetical, Gospels, Etc.
- ShortName - Smallest possible unique book abbrevation
- OsisName - Standard OSIS book name abbrevitaion

### CrossRefIndex
Compilation of cross references obtained from R.A. Torrey's Treasury of Scripture Knowledge (Public Domain) Duplicate cross-references have been excluded.
	
- VerseID - Primary verse by ID from the Verses table.
- VerseRefID - Verse ID (from Verses table) to which the primary verse refers.

### MainIndex
The main index associating the various tables in this database with individual words.  Text used: 1769 Cambridge Edition of the King James Version, also known as the Authorized Version (Public Domain)
	
- BookID - Number corresponding to the book title in the Books table.
- Chapter - Chapter number in the referenced book.
- ParaID - Number assigned to each paragraph in canonical order for the entire Bible.
- SentID - Number assigned to each sentence in canonical order for the entire Bible.
- VerseID - Number corresponding to the verse in the verses table in canonical order for the entire Bible.
- VerseNum - The standard verse number within the referenced chapter.
- VersePos - Number referencing an individual word's position within a verse.  Negative numbers indicate introductory text.
- WordID - Number assigned to each word in canonical order for the entire Bible.
- Word - The individual English word.
- Punc - The punctuation mark immediately following the word, excluding parentheses.
- Italic - True/False indicating whether the word is italicized in the source text.
- cParen - True/False indicating whether the word is followed by a closing parenthesis.
- oParen - True/False indicating whether the word is preceded by an open parenthesis.
- PlaceID - Number corresponding to a record in the Places table.
- Syllables - The number of syllables in the word.
- YearNum - The approximate year of the event described or the time a prophecy was given.  Negative numbers are BC, positive numners are A.D.  Source: Annals of the World, James Ussher and R.A. Torrey, Treasury of Scripture Knowledge.  Public Domain.
- PersonID - Number corresponding to a record in the People table.
- RunCharLen - running count of characters restarting for every SentenceID, used for readability calculations

### People
Listing of all people in the Bible and key facts about them.  This is a mashup of data found at www.complete-bible-genealogy.com and www.marshallgenealogy.org/bible.  Name spelling has been updated to match the source bible text.
	
- PersonID - Unique numerical value assigned to each individual.
- Name - The given name by which the individual is most often referred in the source text.
- Surname - An indivu=idual's surname, if known.
- IsProperName - True indicates the name is a proper name.  False indicates that the name is simply a description of the person where no proper name is given in the text.
- Gender - Male or Female. Eunuchs may be specified in later revisions.
- BirthYear - The approximate year a person was born. Note: may not correspond with the year in the MetaV table.
- DeathYear - The approximate year a persondied. Note: may not correspond with the year in the MetaV table.
- BirthPlace - The name of the place the person was born.
- DeathPlace - The name of the place the person died or was transfigured.

### PeopleAliases
All known aliases by which a person is referred to in the KJV as well as variant spellings from the source websites.
	
- PersonID - Unique identifier corresponding to the People table.
- Alias - Known aliases or alternate spellings for the individual's name.

### PeopleRelationships
All known relationships between people listed in the KJV.  Note: `Father` may refer toa  more distant ancestor.  This and `spouseOrConcubine` relationships will be disambiguated in a later revision.
- Primary - Unique identifier for the person corresponding to the People table.
- RelatedTo - Unique identifier for the related perrson corresponding to the People table.
- RelType - The relationship the "Primary" Person has with the "RelatedTo" person, as in: Primary->Adam, Relatedto->Cain, RelType->Father, or "Adam is Cain's Father"

### PeopleGroups
Groups to which individuals belong.
- PersonID - Unique identifier for a person
- GroupName - The group to which the person belongs

### PlaceAliases
All names by which a particular place is referred to in the KJV & variant spellings from the ESV.  
	
- PlaceID - Unique identifier for each place
- Alias - All names and alrternate spellings which refer to that location.

### Places
All identifiable places mentioned in the bible.  Locations may be approximate.  Source: www.openbible.info/geo (Creative Commons Attribution License).  Place references in time periods prior to Noah's Flood have been removed.
	
- PlaceID - Unique identifier
- PlaceName - Name of the place according to the source table from openbible.info.  May not correspond to KJV name.
- Root - Original place name, if it ahs changed over time.
- Comment - Clarifying comments from source tables at openbible.info
- Lat - Latitude in decimal form.
- Lon - Longitude in decimal form.
- PlaceMarkID - foreign key to match with the PlaceMarks table.

### PlaceMarks
Unique Latitude and Longitude from the Places Table with the most common place name as the Label.

- PlaceMarkID - Unique identifier
- Latitude - Latitude in decimal form.
- Longitude - Longitude in decimal form.
- Label - Most common name used in the Bible for a unique lat/long coordinate.

### Strongs
Strong's Concordance in Hebrew and Greek.  Source: [openscriptures/strongs](https://github.com/openscriptures/strongs) License: Creative Commons Attribution-ShareAlike 3.0
	
- StrongsID - Unique identifier. Greek entries are preceded by "G" adn Hebrew entries are preceded by "H"
- lemma - the original language form of the word
- xlit - transliteration into English
- pronounce - Guide to  pronunciation of the word in its original language.
- description - Stong's Definition of the Greek or Hebrew word, including word origin, long and short definitions.
- PartOfSpeech - indicates noun, verb, proper name, etc.
- Language - Greek, Hebrew (heb), Aramaic "arc", or Greek Proper Noun "x-pn"

### StrongsIndex
*DEPRECATED DUE TO MISSING DATA*
Correlates Stong's Number(s) with individual words in the KJV.
	
- StrongsID - Unique ID corresponding to Strongs table.
- WordID - The word associated with the Srong's number.

### TopicIndex
Correlates topics with each verse in the KJV.
	
- TopicID - Number corresponding to a record in the Topics table.
- VerseID - The verse to which the topic refers.

### Topics
Mashup of Torrey's New Topical Textbook.  Public Domain.
	
- TopicID - Unique identifier for each topic.
- Topic - The main topic heading as it appears in Nave's or Torrey's
- Subtopic - The sub topic heading as it appears in Nave's or Torrey's

### Verses
Full text of each verse in the King James Version of the Holy Bible.
	
- VerseID - Unique identifier for every verse in the Bible, in canonical order.
- BookID - Number corresponding to a record in the Books table.
- Chapter - The chapter in which the verse appears.
- VerseNum - The verse number within the chapter.
- OsisRef - Standardized OSIS form, Book.Chapter.Verse
- VerseText - Full text of the verse as it appears in the KJV, 179 Canbridge Edition.

### Writers
Lists authors of each book of the Bible.  Where one book may have had more than one writer, the primary author's name is used.
	
- BookID - Number corresponding to a record in the Books table.
- Writer - The name of the person who wrote the book, or the primary author of a book with multiple authors.


## License
All files Copyright 2013-2016 viz.bible
This work is free to use and copy under a creative Commons Attribution Share-Alike 3.0 License.  See individual table information for details on original sources and licensing permissions.

Last updated 4-28-2016.
