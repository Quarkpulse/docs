# Begin hier

## Andere heading

Wat voorbeeld tekst!

## Code annotatie voorbeelden
### Codeblokken
Wat `code` komt hier.

### Simpele codeblokken
Een simpele codeblok:
```
def print_fibonacci(n):
    a, b = 0, 1
    while a < n:
        print(a, end=' ')
        a, b = b, a+b
    print()

print_fibonacci(100)
```
This code will print all Fibonacci numbers less than 100. You can replace 100 with any number you want to limit the Fibonacci series. The print_fibonacci function calculates the Fibonacci series up to the given limit n. It starts with 0 and 1 (the first two numbers in the Fibonacci series) and then keeps adding the last two numbers to generate the next number in the series. It continues this until it reaches or exceeds the limit n. The print() function is used to print the numbers on the same line with a space in between, and the end=' ' parameter ensures that a space is printed instead of a newline after each number. The final print() without any arguments is used to print a newline after the entire series is printed. This ensures that anything you print afterwards will start on a new line.

### Code voor specifieke talen

Wat meer code met the `py` aan het begin:

``` py
import tensorflow as tf
def whatever()
```

### Code met een titel

``` py title="bubble_sort.py"
def bubble_sort(items):
    for i in range(len(items)):
        for j in range(len(items) - 1 - i):
            if items[j] > items[j + 1]:
                items[j], items[j + 1] = items[j + 1], items[j]
```

### Code met een lijnummers

``` py linenums="1"
def bubble_sort(items):
    for i in range(len(items)):
        for j in range(len(items) - 1 - i):
            if items[j] > items[j + 1]:
                items[j], items[j + 1] = items[j + 1], items[j]
```

### Code met een highlight lijnen

``` py hl_lines="2 3"
def bubble_sort(items):
    for i in range(len(items)):
        for j in range(len(items) - 1 - i):
            if items[j] > items[j + 1]:
                items[j], items[j + 1] = items[j + 1], items[j]
```

## Iconen en Emojis
:smile:
:fontawesome-regular-face-laugh-wink:
:fontawesome-brands-twitter:{ .twitter }
:octicons-heart-fill-24:{ .heart }