# OOP Calculator

This calculator supports addition, subtraction, viewing history, removing an entry, help, and exit. History is saved only during the current session.

## Setup

Use Python 3.11 or newer. From the project folder, run:

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
```

## Run

```bash
python -m calculator
```

Enter `add` or `subtract`, then enter the two numbers. Use `history` to view calculations and `remove` to delete an entry by its displayed number. Use `help` for instructions and `exit` to quit.

Invalid numbers and removal requests display an error without crashing the calculator.

## Test

```bash
python -m pytest
```

The test configuration requires 100% line and branch coverage. GitHub Actions runs the tests on Python 3.11, 3.12, 3.13, and 3.14.

## Design

`Calculation` stores the operands and defines the shared `get_result()` method. `Add` and `Subtract` inherit from it and perform their own arithmetic. The same method can be called on either kind of object.

`History` manages the calculation collection. It returns a copy of its list so outside code cannot clear the original list. The command-line interface handles user input and displays results separately from the arithmetic.

## Reflection

### Adding multiplication

I would add a `Multiply` class in `calculation.py` that inherits from `Calculation` and implements `get_result()`. I would also register the `multiply` command in `cli.py`, update the help message, and add tests for multiplication and its command. `History` would not need multiplication logic because it stores calculation objects rather than performing their arithmetic.

### Email and text notifications

Email and text-message classes could share a `send()` method. Each class would implement it differently: one would send an email and the other would send a text. The calling code could use the same method without needing to handle each delivery process itself.

### Using these ideas in another language

I could reuse the ideas of classes, inheritance, shared interfaces, and giving each part of a program a clear responsibility. I would still need to learn the new language's syntax, type rules, exception handling, and how it creates and manages objects.

### Investigating missing coverage

If the tests passed but coverage failed, I would check the report for missing lines and branches. I would identify the behavior those paths represent and add tests that check it, such as an invalid removal or an interrupted input.