# Art [De|En]Coder

A command line and web tool which converts shorthand into ASCII art and vice versa.

It takes a string as an input and converts it into a piece of text-based art, or alternatively converts a piece of ASCII art into handy shorthand. It supports multiple inputs (either literal or files) and outputting to stdout or a file. It also supports colored outputs.

## Installation

1. Clone the repository
    `git clone https://gitea.koodsisu.fi/mikapitkala/art/art.git [directory]`
2. Navigate to directory
3. You can either build the project (`art` and `web`) or run the `main.go` files that live in `/cmd/art` and `/cmd/web` respectively
3.1. To build the Command-Line version

```
cd cmd/art
go build -o art .
```

3.1.1. To run the CLI:

```
art "[5 #][5 -_]-[5 #]"
or
go run cmd/art/main.go "[5 #][5 -_]-[5 #]"
```

3.2. To build the Web version:

```
cd cmd/web
go build -o web .
```

3.2.1. To run the web version (from repo root)

```
web
or
go run cmd/web/main.go
```
3.2.2. Navigate to the displayed URL, usually `http://localhost:8080`

## Command Line Usage

The default mode is `decode` which expands shorthand into ASCII art. The most basic implementation (as specified in the assignment) would be

```
art "[5 #][5 -_]-[5 #]"
go run /cmd/art/main.go "[5 #][5 -_]-[5 #]"
```

Which expands the input argument into `#####-_-_-_-_-_#####`

## Web Usage

There are four sections: `How to use`, `Input`, `Output` and `Status`. `Output` is only visible if there is an output to display.

### How to use

Expand for documentation

### Input

#### Options
Toggle options and save them for later use

`Toggle Dark/Light mode` switch your mode

`Color` toggle color output for decode. Control blocks will be ignored, when off

`Relaxed` toggle relaxed mode for decode which leaves malformed blocks as is (default is *strict* - malformed blocks cause an **error**)

`Rainbow` add some wow to your outputs. Overrides color any other formatting

`Save Session` save your current session (options & input) into a cookie for later use. They will load automatically, when you start the server

`Clear options` wipe the cookie used to save options and inputs for a clean slate


#### Input
Enter (or Import) your text and hit decode to turn it into ASCII art or Encode to turn ASCII art into shorthand.

`Decode` decode input into ASCII art

`Encode` encode ASCII art into shorthand

`Import` Import a file **after** opening it with

`Reset` Reset input and output

`Browse` pick a `txt` file from your computer for processing. Files ending in `.encoded.txt` will get decoded automatically and files ending in `art.txt` will get encoded automatically.

### Output
Displays your art or shorthand in most of it's glory. You can hit the `Full Screen` button to enjoy it in its full glory in a new tab.

### Status
Displays your current HTTP status. You can expand to see any error messages and view source for some debugging information. You can also see the last saved session here, if there is one.


### Format
The shorthand is formatted as square brackets, which contain a `number` (number of repetitions) followed by a single space followed by a `pattern` (any pattern of symbols) which will get repeated `number` of times. With that in mind the `block` needs to:

1. Start with a valid number
2. Followed by a single space
3. Followed by a non-empty (space is fine) string
4. Have *balanced* square brackets around it

If any of the conditions is not met, the program will produce an error and stop, unless `-r` or `--relaxed` flag is set, in which case the malformed block will just be output *as is*.

Square brackets will not be rendered in the final product.

There are also **Control Block**s which are used to further prettify the art by adding colors and styling. Their format is `[0 color]` or `[-1 color]` for character color and inverted color, respectively, and they are enabled with the `-c` or `--color` flag. A **Control Block** will add the designated color to the following **block** or **literal character**. Possible colors are: 

Command line:
Red, Blue, Green, Yellow, Cyan, Magenta, White, Black, Gray and Rainbow

Web:
Any [HTML color names or values](https://www.w3schools.com/html/html_colors.asp)
`[0 #be93ff]`
`[0  magenta]`


### Command Line Flags and Options
The following flags are available:

`-d` or `--decode` Run in *decode mode*: Expand shorthand into art, **default mode**

`-e` or `--encode` Run in *encode mode*: Compress art into shorthand

`-r` or `--relaxed` Leave malformed blocks as is (default is *strict* - malformed blocks cause an **error**)

`-i` or `--input` *Input file*, or comma-separated *list of input file names*

`-o` or `--output` *Output file* (if not provided, output is printed to `stdout`)

`-c` or `--color` Enable *colored output*, if output file is enabled, it will ask if you want to save color information in it

`-m` or `--multi` Process multiple *inputs*, if unset only first input is processed

`--rainbow` Secret code!


Additionally, positional arguments may be provided. If an argument starts with `input=` or `output=` then the remainder is treated as a file name (and read or written, respectively) rather than a literal input.

#### Some caveats (Command Line)
`--input` and `--output` flags will treat the next argument as a file name, so they should be the last flags in any given command and followed by the `path/to/file`. If you need more flexibility, you can use the `"input="` and `"output="` prefixes in your arguments.

**Control blocks** `[0 color]` and `[-1 color]` control colors. Any other negative number will produce an **error**, or be left *as is* if `--relaxed` flag is set.

If both `--output` and `--color` are enabled, the program will check whether you want to include the color information in the output file. It'll look weird in an editor but print fine in terminal.

#### Some caveats (Web)

You need to **Pick** a file *before* you hit import. 

**Control blocks** `[0 color]` and `[-1 color]` control colors. Any other negative number will produce an **error**, or be left *as is* if `relaxed` option is set.

**Rainbow** overrides any other styling

### Command Line Usage examples
```art --decode "[5 #_]"```

Prints the decoded version of the input string `5 #_` --> `#_#_#_#_#_`

```art --decode --input "/path/to/input.txt"```

Prints the decoded version of `input.txt`

```art --decode --multi "[5 #_]" "[3 l:::l]" "[4 h:::h]"```

Decodes multiple literal inputs provided as separate positional arguments. -->
```
#_#_#_#_#_
l:::ll:::ll:::l
h:::hh:::hh:::hh:::h\n
```

```art --decode --multi --input "/path/to/file1.txt,/path/to/file2.txt"```

Decodes each file's content (each file is treated as a separate input) and prints them sequentially.

```art --decode --multi --input "/path/to/file1.txt" "input=/path/to/file2.txt\" "literal input"```

Decodes a mix of file inputs (using the input= prefix) and literal inputs.

```art --encode "HelloHelloHello\"```

Encodes the *input* into shorthand (e.g. `[3 Hello]`)

```art --encode --output "/path/to/out.txt\" "samplesamplesample\"```

Encodes the input and writes the output to the specified file.

```art --encode --multi --output "/path/to/out.txt" "TestTest\" "ExampleExampleExample\"```

Encodes multiple *inputs* and writes all outputs into a single *output file*.

```
cat examples/kood2.art.txt
cat examples/kood2.encoded.txt
art --decode --color --input "examples/kood2.encoded.txt
```

Example of the color control blocks.

### Project Structure

```
.
├── cmd
│   ├── art                 # Command-line version (CLI)
│   │   └── main.go
│   └── web                 # Web interface (web)
│       ├── main.go
├── examples                # Sample inputs/outputs (both)
├── internal                # Internal packages
│   ├── color               # Color processing utilities for (CLI)
│   │   └── color.go
│   ├── common              # Shared data structures and helper functions (web)
│   │   └── common.go
│   ├── decoder             # Decoding logic (both)
│   │   ├── decoder.go
│   │   ├── html_helpers.go
│   │   └── parser.go
│   ├── encoder             # Encoding logic (both)
│   │   └── encoder.go
│   ├── file                # File utilities (CLI)
│   │   └── (source files)
│   ├── handlers            # HTTP handlers (web)
│   │   ├── decode.go
│   │   ├── error.go
│   │   ├── form.go
│   │   ├── fullscreen.go
│   │   ├── handlers.go
│   │   └── options.go
│   └── utils               # Miscellaneous helpers (CLI)
│       ├── help.go
│       └── strippers.go
├── web                     # Web assets and templates
│   ├── static              
│   │   ├── fonts
│   │   ├── fullscreen.css
│   │   └── styles.css
│   └── templates           # HTML templates
│       ├── fullscreen.html
│       └── index.html
├── .gitignore
├── go.mod
└── README.md               # This file
```
