
# Messages

We all like to use programs that let us know what's going on. Programs that keep us informed often do so by displaying status and error messages. Of course, these messages need to be translated so they can be understood by end users around the world. The section
[Isolating Locale-Specific Data](../resbundle/index.html) discusses translatable text messages. Usually, you're done after you move a message `String` into a `ResourceBundle`. However, if you've embedded variable data in a message, you'll have to take some extra steps to prepare it for translation.

A **compound message** contains variable data. In the following list of compound messages, the variable data is underlined:

```

The disk named <u>MyDisk</u> contains <u>300</u> files.
The current balance of account <u>#34-09-222</u> is <u>$2,745.72</u>.
<u>405,390</u> people have visited your website since <u>January 1, 2009</u>.
Delete all files older than <u>120</u> days.

```

You might be tempted to construct the last message in the preceding list by concatenating phrases and variables as follows:

```

double numDays;
ResourceBundle msgBundle;
// ...
String message = msgBundle.getString(
                     "deleteolder" +
                     numDays.toString() +
                     msgBundle.getString("days"));

```

This approach works fine in English, but it won't work for languages in which the verb appears at the end of the sentence. Because the word order of this message is hardcoded, your localizers won't be able to create grammatically correct translations for all languages.

How can you make your program localizable if you need to use compound messages? You can do so by using the `MessageFormat` class, which is the topic of this section.

Compound messages are difficult to translate because the message text is fragmented. If you use compound messages, localization will take longer and cost more. Therefore you should use compound messages only when necessary.

## [Dealing with Compound Messages](messageFormat.html)

A compound message may contain several kinds of variables: dates, times, strings, numbers, currencies, and percentages. To format a compound message in a locale-independent manner, you construct a pattern that you apply to a `MessageFormat` object.

## [Handling Plurals](choiceFormat.html)

The words in a message usually vary if both plural and singular word forms are possible. With the `ChoiceFormat` class, you can map a number to a word or phrase, allowing you to construct messages that are grammatically correct.
