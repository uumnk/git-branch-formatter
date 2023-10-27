# git-branch-formatter
Utility for creating GIT branch names out of feature names

## Version
1.0.0

## Description
This utility helps you to create GIT branch names like `feature/ABC-123-New_feature` from common text to GIT-compatible format.
You can set a pattern and fill parameters to it. Each of the parameters is converted to GIT-compatible format according to following formatting table.
Then, the parameters are put together into the branch name according to given pattern (which is not further formatted).

### Formatting table
Each input parameter is formatted according this table, in following order:

| Action                                                                        | Find                            | Replace by                   |
|:------------------------------------------------------------------------------|---------------------------------|------------------------------|
| remove diacritics                                                             | (any diacritics)                | (letters without diacritics) |
| trim the string                                                               | (whitespaces on the start or end) | `""` (remove)                |
| remove spaces around dashes                                                   | `" - "`                         | `"-"`                        |
| remove spaces around slashes and convert them to dashes                       | `" / "`                         | `"-"`                        |
| remove spaces around backslashes and convert them to dashes                   | `" \ "`                         | `"-"`                        |
| remove space after commas and convert it to underscores                       | `", "`                          | `"_"`                        |
| convert all remaining commas to underscores                                   | `","`                           | `"_"`                        |
| convert all tildes to dashes                                                  | `"~"`                           | `"-"`                        |
| convert all remaining slashes to dashes                                       | `"/"`                           | `"-"`                        |
| convert all remaining backslashes to dashes                                   | `"\"`                           | `"-"`                        |
| convert all at signs to underscores                                           | `"@"`                           | `"_"`                        |
| convert all pipes to underscores                                              | `"\|"`                          | `"_"`                        |                              |
| convert all remaining spaces to underscores                                   | `" "`                           | `"_"`                        |
| remove all dots at the beginning                                              | `/^\.+/g`                       | `""` (remove)                |
| remove all dots at the end                                                    | `/\.+$/g`                       | `""` (remove)                |
| convert all remaining dots to underscores                                     | `"."`                           | `"_"`                        |
| remove everything else except alphanumeric characters, underscores and dashes | `/[^a-zA-Z0-9_-]/g`             | `""` (remove)                |

(these replacements are not configurable at this time)

## Usage
1. Go to http://uumnk.github.io/git-branch-formatter
2. Enter your GIT branch pattern (or leave the default if it fits you).
   - You can put any placeholder `${yourPlaceholder}` here and the formatter creates corresponding input for you.
   - The pattern (or anything else in the form) is not remembered - save it your own way. 
3. Enter your parameters of the pattern to subsequent inputs.
   - Do not change the pattern afterward, otherwise the parameters will disappear due to inputs refresh.
4. Copy the branch generated under the form and use it wherever you like.
   - If it is not generated automatically, try to click the Generate button.

## Requirements
**Required browser** (because usage of `replaceChildren()` API):
- Chrome/Edge 86+,
- Firefox 78+,
- Safari 14+.

## Possible future improvements (known issues):
- during pattern change the rest of the form is erased -> possibility to remember the values
- the pattern itself is not formatted for GIT -> possibility to enable and disable the formatting of individual items including the result?
- better styling of the page
- divide the code to more files (CSS, JS)
- remembering the pattern and other settings