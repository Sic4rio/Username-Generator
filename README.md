
# Advanced Username Generator

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
nick brah
heathy ledger
mike hunt
mad max
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
nickbrah
nick.brah
nick_brah
nick-brah
nickb
nick.b
nick_b
nick-b
nbrah
n.brah
n_brah
n-brah
nickbrah123
nick.brah2024
nick_brah!
nick-brah@
...
```

## Script Details

The script reads the input file, processes each name to generate usernames based on predefined formats, and writes the usernames to an output file.

### Script Code

```python
import argparse
import itertools

def load_names(file_path):
    with open(file_path, 'r') as file:
        names = [line.strip().split() for line in file if line.strip()]
        return [{'firstname': parts[0], 'lastname': parts[1] if len(parts) > 1 else ''} for parts in names]

def generate_usernames(name_list):
    formats = [
        "{firstname}{lastname}", "{firstname}.{lastname}", "{firstname}_{lastname}", "{firstname}-{lastname}",
        "{firstname}{lastinitial}", "{firstname}.{lastinitial}", "{firstname}_{lastinitial}", "{firstname}-{lastinitial}",
        "{firstinitial}{lastname}", "{firstinitial}.{lastname}", "{firstinitial}_{lastname}", "{firstinitial}-{lastname}",
        "{firstinitial}{lastinitial}", "{firstinitial}.{lastinitial}", "{firstinitial}_{lastinitial}", "{firstinitial}-{lastinitial}",
        "{lastname}{firstname}", "{lastname}.{firstname}", "{lastname}_{firstname}", "{lastname}-{firstname}",
        "{lastinitial}{firstname}", "{lastinitial}.{firstname}", "{lastinitial}_{firstname}", "{lastinitial}-{firstname}",
        "{lastinitial}{firstinitial}", "{lastinitial}.{firstinitial}", "{lastinitial}_{firstinitial}", "{lastinitial}-{firstinitial}",
        "{firstname}{lastname}123", "{firstname}.{lastname}2024", "{firstname}_{lastname}!", "{firstname}-{lastname}@",
        "{firstname}{lastinitial}!", "{firstname}.{lastinitial}@!", "{firstname}_{lastinitial}2024", "{firstname}-{lastinitial}123",
        "{firstinitial}{lastname}!", "{firstinitial}.{lastname}@2024", "{firstinitial}_{lastname}123!", "{firstinitial}-{lastname}!",
        "{firstinitial}{lastinitial}2024", "{firstinitial}.{lastinitial}@123", "{firstinitial}_{lastinitial}!", "{firstinitial}-{lastinitial}@",
        "{lastname}{firstname}123", "{lastname}.{firstname}2024", "{lastname}_{firstname}!", "{lastname}-{firstname}@",
        "{lastinitial}{firstname}!", "{lastinitial}.{firstname}@2024", "{lastinitial}_{firstname}123", "{lastinitial}-{firstname}!",
        "{lastinitial}{firstinitial}2024", "{lastinitial}.{firstinitial}@123", "{lastinitial}_{firstinitial}!", "{lastinitial}-{firstinitial}@"
    ]
    
    usernames = set()
    for name in name_list:
        firstinitial = name['firstname'][0] if name['firstname'] else ''
        lastinitial = name['lastname'][0] if name['lastname'] else ''
        for fmt in formats:
            username = fmt.format(
                firstname=name['firstname'],
                lastname=name['lastname'],
                firstinitial=firstinitial,
                lastinitial=lastinitial
            )
            usernames.add(username)
    return list(usernames)

def main():
    parser = argparse.ArgumentParser(description="Advanced Username Generator")
    parser.add_argument('-i', '--input-file', type=str, required=True, help='Input list of names (plain text)')
    parser.add_argument('-o', '--output-file', type=str, default='output-usernames.txt', help='Output file for usernames')

    args = parser.parse_args()

    name_list = load_names(args.input_file)

    usernames = generate_usernames(name_list)
    
    with open(args.output_file, 'w') as output_file:
        for username in usernames:
            output_file.write(f"{username}
")
    
    print(f"Generated {len(usernames)} usernames and saved to {args.output_file}")

if __name__ == "__main__":
    main()
```

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
