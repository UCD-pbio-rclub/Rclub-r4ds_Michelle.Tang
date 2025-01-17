---
title: "R-Club-July12"
author: "Michelle Tang"
date: "7/7/2017"
output: html_document
---


```r
library(tidyverse)
```

```
## Loading tidyverse: ggplot2
## Loading tidyverse: tibble
## Loading tidyverse: tidyr
## Loading tidyverse: readr
## Loading tidyverse: purrr
## Loading tidyverse: dplyr
```

```
## Conflicts with tidy packages ----------------------------------------------
```

```
## filter(): dplyr, stats
## lag():    dplyr, stats
```

```r
library(stringr)
```

1) Section 14.1 and 14.2 in the book (and exercises)

### 14.2.5 Exercises

1. In code that doesn’t use stringr, you’ll often see paste() and paste0(). What’s the difference between the two functions? What stringr function are they equivalent to? How do the functions differ in their handling of NA?

paste and paste0 concatenate vectors after converting to character.

paste default sep is a space whereas paste0 has no sep.

The paste functions are similar to str_c(). str_c will skip the NA but paste() coerces NA character. In stringr, will have to specify str_replace_na()

2. In your own words, describe the difference between the sep and collapse arguments to str_c().

In sep, if pasting two vectors of string, will insert whatever sep is specified in between the two inputs as going through vector. I.e. if the two input vectors is sep by a character, the output will be the same length longest vector.

In collapse, will insert whatever collapse is specified between each element in input vector, and make entire input vector into a single string. The output vector will include one element

3. Use str_length() and str_sub() to extract the middle character from a string. What will you do if the string has an even number of characters?


```r
odd <-c("abcdefg")
odd
```

```
## [1] "abcdefg"
```

```r
str_sub(odd, start = str_length(odd)/2+1, end = str_length(odd)/2+1)
```

```
## [1] "d"
```

```r
even <-c("abcdef")
even
```

```
## [1] "abcdef"
```

```r
#take both middle
str_sub(even, start = str_length(even)/2, end = str_length(even)/2+1)
```

```
## [1] "cd"
```

```r
# If I write it in a function
str_ex<-function(x){
  if(str_length(x) %% 2 ==0){
    str_sub(x, start = str_length(x)/2, end = str_length(even)/2+1)
  }
  else{
    str_sub(x, start = str_length(x)/2+1, end = str_length(x)/2+1)
  }
}
```

4. What does str_wrap() do? When might you want to use it?


```r
?str_wrap
```

I can see myself use it for multi-line labels

breaks text into lines of specific widths and adds indents

5. What does str_trim() do? What’s the opposite of str_trim()?

Trim whitespace from start and end of string

str_pad() adds whitespace

6. Write a function that turns (e.g.) a vector c("a", "b", "c") into the string a, b, and c. Think carefully about what it should do if given a vector of length 0, 1, or 2.


```r
turn_vector <- function(x){
  if(length(x) > 1){
    str_c(x, collapse = ", ")
  }
  else{
    print(x)
  }
}
```


### The tutorial on regular expression at https://regexone.com/

Exercise 1: Matching Characters

Task	Text	 

Match	abcdefg	To be completed

Match	abcde	To be complete

Match	abc

`abc`

Exercise 1½: Matching Digits

Task	Text	 

Match	abc123xyz	Success

Match	define "123"	Success

Match	var g = 123;

`123`

Exercise 2: Matching With Wildcards

Task	Text	 

Match	cat.	Success

Match	896.	Success

Match	?=+.	Success

Skip	abc1

`...\.`

Exercise 3: Matching Characters

Task	Text	 

Match	can	Success

Match	man	Success

Match	fan	Success

Skip	dan	To be completed

Skip	ran	To be completed

Skip	pan	

`[cmf]an`

Exercise 4: Excluding Characters

Task	Text	 

Match	hog	To be completed

Match	dog	To be completed

Skip	bog

`[^b]og`

Exercise 5: Matching Character Ranges

Task	Text	 

Match	Ana	Success

Match	Bob	Success

Match	Cpc	Success

Skip	aax	To be completed

Skip	bby	To be completed

Skip	ccz

`[A-C][n-p][a-c]`

Exercise 6: Matching Repeated Characters

Task	Text	 

Match	wazzzzzup	Success

Match	wazzzup	Success

Skip	wazup

`waz{3,5}up`

Exercise 7: Matching Repeated Characters

Task	Text	 

Match	aaaabcc	Success

Match	aabbbbc	Success

Match	aacc	Success

Skip	a

`aa+b*c+`

Exercise 8: Matching Optional Characters

Task	Text	 

Match	1 file found?	Success

Match	2 files found?	Success

Match	24 files found?	Success

Skip	No files found.

`\d+ files? found\?`

Exercise 9: Matching Whitespaces

Task	Text	 

Match	1.   abc	Success

Match	2.	abc	Success

Match	3.           abc	Success

Skip	4.abc	To be completed

`[1-3].\s+abc`

Exercise 10: Matching Lines

Task	Text	 

Match	Mission: successful	Success

Skip	Last Mission: unsuccessful	To be completed

Skip	Next Mission: successful upon capture of target

`^Mission: successful$`

Exercise 11: Matching Groups

Task	Text	Capture Groups	 

Capture	file_record_transcript.pdf	file_record_transcript	Success

Capture	file_07241999.pdf	file_07241999	Success

Skip	testfile_fake.pdf.tmp		Failed

`^(file_.+)\.pdf$`

Exercise 12: Matching Nested Groups

Task	Text	Capture Groups	 

Capture	Jan 1987	Jan 1987 1987	Success

Capture	May 1969	May 1969 1969	Success

Capture	Aug 2011	Aug 2011 

`(\D{3} (\d{4}))`

Exercise 13: Matching Nested Groups

Task	Text	Capture Groups	 

Capture	1280x720	1280 720	Success

Capture	1920x1600	1920 1600	Success

Capture	1024x768	1024 768	Success

`(\d{4})x(\d+)`

Exercise 14: Matching Conditional Text

Task	Text	 

Match	I love cats	Success

Match	I love dogs	Success

Skip	I love logs	To be completed

Skip	I love cogs

`I love (cats|dogs)`

### The practice problems on regular expressions at https://regexone.com/problem/matching_decimal_numbers

Exercise 1: Matching Numbers

Task	Text	 

Match	3.14529	Success

Match	-255.34	Success

Match	128	Success

Match	1.9e10	Success

Match	123,340.00	Success

Skip	720p	Failed

`^-?\d+(,\d+)*(\.\d+(e\d+)?)?$`

Exercise 2: Matching Phone Numbers

Task	Text	Capture Groups	

Capture	415-555-1234	415	Success

Capture	650-555-2345	650	Success

Capture	(416)555-3456	416	Success

Capture	202 555 4567	202	Success

Capture	4035555678	403	Success

Capture	1 416 555 9292	416	Success

`1?[\s-]?\(?(\d{3})\)?[\s-]?\d{3}[\s-]?\d{4}`

Exercise 3: Matching Emails

Task	Text	Capture Groups	 

Capture	tom@hogwarts.com	tom	Success

Capture	tom.riddle@hogwarts.com	tom.riddle	Success

Capture	tom.riddle+regexone@hogwarts.com	tom.riddle	Success

Capture	tom@hogwarts.eu.com	tom	Success

Capture	potter@hogwarts.com	potter	Success

Capture	harry@hogwarts.com	harry	Success

Capture	hermione+regexone@hogwarts.com	hermione	Success

`([\w\.]*)(\+regexone)?@hogwarts\.(eu\.)?com`

`([\w\.]*)\D+`

Exercise 4: Capturing HTML Tags

Task	Text	Capture Groups	

Capture	<a>This is a link</a>	a	Success

Capture	<a href='https://regexone.com'>Link</a>	a	Success

Capture	<div class='test_style'>Test</div>	div	Success

Capture	<div>Hello <span>world</span></div>	div	Success

`<(\w+)\D+`

Exercise 5: Capturing Filename Data

Task	Text	Capture Groups	 

Skip	.bash_profile		To be completed

Skip	workspace.doc		To be completed

Capture	img0912.jpg	img0912 jpg	Success

Capture	updated_img0912.png	updated_img0912 png	Success

Skip	documentation.html		To be completed

Capture	favicon.gif	favicon gif	Success

Skip	img0912.jpg.tmp		To be completed

Skip	access.lock		To be completed

`^(\w+)\.(jpg|png|gif)$`

Exercise 6: Matching Lines

Task	Text	Capture Groups	 

Capture				The quick brown fox...	The quick brown fox...	Success

Capture	   jumps over the lazy dog.	jumps over the lazy dog.	Success

`[\s]?(\w+\s\w+\s\w+\s\w+(\.(\.\.)?)?(\s\w+\.)?`

Exercise 7: Extracting Data From Log Entries

Task	Text	Capture Groups	 

Skip	W/dalvikvm( 1553): threadid=1: uncaught exception		To be completed

Skip	E/( 1553): FATAL EXCEPTION: main		To be completed

Skip	E/( 1553): java.lang.StringIndexOutOfBoundsException		To be completed

Capture	E/( 1553):   at widget.List.makeView(ListView.java:1727)	makeView ListView.java 1727	Success

Capture	E/( 1553):   at widget.List.fillDown(ListView.java:652)	fillDown ListView.java 652	Success

Capture	E/( 1553):   at widget.List.fillFrom(ListView.java:709)	fillFrom ListView.java 709	Success

`E/\(\s\d{4}\):\s\s\s\at\swidget\.List\.(\w+)\((ListView.java)\:(\d+)\)`

Exercise 8: Extracting Data From URLs

Task	Text	Capture Groups	 

Capture	ftp://file_server.com:21/top_secret/life_changing_plans.pdf	ftp file_server.com 21	Success

Capture	https://regexone.com/lesson/introduction#section	https regexone.com	Success

Capture	file://localhost:4040/zip_file	file localhost 4040	Success

Capture	https://s3cur3-server.com:9999/	https s3cur3-server.com 9999	Success

Capture	market://search/angry%20birds	market search	Success

`(\w+)://((\w+(\.|-)?\w+)?(\.\w+)?)(:|/)(\d+)?.*`

[OPTIONAL] The beginner crosswords at https://regexcrossword.com/  (See https://regexcrossword.com/howtoplay for how to play)


### 14.3.5.1 Exercises

Describe, in words, what these expressions will match:

(.)\1\1

any character repeated 3x

"(.)(.)\\2\\1"

character1, character2, character2, character1

(..)\1

character1, character2, character1, character2

"(.).\\1.\\1"

character1 character2 character1 . character1

"(.)(.)(.).*\\3\\2\\1"

character1, character2 character3 any character 0 or more times, character3, character2, character1

2. Construct regular expressions to match words that:

Start and end with the same character.

`^(.).*\1$`

Contain a repeated pair of letters (e.g. “church” contains “ch” repeated twice.)

`^(..).*\\1$`

Contain one letter repeated in at least three places (e.g. “eleven” contains three “e”s.)

`(.).*\\1.*\\1`

