## Regex
### Aanchors:

1. #### ^ 
  This matches begining
  
2. #### $
  This matched end
 
 Example : ^The end$ : matches "The end"
 
 ### Quantifiers:
 
1. #### *
   This matches zero or more occurrences
2. #### +
   This matches one or more occurrences
3. #### ?
   This matched zero or one occurence
4. #### {number}
   This matches "number" of times occurenes
5. #### {number, }
   This matches "number" of times to more occurenes
6. #### {number1, number2}
   This matches "number1" of times to "number2" of times occurenes
7. #### (text)
   followed by "text"
   
### OR operator
1. #### | or []
    1. a(b|c)
       - This matches a followed by b or c
    2. a[bc]
       - This matches a followed by b or c
### Character classes
1. #### \d 
   matches a single digit
2. #### \w
   matches a word character including underscore
3. #### \s
   matches a whitespace character, tabs, line breaks
4. #### .
   matches any character
> 1. \D, \W, \S are there as their negations.
> 2. in order to match these characters: ^, $, *, +, ?, (, ), {, |, }, [, ] we need to escape them using `\`.

### Flags
 regex usually comes like this: /regex/. At the end we can specify following:
 1. /g (global): does not return after the first match. restart search from the previous match
 2. /m (multi-line): will match the start and end of the line when '^' and '$' are used.
 3. /i (insensitive): make the whole expression case-insensitive
 
 ### Grouping
 1. #### ()
    this creates a capturing group.
 2. #### ?: inside the patantesis ex: (?:chars)
    this disables the capturing group
 3. ?<name>
    this puts a name to the group
 > * (zero or more occurrences), +(one or more occurrences), and {} are called greedy operatoers as they match as far as then can. 
 
 ### \btext\b 
   this acts like a bounday. same as '^' and '$'
