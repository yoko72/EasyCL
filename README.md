# clappy

Command Line Argument Parser for pythonic code.


Simple example with clappy:

    import clappy as cl

    foo = cl.parse("--foo")
    bar = cl.parse("--bar", is_flag=True)

Equivalent script without clappy:

    from argparse import ArgumentParser

    parser = ArgumentParser()
    parser.add_argument("--foo")
    parser.add_argument("--bar", action="store_true")
    args = parser.parse_args()
    foo = args.foo
    bar = args.bar
    

Script with clappy is more readable and writable.

Clappy will be big help especially when you use subcommands.

Subcommand with clappy:

    import clappy as cl

    if cl.subcommand("foo").invoked:
        opt = cl.parse("--foo_opt")
    elif cl.subcommand("bar").invoked:
        opt = cl.parse("--bar_opt")

Equivalent script without clappy:

    import argparse

    parser = argparse.ArgumentParser()
    subparsers = parser.add_subparsers()
    subparser1 = subparsers.add_parser("foo")
    subparser1.add_argument("--foo_opt")
    subparser2 = subparsers.add_parser("bar")
    subparser2.add_argument("--bar_opt")
    args = parser.parse_known_args()
    try:
        opt = args.foo_opt
    except AttributeError:
        try:
            opt = args.bar_opt
        except AttributeError:
            pass

Clappy becomes really helpful when you have multiple modules requiring command line arguments.
Without clappy you must manage same parser and the result of parse across multiple modules.

Clappy frees you from such tiresome process by independent parsing.


## Install

`pip install clappy`

## How to use

clappy is a wrapper of argparse. You can give arguments for clappy as if you use argparse. [Reference of argparse is here.](https://docs.python.org/ja/3/howto/argparse.html)

Just call clappy.parse(*args, **kwargs) as if argparse.ArgumentParser().add_argument(*args, **kwargs). 
Same args are available for clappy.parse. Additionally, clappy accepts one keyword argument, "is_flag".
It's just an alias of action="store_true". If you set "is_flag" True, you don't need to give argument after the option.

e.g.  clappy.parse("--verbose", is_flag=True)

👍 --verbose 

👎 --verbose True


### Auto help generation

If you want to generate help automatically, call clappy.create_help(). 
It must be done after all arguments got parsed.

### Construct parser with args

Initialize parser with clappy.initialize_parser(*args, **kwargs).
These args are also common with argparse.ArgumentParser(*args, **kwargs).

### Parse with args

Runs clappy.set_args_on_parse(*args, **kwargs).
Same args with ArgumentParser().parse_args(*args, **kwargs)



