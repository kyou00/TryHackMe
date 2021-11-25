# Regular Expression / Catregex

Learn and practise using regular expressions

Nov 24, 2021

#### Task 1: Introduction
- Read the above.
  - `no answer needed`

#### Task 2: Charsets-
- Match all of the following characters: c, o, g
  - `[cog]`
- Match all of the following words: cat, fat, hat
  - `[cfh]at`
- Match all of the following words: Cat, cat, Hat, hat
  - `[CcHh]at`
- Match all of the following filenames: File1, File2, file3, file4, file5, File7, file9
  - `[Ff]ile[1-9]`
- Match all of the filenames of question 4, except "File7" (use the hat symbol)
  - `[Ff]ile[^7]`

#### Task 3: Wildcards and optional characters
- Match all of the following words: Cat, fat, hat, rat
  - `.at`
- Match all of the following words: Cat, cats
  - `[cC]ats?`
- Match the following domain name: cat.xyz
  - `cat\.xyz`
- Match all of the following domain names: cat.xyz, cats.xyz, hats.xyz
  - `[ch]ats?\.xyz`
- Match every 4-letter string that doesn't end in any letter from n to z
  - `...[^n-z]`
- Match bat, bats, hat, hats, but not rat or rats (use the hat symbol)
  - `[^r]ats?`
 
#### Task 4: Metacharacters and repetitions
