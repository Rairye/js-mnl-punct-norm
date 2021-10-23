# js-mnl-punct-norm

Tool for stripping and normalizing punctuation and other non-alphanumeric characters. Supports multiple natural languages. Useful for scrapping, machine learning, and data analysis.

Note: "non-alphanumeric characters" include characters such as emojis and pictographs. Whitespace characters are not included. (If you would like to normalize whitespace characters, please see https://github.com/Rairye/js-mnl-ws-norm ) 

Hereinafter, the terms "punctuation marks" and "punctuation" refer to both punctuation marks and other non-alphanumeric characters.

## Installation

npm install mnl-punct-norm

## function isPunct(char)

Required parameter -> char

Note: char must be a string with length of 1.

```javascript

import {isPunct} from 'mnl-punct-norm';

//Half-width period used in English, etc.
console.log("Half-width period isPunct -> " + isPunct("."));

//Full-width period used in Japanese, etc.
console.log("Full-width period isPunct -> " + isPunct("。"));

//Hiragana character
console.log("Hiragana character isPunct -> " + isPunct("あ"));

//Kanji
console.log("Kanji character isPunct -> " + isPunct("私"));

//Pictograph example
console.log("★ isPunct -> " + isPunct("★"));
```

## function stripPunct(inputStr, inputSkips = "")

This function strips all punctuation marks from a string.

Required parameter -> inputStr

inputStr is the string from which punctuation marks are to be stripped.

inputStr must be passed as a string.

Optional parameter -> inputSkips

inputSkips is a string containing a sequence of punctuation marks that are not to be stripped from inputStr. 

inputSkips must be passed as a string. 

```javascript

import {stripPunct} from 'mnl-punct-norm';

var sourceStr = "This light-weight module, which provides multi-language support, normalizes punctuation in strings.";

//Strips all punctuation from sourceStr.
console.log(stripPunct(sourceStr));

//Strips all punctuation from sourceStr, except for hyphens.
console.log(stripPunct(sourceStr, "-"));

//Strips all punctuation from sourceStr, except for hyphens and commas.
console.log(stripPunct(sourceStr, "-,"))

var japaneseStr = "私は人間（にんげん）です。";

//Strips all punctuation from japaneseStr.
console.log(stripPunct(japaneseStr));

//Strips all punctuation from japaneseStr, except for parentheses.
console.log(stripPunct(japaneseStr, "（）"));

```

## function replacePunct(inputStr, inputSkips = "", replacement= " ")

This function replaces all punctuation marks in a string with either a half-width space (default) or a user-specified string.

Required parameter -> inputStr

inputStr is the string in which punctuation marks are to be replaced. inputStr must be passed as a string.

Optional parameters -> inputSkips, replacement

inputSkips is a string containing a sequence of punctuation marks that are not to be replaced with the replacement string. 

inputSkips must be passed as a string. 

replacement is a string that is used to replace punctuation marks (a half-width space by default). 

replacement must be passed as a string. 

Note: If the replacement string follows a space or other substring that is equal to the replacement string, the replacement string will not be added (to avoid creating extra spaces/substrings in the string returned by the function). 

Also, in cases where multiple punctuation marks are used sequentially, only a single instance of the replacement string will be used.

Note: There may be leading/trailing spaces in the string returned by the function, so you may want to use the trim() method if necessary.

```javascript
import {replacePunct} from 'mnl-punct-norm';

//Replaces all punctuation in sourceStr with a half-width space.
console.log(replacePunct(sourceStr));

//Replaces all punctuation in sourceStr with " <PUNCT> ".
console.log(replacePunct(sourceStr, "", " <PUNCT> "));

//Replaces all punctuation in japaneseStr with a full-width space.
console.log(replacePunct(japaneseStr, "", "　"));

//String with multiple punctuation marks. The extra spaces in the string are not normalized by the function.
var multiplePunctStr = "Wha ... what are you     doing!?!?";

//Example in which multiple punctuation marks are used in a row.
console.log(replacePunct(multiplePunctStr));

//Example in which multiple punctuation marks are used in a row, with replacement passed as " <PUNCT> ".
console.log(replacePunct(multiplePunctStr, "", " <PUNCT> "));
```

## Use Case: Removing non-standard punctuation marks (such as emojis) while keeping standard punctuation marks

There may be cases where you only want to remove non-standard punctuation marks (such as in text taken from reviews, comment sections, or other places on the Web).

```javascript
import {stripPunct} from 'mnl-punct-norm';

var englishPunct = "\"!#$%&\'()=-~^\\|[]{}:*;+,.<>?/_";

//Source string containing both standard and non-standard punctuation marks.
var sourceStr = "★♡▲ Have a nice day!! ★♡▲";

//Non-standard punctuation marks are removed, while the standard punctuation marks remain.
console.log(stripPunct(sourceStr, englishPunct));

```

## Other Languages

Python -> https://github.com/Rairye/mnl-punct-norm
