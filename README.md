**Here's a clean and useful utility in English** — **Strong Password Generator**

```python
#!/usr/bin/env python3
"""
Simple Password Generator - A handy CLI utility
"""

import argparse
import random
import string
import sys


def generate_password(length=16, use_upper=True, use_digits=True, use_special=True):
    """Generate a strong random password"""
    
    # Base characters
    characters = string.ascii_lowercase
    
    if use_upper:
        characters += string.ascii_uppercase
    if use_digits:
        characters += string.digits
    if use_special:
        characters += "!@#$%^&*()_+-=[]{}|;:,.<>/?"
    
    # Ensure at least one character from each selected category
    password = []
    if use_upper:
        password.append(random.choice(string.ascii_uppercase))
    if use_digits:
        password.append(random.choice(string.digits))
    if use_special:
        password.append(random.choice("!@#$%^&*()_+-"))
    
    # Fill the rest of the password
    while len(password) < length:
        password.append(random.choice(characters))
    
    random.shuffle(password)
    return ''.join(password)


def main():
    parser = argparse.ArgumentParser(
        description="🔐 Strong Password Generator",
        formatter_class=argparse.RawDescriptionHelpFormatter
    )
    parser.add_argument("-l", "--length", type=int, default=16,
                        help="Password length (default: 16)")
    parser.add_argument("-n", "--no-upper", action="store_true",
                        help="Do not include uppercase letters")
    parser.add_argument("-d", "--no-digits", action="store_true",
                        help="Do not include digits")
    parser.add_argument("-s", "--no-special", action="store_true",
                        help="Do not include special characters")
    parser.add_argument("-c", "--count", type=int, default=1,
                        help="Number of passwords to generate")
    
    args = parser.parse_args()
    
    for _ in range(args.count):
        pwd = generate_password(
            length=args.length,
            use_upper=not args.no_upper,
            use_digits=not args.no_digits,
            use_special=not args.no_special
        )
        print(pwd)


if __name__ == "__main__":
    try:
        main()
    except KeyboardInterrupt:
        print("\nGoodbye!", file=sys.stderr)
```

### How to use:

1. Save as `passgen.py`
2. Make it executable (optional): `chmod +x passgen.py`
3. Run:

```bash
python3 passgen.py                    # 16 character password
python3 passgen.py -l 24              # 24 character password
python3 passgen.py -c 5               # Generate 5 passwords
python3 passgen.py --no-special       # No special characters
python3 passgen.py -l 20 -c 3         # 3 passwords, 20 chars each
```
