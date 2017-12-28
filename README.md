# Ruby-Quick-Reference-Guide
Ruby through code samples

## Table of Contents
* [Hello World](#hello-world)
* [Keywords](#keywords)
* [Comments](#comments)
* [Variables](#variables)
* [Constants](#constants)
* [Integer Numbers](#integer-numbers)
* [Floating Numbers](#floating-numbers)
* Strings (TODO)
* [Backslash Notations](#backslash-notations)
* %Literals (TODO)
* HERE Docs (TODO)
* [Arrays](#arrays)
* Hash (TODO)
* Ranges (TODO)
* Symbols (TODO)
* [Class](#class)
* Operators (TODO)
* Conditional Structures (TODO)
* Loops (TODO)
* Methods (TODO)
* Blocks (TODO)
* Modules (TODO)
* Exceptions (TODO)
* I/O (TODO)

### Hello World
```ruby
puts 'Hello World!'
```
[back to top](#table-of-contents)

### Keywords
```ruby
__ENCODING__  # The script encoding of the current file
__END__       # Marks the end of the Ruby program; DATA can follow  
__FILE__      # The path to the current file
__LINE__      # The line number of this keyword in the current file

BEGIN         # Runs before any other code in the current file
END           # Runs after any other code in the current file
DATA          # An IO stream to read data embedded in the program following __END__

def           # Defines a method
defined?      # Returns a string describing its argument
do            # Starts a block
alias         # Creates an alias between two methods (and other things)
and           # Short-circuit Boolean and with lower precedence than &&
begin         # Starts an exception handling block
break         # Leaves a block early
case          # Starts a case expression
class         # Creates or opens a class
def           # Defines a method
defined?      # Returns a string describing its argument
do            # Starts a block
else          # The unhandled condition in case, if and unless expressions
elsif         # An alternate condition for an if expression
end           # The end of a syntax block.
ensure        # Starts a section of code that is always run when an exception is raised
false         # Boolean false
for           # A loop that is similar to using the each method
if            # Used for if and modifier if expressions
in            # Used to separate the iterable object and iterator variable in a for loop
module        # Creates or opens a module
next          # Skips the rest of the block
nil           # A false value usually indicating “no value” or “unknown”
not           # Inverts the following boolean expression. Has a lower precedence than !
or            # Boolean or with lower precedence than ||
redo          # Restarts execution in the current block
rescue        # Starts an exception section of code in a begin block
retry         # Retries an exception block
return        # Exits a method
self          # The object the current method is attached to
send          # Invoke a method
__send__      # Alternative for the above, in case of name clashes
super         # Calls the current method in a superclass
then          # Indicates the end of conditional blocks in control structures
true          # Boolean true
undef         # Prevents a class or module from responding to a method call
unless        # Used for unless and modifier unless expressions
until         # Creates a loop that executes until the condition is true
when          # A condition in a case expression
while         # Creates a loop that executes while the condition is true
yield         # Starts execution of the block sent to the current method
```
[back to top](#table-of-contents)

### Comments
```ruby
#This is a single line comment

=begin
This is a multiline comment
This is a multiline comment
=end
```
[back to top](#table-of-contents)

### Variables
```ruby
_age = 21     # local variable
1age = 21     # INVALID variable name
age = 21      # local variable
@age = 21     # instance variable
@@age = 21    # class variable
$age = 21     # global variable
```
[back to top](#table-of-contents)

### Constants
```ruby
AGE = 21      # constant; by convention - constants can be modified and generate a warning
```
[back to top](#table-of-contents)

### Integer Numbers
```ruby
1234                 # Fixnum decimal
-1234                # Negative Fixnum
1_234                # Fixnum decimal (with underscore to improve readability)
0b1011               # binary
0xff                 # hexadecimal
0377                 # octal
12345678901234567890 # Bignum
```
[back to top](#table-of-contents)

### Backslash notations 
```ruby
# work in "" -- interpolated -- strings
puts "ln1\nln2"     # Newline (0x0a); prints two lines
puts "n123\rab"     # Carriage return (0x0d); prints one line, overlaid
puts "f12\f345"     # Formfeed (0x0c); prints two lines, offset
puts "abc\bx"       # Backspace (0x08); prints 'abx'
puts "bell\a\a\a"   # Bell (0x07); prints 'bell' and rings bell three times
puts "ab\ecd"       # Escape (0x1b); prints 'abd'
puts "ab\scd"       # Space (0x20); prints 'ab cd'
puts "ab\xcd"       # Character x; prints 'abxcd'
puts "ab\015x"      # Octal (n = 0-7); prints 'xb', same as \r
puts "ab\xdx"       # Hesadecimal (n = 0-9, a-f, A-F); prints 'xb', same as \r
puts "abc\C-Hxyz"   # Control-x; prints 'abxyz', same as \b; \C-@ == \x00, \C-A == \x01, ...  [see complete list here](https://www.cisco.com/c/en/us/td/docs/ios/12_2/configfun/command/reference/ffun_r/frf019.pdf)
puts "abc\C-Hxyz"   # Control-x; prints 'abxyz', same as \b; \C-@ == \x00, \C-A == \x01, ...  
[see complete list here](https://www.cisco.com/c/en/us/td/docs/ios/12_2/configfun/command/reference/ffun_r/frf019.pdf)
"\M-x"               # Meta x; usually used for keyboard/terminal control
"\M-\C-x"            # Meta-Control-x; usually used for keyboard/terminal control
puts "\u2713"        # Unicode code point U+nnnn (Ruby 1.9+); prints "✓"

```
[back to top](#table-of-contents)

### HERE Docs
```ruby
str1 = <<EODOC
This is some data to 
go into
the str1 variable
EODOC
puts str1       # Exact text, with carriage returns, in str1

str2 = <<-INDENTED
  More dumnmy text, indented.
  Leading spaces are included in the output
  #{str1} - yes, interpolation is supported
  INDENTED
puts str2       # Exact text including indent spaces; HERE marker can be indented

str3 = <<"***"
You can use special characters,
enclosed in quqotes.
***
puts str3       # Exact text

str4 = <<~SQUIGGLY_DOC
  The tilde '~" modifies the indentation
  of the text. The leading spaces of the
  least-indented line are removed from all lines.
    This line will be indented two spaces.
SQUIGGLY_DOC
puts str4       # Modified indentation, as noted in the text

str5 = <<'NO_INTERPOLATION'
Enclosing the HEREDOC identifier in
sinqle quotes means no interpolation,
so #{str4} is printed character-for-character.
puts str5       # HEREDOC with no interpolation

str6 <<`BACKTICKS`
cat #{__FILE__}
BACKTICKS
puts str6       # Prints the results of the cat command
```

### Floating Numbers
```ruby
123.4                # floating point value
4.0e2                # 400.0 - scientific notation
4E2                  # 400.0 - dot not required
4e+2                 # 400.0 - sign before exponential
```
[back to top](#table-of-contents)


### Arrays
```ruby
array = []                  # Array; zero-based indexing
array = Array.new(5)        # Array with size 
array = Array.new(2, "abc") # ["abc", "abc"]
array = Array(0..9)         # [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
# Using string literals
num = 5
array = %w{a b c #{num}}    # ["a", "b", "c", "\#{num}"]
array = %W{a b c #{num}}    # ["a", "b", "c", "5"]

first_item = array.first    # Array first item
first_item = array[0]       # Array first item
last_item = array.last      # Array last item
last_item = array[array.size - 1]   # Array last_item
array.size                  # Array size
array.length                # Array size
array.count                 # Array size
array.at(5)                 # Element at index 5
array.push(42)              # Add 42 to end of array
array.pop                   # Remove last element from array
array.shift                 # Remove first element from array
array.unshift(15)           # Add 15 to beginning of array
array.methods.sort - Object.methods   # List all Array instance methods
```
[back to top](#table-of-contents)

### Class
```ruby
class Customer
end
```
[back to top](#table-of-contents)
