# Everett Student Projects
This repo is here to teach a lesson about reformating data from one source and getting it ready for another platform. It also explores on the issues and limitations of the CSV format.

**Update 07/17/15**
Some of the coordinates in the projects were messed up somehow. It's pointless work to go back and fix them, so we'll only be correcting one: Everett-Projects-Map-Data.csv because that's the one we'll be using to update the map data on the main site.

====
## Cleaning Data
You'll often get data from one source and need to put it into another. In a perfect world, everything works with everything else, but we don't live in that world.
### raw.csv
This file contains the map data as it was exported from the Everett website back in Winter of 2015. It's unusable in this form, but it can actually be fixed in only a few steps. Find out how in [This Screencast](https://www.youtube.com/watch?v=-mspWUFXTJI)!

## Dealing with Commas and Paragraph Text
The problem with Comma Separated Values (CSV) format is that it can give you problems when you're trying to put paragraph data in one of the columns. In the case of this map data, regarding Everett student projects, we have all the project vitals (location, project title, etc.) and at the end we have a paragraph describing the project in the column "Description".

Paragraphs often contain numerous sentences, and some of those sentences will invariably contain multiple clauses which are separated by...Commas! Without taking special steps, these commas will be interpated as being the same as the commas that separate your columns instead of part of a paragraph. Consequently, everything gets all messed up. This repo is to explore various ways of dealing with this issue.

 
### projects.csv
By wrapping the "Description" paragraph in double quotes, we signal that everything inside the quotes should be treated as part of a single paragraph. In other words, the commas inside the quotes are not delimeters, they are a string.

#### A Note on Placing Quotes in a CSV
It can be very tricky to put quotes into the proper place in a CSV. Think about how you would actually go about doing it. A CSV file doesn't have easily human readable columns, just commas. You could open a CSV in Excel, but it's still going to see those commas as new columns. So how are you supposed to put them at the beginning and end of the description?

One way of doing this is to leverage the ultra-powerful concept of "Regular Expressions" or "Regex" to understand the pattern we are trying to create. Regex is basically a sophisticated form of find and replace that uses symbols to represent patterns of text rather than exact matches.

<!--
**What Are We Trying To Do?**: We want to put a double quote at the very beginning of the "Description" collumn as well as the very end.

**What That Means in Terms of Patterns**: All the rows look the same. There is text separated by commas until we get to the column we want. There are 5 columns before **Descriotion**, so what we need to do is find a way to write that pattern. The following command will find everyting in a row up to and including the comma just before text within the **Descrition** column. It saves this pattern and replaces it with the exact same thing, but now with a quotation mark at the end 

Find:

	^([^,]*\,[^,]*\,[^,]*\,[^,]*\,)
Replace:

	\1"
-->


### projects.tsv
If CSV is **Comma** Separated Values, then TSV is obviously **Tab** Separated Values. This is simply a matter of saying that tabs are the delimiting character rather than commas.

### using-html-entities.csv
Symbols like typographer quotes (&ldquo; &rdquo;), pilcrows (&para;), and accent marks (&aacute;, &eacute;, &iacute;) won't show up if you put them directly into your html. The browser doesn't know what to do with them. Instead you have to use an "HTML Enitity". This consists of typing an ampersand, the entity value, and a semicolon. Some examples:

* Euro Sign - &euro; = `&euro;`* 
* Trademark - &trade; = `&trade;`
* Alembic - &#9879; = `&#9879;`

Ok I have no clue why there is an alembic symbol, but there it is. You can find plenty of comprehensive entity references online. [HTML Arrows](http://htmlarrows.com/symbols/) has a nice format.

Anyway, by repalacing all the paragraph commas with comma entities, we'll avoid delimiter errors. The code for comma is, `&comma;`. Think you can remember that?