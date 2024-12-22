- If Python is not available then [download it](https://www.python.org/downloads/windows/)
- Code is  intended 

## Virtualenv

Virtualenv allows to manage and keep dependencies for each projects separately think of like npm for Node.js projects 

```shell
pip install virtualenv
```

python3 -m venv .venv

source .venv/bin/activate

deactivate

pip freeze > requirements.txt

pip install -r requirements.txt

requirements.txt will list down all the dependencies that we've installed along with it's version

## REPL
- Read Evaluate Print Loop
- Whenever we exit it, it'll be flushed out.

## Null

- Null is `None` in python
- Use `is` operator to check for None

```py
example = None
if example is None:
	print("It's null")
```

- `==` operator is not preferred in Python
- why?
	- In py, everything has **id** `id(variable_name)` will return it's id
	- When we use `is` it does id comparission, for `==` it uses dictonary lookup and it's slow than is. 

```py
example = None
if example == None:
	print("It's null")
```

```py
example = None
print(id(example)) # 4315383752
print(id(None)) # 4315383752
```

## Mutable vs Immutable
- Array and dictonary are Mutable
- Strings, integers and tupuls are immutable

```py
emails = [] 
print(id(emails)) # 4396335680
emails.append("nesin@duck.com")
print(id(emails)) # 4396335680

name = "Ashik"
print(id(name)) # 4396353648
name = name + " " + "Nesin"
print(id(name)) # 4396216176
```

## Executing Python script

```shell
echo "print('It works!')" >> hello.py
cat hello.py
python hello.py
```

![[2024-02-05 at 08.50.23@2x.png]]

The `>>` operator redirects the output of the command to a file named `hello.py`. 

To make it executable add `#! /usr/bin/python3` at the top

```py
#! /usr/bin/env python
print('It works!')
```

Make it executable

```shell
chmod +x ./hello.py
```

```shell
./hello.py
```

`/usr/bin/env` We're telling `env` to figure out the path for python #nt-blog-idea

## Math Operations
- `+, -, *, %` are same in both python versions
- `/` works different
![[2024-02-05 at 09.00.50@2x.png]]

`.` at the end returns the actual value

![[2024-02-05 at 09.01.11@2x.png]]

## Naming in Python
- All in lowercase
- separated by underscore

## Formatting Strings
![[2024-02-05 at 09.07.20@2x.png]]
- In multiline string, the `\n` are preserved. So it'll print exactly like how we've written
- Escaping characters

```python
# backslash
single_quote = 'What\'s your name?'
double_quote = "What's your name?"
multiline = """What's your name?"""
```

- `\t` (tab character) can also be included
- `%s` is substitution character 

```python
name="Ashik"
email="nesin@duck.com"
print("My name is %s and my email is %s" % (name, email))
print("My name is {1} and my email is {0}".format(email, name))
```

## Manuplate and search string

### EndsWith
```python
"Hello World".endswith("World") #True
```

### Find the index
- Returns index if the substring is found
- returns `-1` if the substring is not found

```python
example = "Hello World!"
example.find("World") # 6
example.find("is") # -1
```

### format
```python
print("My name is {0} and my email is {1}".format(name, email))
```

### join
```python
"".join(["Hello ","World"])
```

### strip
Like trim() in javascript. It strips out whitespaces in beginning and the end

```python
"  Hello  ".strip()
```

### lstrip
Trims out the left side spaces

```python
"  Hello  ".lstrip()
```

### rstrip
Trims out the right side spaces

```python
"  Hello  ".rstrip()
```

## Find out the available methods

```python
dir("")
```

![[2024-02-06 at 07.47.30@2x.png]]

To know more

```python
help("".format_map)
```

## Flow Control

### if

```python
x = int(input("Enter any number:"))

if x < 0:
	x = 0
	print("Negative number changed to zero")
elif (x % 2 == 0):
	print("It's a even number")
else:
	print("It's a odd number")

```

### for loop

```python
websites = ["google.com", "youtube.com", "facebook.com"]
for website in websites:
    print(website)

for i in range(5):
    print(i)
for i in range(10, 15):
    print(i)
for i in range(0, 10, 2):
    print(i)
for i in range(10, 0, -1):
    print(i)
```

#### range
- `range(x)` upto the x (does not include x)
- `range(start,end)`
- `range(start, end, increment)`

## While condition
To keep running as long as the given condition is true

```python
x = 1
while x < 10:
    print(x)
    x += 1
```

#### Breaking the loop

```python
websites = ["google.com", "youtube.com", "facebook.com"]
for website in websites:
    if "youtube" in website:
        print("{0} is not allowed".format(website))
        break
    else:
        print("{0} is allowed".format(website))

```

cont from 11