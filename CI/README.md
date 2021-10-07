# PHP Style Guide

The following page describes the coding styles adhered to when contributing to the development of CodeIgniter. There is no requirement to use these styles in your own CodeIgniter application, though they are recommended.

Table of Contents
[PHP Style Guide](#php-style-guide)

1. [File Format](#file-format)

   - [TextMate](#text-mate)
   - [BBEdit](#bbedit)

1. [PHP Closing Tag](#php-closing-tag)
1. [File Naming](#file-naming)
1. [Class and Naming Method](#class-and-method-naming)
1. [Variable Names](#variable-names)
1. [Comennting](#commenting)
1. [Constants](#constants)
1. [TRUE, FALSE, and NULL](#true-false-and-null)
1. [Logical Operators](#logical-operators)
1. [Comparing Return Values and TypeCasting](#comparing-return-values-and-typecasting)
1. [Debugging Code](#debugging-code)
1. [Whitespace in Files](#whitespaces-in-files)
1. [Compatibility](#compatibility)
1. [One File Per Class](#one-file-per-class)
1. [WhiteSpace](#whitespace)
1. [Line Breaks](#line-breaks)
1. [Code Indenting](#code-indenting)
1. [Bracket and Prenthetic Spacing](#bracket-and-parenthetic-spacing)
1. [Localized Text](#localized-text)
1. [Private Methosds and Variables](#private-methods-and-variables)
1. [PHP Errors](#php-errors)
1. [Short Open Tags](#short-open-tags)
1. [One Statement Per Line](#one-statement-per-line)
1. [Strings](#strings)
1. [SQL Queries](#sql-queries)
1. [Default Function Arguments](#default-function-arguments)

# File Format

Files should be saved with Unicode (UTF-8) encoding. The BOM should not be used. Unlike UTF-16 and UTF-32, there’s no byte order to indicate in a UTF-8 encoded file, and the BOM can have a negative side effect in PHP of sending output, preventing the application from being able to set its own headers. Unix line endings should be used (LF).

Here is how to apply these settings in some of the more common text editors. Instructions for your text editor may vary; check your text editor’s documentation.

## Text Mate

1.  Open the Application Preferences
1.  Click Advanced, and then the “Saving” tab
1.  In “File Encoding”, select “UTF-8 (recommended)”
1.  In “Line Endings”, select “LF (recommended)”
1.  Optional: Check “Use for existing files as well” if you wish to modify the line endings of files you open to your new preference.

## BBEdit

1.  Open the Application Preferences
1.  Select “Text Encodings” on the left.
1.  In “Default text encoding for new documents”, select “Unicode (UTF-8, no BOM)”
1.  Optional: In “If file’s encoding can’t be guessed, use”, select “Unicode (UTF-8, no BOM)”
1.  Select “Text Files” on the left.
1.  In “Default line breaks”, select “Mac OS X and Unix (LF)”

# PHP Closing Tag

The PHP closing tag on a PHP document ?> is optional to the PHP parser. However, if used, any whitespace following the closing tag, whether introduced by the developer, user, or an FTP application, can cause unwanted output, PHP errors, or if the latter are suppressed, blank pages. For this reason, all PHP files MUST OMIT the PHP closing tag and end with a single empty line instead.

# File Naming

Class files must be named in a Ucfirst-like manner, while any other file name (configurations, views, generic scripts, etc.) should be in all lowercase.

```php
// bad
somelibrary.php
someLibrary.php
SOMELIBRARY.php
Some_Library.php

Application_config.php
Application_Config.php
applicationConfig.php

// good
Somelibrary.php
Some_library.php

applicationconfig.php
application_config.php
```

Furthermore, class file names should match the name of the class itself. For example, if you have a class named Myclass, then its filename must be Myclass.php.

(#class-and-method-naming) **Class and Method Naming**

Class names should always start with an uppercase letter. Multiple words should be separated with an underscore, and not CamelCased.

```php
// bad
class superclass
class SuperClass

// good
class Super_class

class Super_class {

      public function __construct()
      {

      }
}
```

Class methods should be entirely lowercased and named to clearly indicate their function, preferably including a verb. Try to avoid overly long and verbose names. Multiple words should be separated with an underscore.

```php
//bad
function fileproperties()                               // not descriptive and needs underscore separator
function fileProperties()                               // not descriptive and uses CamelCase
function getfileproperties()                            // Better!  But still missing underscore separator
function getFileProperties()                            // uses CamelCase
function get_the_file_properties_from_the_file()        // wordy

//good
function get_file_properties()  // descriptive, underscore separator, and all lowercase letters
```

(#variable-names) **Variale Names**

The guidelines for variable naming are very similar to those used for class methods. Variables should contain only lowercase letters, use underscore separators, and be reasonably named to indicate their purpose and contents. Very short, non-word variables should only be used as iterators in for() loops.

```php
//bad
$j = 'foo';             // single letter variables should only be used in for() loops
$Str                    // contains uppercase letters
$bufferedText           // uses CamelCasing, and could be shortened without losing semantic meaning
$groupid                // multiple words, needs underscore separator
$name_of_last_city_used // too long

//good
for ($j = 0; $j < 10; $j++)
$str
$buffer
$group_id
$last_city
```

(#commenting) **Commenting**

In general, code should be commented prolifically. It not only helps describe the flow and intent of the code for less experienced programmers, but can prove invaluable when returning to your own code months down the line. There is not a required format for comments, but the following are recommended.

<a href="https://manual.phpdoc.org/HTMLSmartyConverter/HandS/phpDocumentor/tutorial_phpDocumentor.howto.pkg.html#basics.docblock">DocBlock</a> style comments preceding class, method, and property declarations so they can be picked up by IDEs:

```php
/**
 * Super Class
 *
 * @package     Package Name
 * @subpackage  Subpackage
 * @category    Category
 * @author      Author Name
 * @link        http://example.com
 */
class Super_class {
```

```php
/**
 * Encodes string for use in XML
 *
 * @param       string  $str    Input string
 * @return      string
 */
function xml_encode($str)
```

```php
/**
 * Data for class manipulation
 *
 * @var array
 */
public $data = array();
```

Use single line comments within code, leaving a blank line between large comment blocks and code.

```php
// break up the string by newlines
$parts = explode("\n", $str);

// A longer comment that needs to give greater detail on what is
// occurring and why can use multiple single-line comments.  Try to
// keep the width reasonable, around 70 characters is the easiest to
// read.  Don't hesitate to link to permanent external resources
// that may provide greater detail:
//
// http://example.com/information_about_something/in_particular/

$parts = $this->foo($parts);
```

(#constant) **Constants**

Constants follow the same guidelines as do variables, except constants should always be fully uppercase. Always use CodeIgniter constants when appropriate, i.e. SLASH, LD, RD, PATH_CACHE, etc.

```php
//bad
myConstant      // missing underscore separator and not fully uppercase
N               // no single-letter constants
S_C_VER         // not descriptive
$str = str_replace('{foo}', 'bar', $str);       // should use LD and RD constants

//good
MY_CONSTANT
NEWLINE
SUPER_CLASS_VERSION
$str = str_replace(LD.'foo'.RD, 'bar', $str);
```

(true-false-and-null) **TRUE, FALSE, and NULL**

TRUE, FALSE, and NULL keywords should always be fully uppercase.

```php
//bad
if ($foo == true)
$bar = false;
function foo($bar = null)

//good
if ($foo == TRUE)
$bar = FALSE;
function foo($bar = NULL)
```

(#logical-operators) **Logical Operators**
Use of the `||`“or” comparison operator is discouraged, as its clarity on some output devices is low (looking like the number 11, for instance).`&&` is preferred over `AND` but either are acceptable, and a space should always precede and follow !.

```php
//bad
if ($foo || $bar)
if ($foo AND $bar)  // okay but not recommended for common syntax highlighting applications
if (!$foo)
if (! is_array($foo))

//good
if ($foo OR $bar)
if ($foo && $bar) // recommended
if ( ! $foo)
if ( ! is_array($foo))
```

(#comparing-return-values-and-typecasting) **Comparing Return Values and Typecasting**

Some PHP functions return `FALSE` on failure, but may also have a valid return value of `“”` or `0`, which would evaluate to `FALSE` in loose comparisons. Be explicit by comparing the variable type when using these return values in conditionals to ensure the return value is indeed what you expect, and not a value that has an equivalent loose-type evaluation.

Use the same stringency in returning and checking your own variables. Use `===` and `!==` as necessary.

```php
// If 'foo' is at the beginning of the string, strpos will return a 0,
// resulting in this conditional evaluating as TRUE

//bad
if (strpos($str, 'foo') == FALSE)

//good
if (strpos($str, 'foo') === FALSE)
```

```php
//bad
function build_string($str = "")
{
        if ($str == "") // uh-oh!  What if FALSE or the integer 0 is passed as an argument?
        {

        }
}

//good
function build_string($str = "")
{
        if ($str === "")
        {

        }
}
```

See also information regarding `typecasting`, which can be quite useful. Typecasting has a slightly different effect which may be desirable. When casting a variable as a string, for instance, `NULL` and boolean `FALSE` variables become empty strings, 0 (and other numbers) become strings of digits, and boolean TRUE becomes “1”:

```php
$str = (string) $str; // cast $str as a string
```
