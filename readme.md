Regular Expresssion
-------------------

> NOTE : By default regular expression are case sensitive

- [Simple String Matching](#simple-string-matching)
- [Meta Characters](#meta-characters)
- [Others](#others)
- [Advanced Pattern Matching](#advanced-pattern-matching)
- [Repetation](#repetation)
- [Wildcard](#wildcard)
- [Escaping](#escaping)
- [Case Insensitive](#case-insensitive)
- [CharacterSets](#character-sets)
- [Character Ranges](#character-ranges)
- [Negated CharacterSets](#negated-character-sets)

## Simple String Matching

###### Eg: in PHP
```
preg_match($pattern, $stringToMatch, $matches);
```

Regular Expresssion          |       String               |            	Match      |     Notes 
---------------------------- | -------------------------  |  --------------------- | -------------
/abc/                        |       abc                  |                Yes      |      As abc is there in the string
/abc/                       |        abcdef               |               Yes       |     As abc is a part of the string
/abc/                       |        bcdef                |               No        |     As string does not contain abc but has only bc
/2:3/                       |        12:34:56             |               Yes       |     As 2:3 exists in string


## Meta Characters

```
\d - Digits from 0-9

\w - Alphabets from a-z, A-Z and Digits from 0-9

\s - Any number of spaces including space, tabs etc

\S - Matches any not whitespace characters

\D - Matches any non digit characters

\W - Matches any non word character

\b - Any boundary word like spaces, dash (-), commas, semi-colons etc
```

## Others 

```
() - Grouping characters the whole express will be acted like a single block 
    Eg: ([A-Z]\w+) - Will match any A to Z character and followed by any no of characters

(|) - OR will match any one of the condition
    Eg: th(at|is|en) - Will match any of that, this or then

\number - Eg: \1 \2
```

Regular Expresssion          |       String               |            	Match      |     Notes 
---------------------------- | -------------------------  |  --------------------- | -------------
/ab\d/               |           ab3                       |          Yes         |    as ab and one digit is there
/abc\d/              |           ab23                      |          No          |    as the string must start with abc and then one digit, but in our string its not there
/\d\d/               |           ab23                      |          Yes         |    As we need 2 digits 23 will match it \d - 1 digit
/\w\s\d/             |           ab 34                     |          Yes         |    As we have b space 3 and our patterns was expecting the same ie character space and digit



## Advanced Pattern Matching

```
^ - Start of string

$ - End of string
```

Regular Expresssion          |       String               |            	Match      |     Notes 
---------------------------- | -------------------------  |  --------------------- | -------------
/^abc/            |          abc               |                      Yes      |       As the string must start with abc
/^abc/            |          abcdef            |                      Yes      |       As the string must start with abc
/^abc/            |          123abcdef         |                      No       |       As the string dont  start with abc but starting with 123
/abc$/            |          123abc            |                      Yes      |       As the string ends with abc
/^abc$/           |          abc               |                      Yes      |       This will match the whole string ie abc
/^abc$/           |          abcdef            |                      No       |       This will match the whole string ie abc but the string has abcdef which wont match


## Repetation

```
* 		- Zero or more

+ 		- One or more

{min, max}	- Repeact the preceding character as many times specified in the {} braces

? 		- Optional character, tells that the preceding charcter may or may not be present 

			Eg: docx? may read to doc or docx
```

Regular Expresssion          |       String               |            	Match      |     Notes 
---------------------------- | -------------------------  |  --------------------- | -------------
/a*bc/      |            abc                 |                        Yes      |       Because 'a' may repeat zero or many times
/a*bc/      |            bc                  |                        Yes      |       Because 'a' may repeat zero or many times
/a+bc/      |            bc                  |                        No       |       Because 'a' may repeat one or many times
/a+bc/      |            bc                  |                        No       |       Because 'a' may repeat one or many times
/a+bc/      |            aabc                |                        Yes      |       Because 'a' may repeat one or many times


## Wildcard

```
. - Match any single character : letter, number, whitespace etc
```

Regular Expresssion          |       String               |            	Match      |     Notes 
---------------------------- | -------------------------  |  --------------------- | -------------
/ab.de/      |       abcde               |                            Yes     |    Because '.' matches any letter, number or whitespace
/ab.de/      |       ab4de               |                            Yes     |    Because '.' matches any letter, number or whitespace
/ab.de/      |       ab de               |                            Yes     |    Because '.' matches any letter, number or whitespace
/ab.de/      |       abde                |                            No      |    Because '.' does not match  0 or more times like * hence there must be atleast one character
/ab.*/       |       abde                |                            Yes     |    Because '.' has '*' which matches  0 or more characters
/ab.*/       |       ab                  |                            Yes     |    Because '.' has '*' which matches  0 or more characters


## Escaping

```
\ - Match meta characters by escaping them
Eg: if you want to match '.' in the pattern then you must escape '.' else the pattern will think that you want to match one character
```

Regular Expresssion          |       String               |            	Match      |     Notes 
---------------------------- | -------------------------  |  --------------------- | -------------
/abc\./     |       abc.                |                             Yes     |    As we have escaped '.' with \. it acts as normal character



## Case Insensitive

By default case sensitive
```
i - to make case insensitive
```

Regular Expresssion          |       String               |            	Match      |     Notes 
---------------------------- | -------------------------  |  --------------------- | -------------
/abc/       |        abc            |                         Yes    |     As it matches
/abc/       |        Abc            |                         No     |     No as the case doesnt match
/abc/i      |        Abc            |                         Yes    |     Because now its matching case insensitive wise with the help of 'i'


## CharacterSets

```
[] - Match one of any characters in the bracket 

	Eg: [abc] will match either a, b or c and nothing else
```

Regular Expresssion          |       String               |            	Match      |     Notes 
---------------------------- | -------------------------  |  --------------------- | -------------
/a[123]b/      |     a2b                       |          Yes     |    as 2 matches in the character set
/a[123]b/      |     a4b                       |          No      |    as 4 does not matches in the character set
/a[123]+b/     |     a122233311b               |          Yes     |    as 123 is there in characterset and + denotes it can have one or more character set of 123



## Character Ranges

```
[ - ] - Specifies the range of the characters inside the characterset
	Eg: [0-9] will match any number between 0 to 9  and nothing else
```

Regular Expresssion          |       String               |            	Match      |     Notes 
---------------------------- | -------------------------  |  --------------------- | -------------
/a[1-5]b/        |   a2b                     |                Yes      |   As 2 is there in the range between 1-5
/a[1-5]b/        |   a6b                    |                 No       |   As 6 is not there in the range between 1-5
/[a-bA-Z0-9 ]+/  |   Hi there               |                 Yes       |  Any character between a-z A-Z 0-9 and Space any number of times repetatively


## Negated CharacterSets

```
[^ ] - This will negate the character set ie it will match any other characrters expect the ones in characterset
```

Regular Expresssion          |       String               |            	Match      |     Notes 
---------------------------- | -------------------------  |  --------------------- | -------------
/a[^1-5]b/     |      a6b                      |               Yes       |     As 6 is not there in the range between 1-5
/a[^1-5]b/    |       a4b                      |               No        |     As 4 is there in the range between 1-5
/[^a-z]/       |     hello                     |               No        |     As a-z is there in the range between a-z
/[^a-z]/      |      HELLO                     |               Yes       |      As a-z is there not in the range between A-Z