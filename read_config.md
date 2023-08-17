# Create a configurable password manager
We will create a simple python password manager which has the following behavior

1. It reads some configuration information from a `.ini` file that exists in the same folder as the script
2. It prints out a password based off the configuration from the `.ini`

These are the parameters which will be controlled by the `config.ini`

**includeLetters** `True | False`  
determines whether the password generator should use letters in the generated password

**includeNumbers** `True | False`  
determines whether the password generator should use numbers in the generated password

**includeSymbols** `True | False`  
determines whether the password generator should use symbols in the generated password

**length** `Regular Number`  
A number which will control the length of the generated password

## Program flow

In order to achieve this, our program must do three things when we run it
1. read the configuration file
2. set the values from the configuration file
3. generate the password and print it

# Tasks

## Create an `config.ini` file.
A ini file is just a text file which follows a certain structure. Our ini file does not need any sections so we will only use the key-value properties syntax.

Here is an example of a ini file

```ini
my_value=1
other_value=some text
```

Write an ini file which has the properties necessary to control the behavior of your program

## create a python script
In the same folder as the `config.ini` create a file named `generate.py`

## Read the ini file into python
In your python file, use the `open()` function to read the `.ini` file.

Here is an example of how you would make python read out a file named `cake.txt` line-by-line


*cake.txt*
```txt
hello
world
```

*cake-read.py*
```py
file = open("cake.txt", "r")
for line in file.readlines():
  print(line)
```

## add variables to your python program to hold the values of the config
Modify your python program so that it has a variable for each of the configuration values from our `config.ini`

Use placeholder values for your variables for now. Here is an example of a python program that reads information about a house from a ini file.

*house.ini*
```ini
house_color=red
house_size=75 m2
```

*house-color.py*
```py
# it is okay not to set the values initially. We are just creating the variables in anticipation of using them.
color = ""
size = ""
lines = open("house.ini", "r").readlines()
for line in lines:
  print(line)
```

## Update the program so that the for loop sets the values
We need to not print the lines from the `.ini` but use them to update our variables.

To do this, we have to do two things:
1. split the key-value pair so that we can use only the value
2. use the key part to determine which variable to update using an if-statement.

For this task use the `split` function on the string method.

```py
color = ""
size = ""
lines = open("house.ini", "r").readlines()
for line in lines:
  # split the line on = so we get the key part and the value part
  key, value = line.split("=")
  if key == "house_color":
    color = value
  if key == "size":
    size = value
```

