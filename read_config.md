# Unrelated code snippet

import random

```py
def symbolTuple():
    tuple = (chr(random.randint(32,47)),chr(random.randint(58,64)),chr(random.randint(91,96)))
    return tuple

print(symbolTuple())
print(symbolTuple())
print(symbolTuple())
```

# Create a configurable password generator
In this guide, we will set some tasks for how to create a simple Python password generator.

## what you will build
A python script which can generate passwords which works by:

1. Read configuration information from a `.ini` file in the same folder as the script.
2. Print a password based on the configuration from the `.ini` file.

In order to achieve this, our program must do three things when we run it
a. read the configuration file
b. set the values from the configuration file
c. generate the password and print it

## Configuration Parameters
To control our program's behavior, our `config.ini` file will need the following parameters.

**includeLetters**: `True` or `False` : (Determines if letters should be used in the password)  
**includeNumbers** `True` or `False` :  (Determines if numbers should be used in the password)  
**includeSymbols** `True` or `False` :  (Determines if symbols should be used in the password)  
**length** `whole number` :  (Controls the length of the generated password)  

# Guided Steps
These steps show examples of how to do tasks *similar* to what is required for building our password generator. That is, the code and examples show techniques you can use to solve the problem for our password generator, but does not show you how to actually use those tools to create the password generator itself.


## Step 1: Create an `config.ini` file.
An INI file is a text file with key-value pairs. Here's an example:

```ini
my_value=1
other_value=some text
```
Create a config.ini file with the properties necessary to control your program's behavior.

## Step 2: Create a python script
In the same folder as the `config.ini` create a file named `generate.py`

## Step 3: Read the INI file in your script
In your Python file, use the `open()` function to read the `.ini` file. Here's an example of reading a file named `cake.txt` using `open()`

*cake.txt*
```txt
hello
world
```

*python script*
```py
file = open("cake.txt", "r")
for line in file.readlines():
  print(line)
```

## Step 4:  Add Variables to Hold the Configuration Values
Modify your python program so that it has declared a variable for each of the configuration values from our `config.ini`

In the following example, we read two properties about a house (colour and size) and print them to console:

*INI example*
```ini
house_color=red
house_size=75 m2
```

*Python Script*
```py
# To begin with, we set the value of our variables to None. These will be updated when we read our INI.
color = None
size = None
lines = open("house.ini", "r").readlines()
for line in lines:
  print(line)
```

Continue to the next task to see how to set the values of your variables, instead of just printing to the console.


## Step 5: Update the program to set the variable values instead of printing

To do this, we have to do two things:
1. split the key-value pair so that we can use only the value
2. use the key part to determine which variable to update using an if-statement.

For this task use the `split()` function on the string method. Assume the same INI-file from Step 4.

```py
color = None
size = None
lines = open("house.ini", "r").readlines()
for line in lines:
  # split the line on = so we get the key part and the value part
  key, value = line.split("=")
  if key == "house_color":
    color = value
  elif key == "size":
    size = value
```

We can now try to print our variables to check that their values have been set to the value in our `config.ini` file.

```py
# add this after the for-loop
print(color)
print(size)
```

Try changing the INI file and running the script again without changing the code to see how it behaves.
