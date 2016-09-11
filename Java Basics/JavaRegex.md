## Regex  
java.util.regex API

Follow [Java Docs](https://docs.oracle.com/javase/tutorial/essential/regex/index.html) & [Hackerrank](https://www.hackerrank.com/domains/regex/re-introduction/difficulty/all/page/1)

 Imp classes - [Pattern](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html), [Matcher](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Matcher.html) and [PatternSyntaxException](https://docs.oracle.com/javase/8/docs/api/java/util/regex/PatternSyntaxException.html)

Why does not Pattern have a public constructor? [Answer](http://stackoverflow.com/questions/13758740/java-pattern-class-doesnt-have-a-public-constructor-why)

Pattern.compile(regex_string) -- conveys the purpose of the static method clearly as the regex is compiled to generate the pattern.

PatternSyntaxException - Unchecked exception that indicates a syntax error in a regular expression pattern

Example from [java docs](https://docs.oracle.com/javase/tutorial/essential/regex/test_harness.html):
```java
import java.io.Console;
import java.util.regex.Pattern;
import java.util.regex.Matcher;

public class RegexTestHarness {

    public static void main(String[] args){
        Console console = System.console();
        if (console == null) {
            System.err.println("No console.");
            System.exit(1);
        }
        while (true) {

            Pattern pattern =
            Pattern.compile(console.readLine("%nEnter your regex: "));

            Matcher matcher =
            pattern.matcher(console.readLine("Enter input string to search: "));

            boolean found = false;
            while (matcher.find()) {
                console.format("I found the text" +
                    " \"%s\" starting at " +
                    "index %d and ending at index %d.%n",
                    matcher.group(),
                    matcher.start(),
                    matcher.end());
                found = true;
            }
            if(!found){
                console.format("No match found.%n");
            }
        }
    }
}
```
matcher.end()   -- gives actual end index + 1 as by convention the range is exclusive of the end index.

Metacharacters - The metacharacters supported by the regex API are: ```<([{\^-=$!|]})?*+.>```

There are two ways to force a metacharacter to be treated as an ordinary character:

* precede the metacharacter with a backslash, or
* enclose it within \Q (which starts the quote) and \E (which ends it).  
*Need to escape backslash in Java (\\).*

Construct	| Description
--------- | -----------
[abc]	| a, b, or c (simple class)
[^abc] | Any character except a, b, or c (negation)
[a-zA-Z] |	a through z, or A through Z, inclusive (range)
**[a-d[m-p]]** |	a through d, or m through p: **[a-dm-p]** (union)
[a-z&&[def]] |	d, e, or f (intersection)
[a-z&&[^bc]]	| a through z, except for b and c: **[ad-z]** (subtraction)
[a-z&&[^m-p]]	| a through z, and not m through p: **[a-lq-z]** (subtraction)

*Here class means a character class which specifies the characters that will successfully match a single character from a given input string.*

Regex | Description
----- | -----------
. | Matches any character except for a new line
\s | Matches any whitespace character [ \r\n\t\f ]
\S | Matches any non-whitespace character
^ | Matches the position at the **start** of a string
$ | Matches the position at the **end** of a string
\w | Will match any word character; Word characters include alphanumeric characters (**a-z**, **A-Z** and **0-9**) and underscores (**_**)
\W | Matches non-word character
\d | Matches any digit [0-9]
\D | Matches any character that is not a digit

## Repetitions

* **{x}** will match exactly repetitions of character/character class/groups
* **{x,y}** will match between and (both inclusive) repetitions of character/character class/group.  
e.g. [xyz]{5,} : It will match the characters x, y or z 5 or more times.
* **+** will match one or more repetitions of character/character class/group.
* **\*** will match zero or more repetitions of character/character class/group.


Try [this](https://www.hackerrank.com/challenges/matching-ending-items). The trick here is that the question states the String only consists of lower and upper case characters. So, [a-zA-Z] does not work as it passes 1asd4, 3asd and asd9. We have to make it ^[a-zA-Z]$.
