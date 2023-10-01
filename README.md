Aga is a lightweight native Python library for quickly creating documented command-line interfaces using `argparse`. It is designed to be as simple as possible to use.

## Usage
Using Aga couldn't be easier. Assume the file below is named _test.py_: 

```
from aga import *


@aga.add_arg
def add(x: int, y: int = 2) -> int:
    """ A simple function to add two numbers

    Args:
        x: The first number to add
        y: The second number to add

    Returns:
        x added to y
    """

    return x + y


if __name__ == '__main__':
    aga.bake()
    print(aga.args.x, aga.args.y)

```

This simple file will result in the `x` and `y` arguments as shown below in the output of `python test.py -h`.

```
❯ python test.py -h    
usage: test.py [-h] y x

positional arguments:
  y           The second number to add
  x           The first number to add

options:
  -h, --help  show this help message and exit
```

As you can see, one must simply add the decorator `aga.add_arg` to a function and Aga will parse the function definition and create a documented command-line interface. 

Aga will search for PEP484 type annotations, default values and Google-style docstrings to add further information to the argument definition. None of these are necessary however, and if one (or all) are missing it will simply be ignored.