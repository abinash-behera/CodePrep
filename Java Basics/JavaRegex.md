## Regex  
java.util.regex API

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

Construct	| Description
--------- | -----------
[abc]	| a, b, or c (simple class)
[^abc] | Any character except a, b, or c (negation)
[a-zA-Z] |	a through z, or A through Z, inclusive (range)
**[a-d[m-p]]** |	a through d, or m through p: [a-dm-p] (union)
[a-z&&[def]] |	d, e, or f (intersection)
[a-z&&[^bc]]	| a through z, except for b and c: [ad-z] (subtraction)
[a-z&&[^m-p]]	| a through z, and not m through p: [a-lq-z] (subtraction

*Here class means a character class which specifies the characters that will successfully match a single character from a given input string.*
