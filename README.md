
# Username Generator

This script generates usernames based on a list of given names. It can produce a wide variety of username formats using first names, last names, initials, and special characters.

## Features

- Generates usernames from first and last names.
- Supports various formats and combinations.
- Adds special characters and numbers to usernames.
- Writes the generated usernames to an output file.

## Usage

### Input File

The input file should be a plain text file containing names, with each name on a new line. Names can be either a single name or a pair of first and last names separated by a space.

**Example `usernames.txt`:**
```
tiny kox
dick swetts
mike hunt 
john bohner
```

### Running the Script

To run the script, use the following command:
```sh
python users.py -i usernames.txt -o output-usernames.txt
```

### Arguments

- `-i`, `--input-file`: Specifies the input file containing the names (required).
- `-o`, `--output-file`: Specifies the output file for the generated usernames (default: `output-usernames.txt`).

## Example

```sh
python users.py -i usernames.txt -o output-usernames.txt
```

This will generate usernames from `usernames.txt` and save them to `output-usernames.txt`.

## Sample Output

The output file `output-usernames.txt` will contain entries like:
```
m_h!
mh
j-b
d_swetts123!
bohnerjohn
s-dick
k.t
dick.swetts
hunt-mike
b.john
mike_h
mike.h
john.b
swetts-dick
m.hunt@2024
k-tiny
john.bohner
mikeh
mike-h123
k.tiny
koxtiny
tk2024
k-t
s-d@
m-h@

...
```

## Script Details

The script reads the input file, processes each name to generate usernames based on predefined formats, and writes the usernames to an output file.


## License

This project is licensed under my Dog, all rights go to him.
