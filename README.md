# TypingDNA JavaScript recorder
##### A simple way to capture user’s typing patterns
Full documentation at [api.typingdna.com](https://api.typingdna.com)*

### Usage and description
First you need to import the [typingdna.js](https://typingdna.com/scripts/typingdna.js) file in the page that wants to record a typing pattern. You will need to record typing patterns when a user first creates his account and again whenever you want to authenticate that user on your platform. You can host the .js file yourself.

Alternative locations from where you can include the last class:
* https://typingdna.com/scripts/typingdna.js
* https://api.typingdna.com/scripts/typingdna.js

### TypingDNA class

Once you create an instance of the TypingDNA class, the user typing starts being recorded (as a history of keystroke events). Whenever you want to get the user's typing pattern you have to invoke .getTypingPattern method described in detail below.

**Returns**: Returns the instance of the TypingDNA class (singleton)

**Example**  
```js
var tdna = new TypingDNA();
```
Here are the functions available in the TypingDNA class:
* Main:
* .getTypingPattern(optionsObject) ⇒ `String`
* Optional:
* .addTarget()
* .removeTarget()
* .start()  *Automatically called by default*
* .stop()
* .reset()
* .getQuality(typingPattern) ⇒ `Number`


### TypingDNA.getTypingPattern(optionsObject)
This is the main function that outputs the user's typing pattern as a `String`

**Returns**: A typing pattern in `String` form  

**optionsObject**: An object of the following form {type:Number, text:String, textId:Number, length: Number, targetId:String, caseSensitive:Boolean}. Detail table below.

| Param | Type | Description |
| --- | --- | --- |
| **type** | `Number` | `0 for anytext pattern` (when you compare random typed texts of usually 120-180 chars long) <br> `1 for sametext pattern` (also called diagram pattern, recommended in most cases, for emails, passwords, phone numbers, credit cards, short texts)<br> ` 2 for extended pattern` (most versatile, can replace both anytext and sametext patterns) |
| **text** | `String` | (Only for type 1 and type 2) a typed string that you want the typing pattern for |
| **textId** | `Number` | (Optional, only for type 1 and type 2) a personalized id for the typed text |
| **length** | `Number` | (Optional) the length of the text in the history for which you want the typing pattern, for type 0 is usually 140 or more |
| **targetId** | `String` | (Optional) specifies if pattern is obtain only from text typed in a certain target |
| **caseSensitive** | `Boolean` | (Optional, default: false) Used if you pass a text for type 1 or type 2|

**Examples**  
```js
//anytext pattern
var typingPattern = tdna.getTypingPattern({type=0, length=160});
//sametext pattern
var typingPattern = tdna.getTypingPattern({type=1, text="Hello5g21?*"});
//extended pattern
var typingPattern = tdna.getTypingPattern({type=2, text="example@mail.com"});
```

### TypingDNA.addTarget(element_id)
(Optional) Adds a target to the targetIds array. It has to be a text input or text area or any other HTML DOM element that has the .value property. You can add multiple targets (such as username and password fields).

If you omit adding targets the typing patterns will be recorded for the entire typing session.

**Example**  
```js
TypingDNA.addTarget(emailaddr_id)
TypingDNA.addTarget(password_id)
```

### TypingDNA.removeTarget(element_id)
Remove a target from the targetIds array.

### TypingDNA.reset()
Resets the history stack of recorded typing events.

### TypingDNA.start()
Automatically called at initilization. It starts the recording of typing events. You only have to call .start() to resume recording after a .stop()

### TypingDNA.stop()
Ends the recording of further typing events.

### TypingDNA.getQuality(typingPattern)
Checks the quality of a general typing pattern (type 0), how well it is revelated, how useful the
information will be for matching applications.

**Returns**: `Number` - A real number between `0` and `1`. Values over `0.3` are acceptable, however a value over `0.7` shows good pattern strength.

| Param | Type | Description |
| --- | --- | --- |
| typingPattern | `String` | The type `0` pattern string returned by the getTypingPattern() function. |

**Example**  
```js
var patternQuality = tdna.getQuality(typingPattern);
```

### License
Apache License, [Version 2.0](http://www.apache.org/licenses/LICENSE-2.0)
