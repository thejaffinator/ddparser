# JSON archive parser, for use in archiving Dawn Deviants RP chats to the Wiki.

N.B. This is currently Windows only. If anyone archiving wants to run this on a Mac, let me know and I can get that sorted.

## Installation

Click the *Clone or download* button at the top of the main page, then *Download as ZIP*. Extract the zip file, then run the parser by opening *jsonparser_v3.x.x.exe*.

## JSON Preparation

Once you've requested and downloaded your Messenger archive in .json format from Facebook, it'll require a little bit of preparation before it can be fed to the parser. Open up the json for the chat you're archiving (a more advanced text editor such as Notepad++ or Sublime Text would be best, but Notepad or Wordpad would do in a pinch. **DO NOT** open jsons in MS Word) and find the section of RP you're looking to extract. **NOTE:** the chats in json archives will appear chronologically back to front, so newer messages will be towards the top while older messages will be further down.

Highlight the section you're extracting, **paying close attention to the locations of the curly brackets at the top and bottom of your selection** (see below). The function that reads json is very picky about brackets, so this is crucial to getting the program to parse correctly. Copy/paste this into a new text document, and save this as a new .json file (file name doesn't matter). The resulting file should now look something like this:

![Creation of a parsable .json](/readme_media/json_prep_1.png)

**The first line should be a single open curly bracket, while the last line should be a single curly closed bracket followed by a comma.**

#### Formatting

N.B. Since we have moved to standardising our text formatting in Messenger, this step should become more unnecessary for more recent RPs. However, it should still be performed as a quick sanity check unless you're SURE all speech was denoted properly in the chat.

Due to it being very difficult for a computer to understand the use of apostrophes for denoting speech, any such apostrophes need to be changed to speech marks before parsing so that the parser can identify speech and mark it as such. This is thankfully very easy in most modern text editors, using *Find and Replace*. The example below is the Find and Replace feature in Sublime text, but other text editors should function equivalently.

Place the typing cursor at the start of the newly made .json, and open your program's *Find and Replace* function. In *Find:* enter a single apostrophe (') and in *Replace:* enter a backslash followed by a speech mark (\\"):

![Find and Replace function in Sublime Text](/readme_media/json_prep_2.png)

Clicking *Find* will then take you through every instance of a single apostrophe in your text. However, we only want to replace apostrophes being used to denote speech, not ones being used as contractions:

![Apostrophes used for speech vs. as contractions](/readme_media/json_prep_3.PNG)

In the above image, the highlighted (yellow) apostrophe is being used as a contraction and should NOT be replaced. The outlined apostrophes at the start and end of the speech SHOULD be replaced. Note that all messages are also surrounded by speech marks, which denotes them as text that can be read by the parser. These should not be confused with **what the parser reads as speech marks**, which are shown as \\".

It is possible to make this process very efficient and easy with shortcuts, eg. in Sublime Text the *Find* button is mapped to F3 on the keyboard while the mouse can be positioned over *Replace* to quickly go through the whole document and get rid of any offending apostrophes.

## Parsing

The actual parser program is pretty simple to operate. Just load it up, select the input json you've just created and give it a place to save the output text file. Then select the character that each person is playing in this RP - don't worry if there are people in the list that aren't in the RP you're parsing, the program will ignore those names. If a player is using a character not in their list, or if someone else is DMing, select *Other* in that player's list and enter the name of the character in the box to the right. Right now we don't have any specific syntax laid out for a player using multiple characters in one RP, so it's best to just use the character they RP as most when parsing and then correct it later.

The selected RP can then be parsed by clicking *Parse Text*. This will output a .txt file to the path you specified above, which can then be copy/pasted straight into the Wiki.

The Debug option at the bottom just saves a version of the internally preparsed text, where it is made back into a legible json file. This can normally be left off, but can be useful when reporting bugs.

## Cleaning Up

These are general tips that should be observed when using parsed chats. Any corrections should be performed on the Wiki, so you can use the *Show preview* button to check that the changes you're making are all good. It is advised that you have the original RP open in Messenger at the same time, so you can cross-check between the two.

#### Speech consistency

Have a quick skim through what is being classed as speech (it can help to preview the Wiki article so the formatting is applied) to make sure it is all consistent and nothing which should be speech isn't speech (and vice-versa). If this is the case, then you've probably just missed changing a single quotation mark into an escaped speech mark, as described in **Formatting**. Go back to your prepared json and check you've nabbed all of them, then parse the text again.

#### Parentheses

The parser takes anything in normal brackets to be an out of character aside comment, and therefore does not include them (since this appears to be the majority use case of these types of brackets). This is mostly the correct thing to do, but in some cases players may place important information such as their character's current thoughts in these brackets. If this is the case, this information will need to be copied from the brackets (easiest to see in Messenger) and placed back into the main text after parsing.

#### DM

Due to the ever-changing nature of the character the DM plays (if even playing a character at all), the parser tags all text given by the DM as such. This is pretty self-explanatory, just change it after parsing to whichever character is being played for each message, or remove the tag if it's something like an environment description that isn't attributed to a character.

## Updates

The program will need to be updated from time to time, as new bugs are discovered or new players join the campaign. This Github repo will host the most up to date version, so just redownload the zip and replace the old version as needed. I'll try to keep everyone using the program up to date on the Archival chat if there are any updates.

## Source Code

Due to privacy issues, the Python source code is hosted on a separate private repository. If you'd like access for development purposes, let me know and I'll get you added to that repo.
