# ICS3U Grade 11 Computer Science Study Guide
### Exam Focus: Paper Exam (MCQs, Code Tracing, & Short Code Segments)

This study guide has been expanded and relocated to the repository root for hosting on **GitHub Pages** (as `index.html` and `README.md`).

---

## 1. STRATEGIES FOR PAPER EXAMS
On a paper exam, you do not have autocomplete, a compiler, or error highlighting. Keep these practices in mind:
*   **Write Clean Syntax**: Pay attention to colons `:` at the end of functions, loops, and conditionals, and indent code blocks properly.
*   **Trace Variables Step-by-Step**: Trace code values on the page margin using a small grid or list.
*   **Gotchas and Tricks**: Watch out for immutable values (like strings) and return states (like `list.sort()`).
*   **Memorize Callback Signatures**: Pay attention to callback parameters. The Scale slider and OptionMenu dropdown pass arguments into their command functions. Buttons and Spinboxes do not.
*   **Draw Layout Grids**: Sketch layout positions as table grids. This makes positioning logic easier to trace.

---

## 2. PYTHON PART 1 (py1) CHEAT SHEET

### Variable Types
*   `int`: Integers/Whole numbers (`15`, `-3`)
*   `float`: Decimal fractions (`19.95`, `0.0`)
*   `str`: String text inside quotes (`"Aaron"`)
*   `bool`: Logical values (`True` or `False` - capitalize the first letter!)

### Arithmetic Operators
*   `**` Exponentiation: `5 ** 2` results in `25`
*   `/` Float Division: `5 / 2` results in `2.5`
*   `//` Integer/Floor Division: `5 // 2` results in `2` (removes decimal, rounds down)
*   `%` Modulo (Remainder): `5 % 2` results in `1`

### Formatting Output (f-strings)
*   **2 Decimal Places**: `f"${price:.2f}"` (turns `10.5` into `$10.50`)
*   **Center Text**: `f"{word:^30}"` (centers the string within a 30-character gap)
*   **Right Align**: `f"{word:>20}"`
*   **Left Align**: `f"{word:<20}"`

### Standard Libraries
*   **Math Module (`import math`)**:
    *   `math.pi`: $\approx 3.14159$
    *   `math.sqrt(x)`: returns decimal square root of `x`
*   **Random Module (`import random`)**:
    *   `random.randint(a, b)`: inclusive of both limits (e.g. `randint(1, 3)` returns `1`, `2`, or `3`).
    *   `random.randrange(start, stop, step)`: exclusive of the stop value (e.g. `randrange(100, 1001, 100)` returns 100, 200, ..., 1000).
    *   `random.uniform(a, b)`: returns a random float between `a` and `b` (inclusive).
    *   `random.choice(sequence)`: selects a random item from a list or string.

---

## 3. PYTHON PART 2 (py2) CHEAT SHEET

### Slicing Sequences
Syntax: `sequence[start:stop:step]` (the stop index is exclusive):
```python
phrase = "quick brown"
print(phrase[6:9])     # Output: "bro"
print(phrase[:5])      # Output: "quick" (omitting start defaults to 0)
print(phrase[::2])     # Output: "qi bwn" (every 2nd character)
print(phrase[-2:])     # Output: "wn" (negative indices count from back)
```

### Mutability (High-Frequency Exam Topic)
1.  **Strings are Immutable**: String methods do not modify the original variable. They return a new value.
    ```python
    word = "python"
    word.upper()        # Returns "PYTHON", but original variable is unchanged!
    print(word)         # Prints "python"
    
    word = word.upper() # This works!
    print(word)         # Prints "PYTHON"
    ```
2.  **Lists are Mutable**: List structures can be updated in place. However, `.sort()` modifies the list and returns `None`.
    ```python
    my_list = ["x", "a", "q"]
    my_list.sort()      # Sorts the list in place
    print(my_list)      # Prints: ["a", "q", "x"]
    
    # EXAM TRICK WARNING:
    my_list = my_list.sort() # DANGER: my_list is now None!
    print(my_list)      # Prints: None
    ```

---

## 4. TKINTER GUI CHEAT SHEET

### variable vs textvariable
*   **`textvariable`**: Binds a widget to a `StringVar` or `IntVar` to dynamically read or display text. Used by: `Label`, `Entry`, `Button`, and `Spinbox`.
*   **`variable`**: Binds a widget to track integers/booleans/decimals directly. Used by: `Checkbutton`, `Scale`, and `Radiobutton`.

### Widget Configuration & State Options
Modify widget properties dynamically via `.config()`:
```python
submit_button.config(text="Sending...", state=DISABLED)
```
*   `NORMAL` (or `"normal"`): Active widget.
*   `DISABLED` (or `"disabled"`): Grayed out, unclickable.
*   `"readonly"`: User can read the value but cannot edit it (Entry/Spinbox).

### Detailed Widget Initialization & Use Cases
1.  **Label**: Shows static text or updates via `textvariable`.
    ```python
    my_label = Label(mainframe, text="Static Text", font=("Courier", 12, "bold"))
    name_var = StringVar()
    dynamic_label = Label(mainframe, textvariable=name_var)
    ```
2.  **Entry**: Text input box.
    ```python
    input_var = StringVar()
    password_entry = Entry(mainframe, textvariable=input_var, width=15, show="*")
    ```
3.  **Button**: Clickable element.
    ```python
    click_btn = Button(mainframe, text="Submit", command=my_function)
    ```
4.  **OptionMenu**: Dropdown selector. Unpacks choices using the asterisk `*` prefix. Callback requires 1 parameter.
    ```python
    choices = ["First", "Second"]
    choice_var = StringVar()
    menu = OptionMenu(mainframe, choice_var, *choices, command=my_callback)
    ```
5.  **Spinbox**: Up/down arrow scroll selection. Callback requires 0 parameters.
    ```python
    number_spin = Spinbox(mainframe, textvariable=spin_var, from_=1, to=10, command=my_callback)
    ```
6.  **Scale**: Sliding bar. Callback requires 1 parameter.
    ```python
    tip_scale = Scale(mainframe, from_=0, to=30, resolution=5, variable=slider_var, orient=HORIZONTAL, command=on_shift)
    ```
7.  **Checkbutton**: Checkbox. Binds to `variable`.
    ```python
    tax_check = Checkbutton(mainframe, text="Tax?", variable=check_var, onvalue=1, offvalue=0)
    ```
8.  **Listbox**: Scrollable select list.
    ```python
    todo_listbox = Listbox(mainframe, listvariable=todo_var, height=3)
    # selected_index = todo_listbox.curselection()[0]
    ```
9.  **PhotoImage**: Load PNG/GIF graphics.
    ```python
    flag_img = PhotoImage(file="flag.png")
    img_label = Label(mainframe, image=flag_img)
    img_label.image = flag_img  # Keep reference!
    ```

---

## 5. MOCK INTERACTIVE EXAM PREVIEW (40 MCQs & 10 Short Challenges)
*(The complete list of 40 MCQs and 10 interactive tracing problems are implemented dynamically inside the [index.html](index.html) file.)*
