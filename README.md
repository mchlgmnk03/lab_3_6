# NOTEBOOK
## Description
It is a siple command line notebook application. A common usage of classes, functions, methods, and docstrings can be seen in this task. 
This module has such functionalities:
+ **Display Notes**
+ **Search Notes**
+ **Add Note**
+ **Modify Note**
+ **Quit**
## Class Note
```python
def __init__(self, memo, tags=''):
  self.memo = memo
  self.tags = tags
  self.creation_date = datetime.date.today()
  global last_id
  last_id += 1
  self.id = last_id
 ```
Initializes variables memo, tags, and creation date.
```python
def match(self, filter):
    return filter in self.memo or filter in self.tags
```
**match** method checks if note cantains the filter texts and returns True or False.
## Class Notebook
```python
def __init__(self):
    self.notes = []
```
Initializes notebook as an empty list. 
```python
def new_note(self, memo, tags=''):
    self.notes.append(Note(memo, tags))
```
**new_note** method appends a note to to the previously created list of notes.
```python
def _find_note(self, note_id):
    for note in self.notes:
      if str(note.id) == str(note_id):
        return note
     return None
```
**_find_note** method finds a note by given id via iterating through all the notes.
```python
def modify_memo(self, note_id, memo):
    self._find_note(note_id).memo = memo
```
**modify_memo** method changes the note with specific id. 
```python
def modify_tags(self, note_id, tags):
    for note in self.notes:
        if note.id == note_id:
            note.tags = tags
            break
```
**modify_tags** method changes the tag of the note with specific id.
```python
def search(self, filter):
    return [note for note in self.notes if note.match(filter)]
```
**search** method finds notes that match the filter
## Class Menu 
```python
def __init__(self):
    self.notebook = Notebook()
    self.choices = {
    "1": self.show_notes,
    "2": self.search_notes,
    "3": self.add_note,
    "4": self.modify_note,
    "5": self.quit
    }
```
Initializes variables notebook and choices.
```python
def display_menu(self):
    print("""
    Notebook Menu
    1. Show all Notes
    2. Search Notes
    3. Add Note
    4. Modify Note
    5. Quit
    """)
```
**display_menu** method prints the notebook menu.
```python
def run(self):
    while True:
        self.display_menu()
        choice = input("Enter an option: ")
        action = self.choices.get(choice)
        if action:
            action()
        else:
            print("{0} is not a valid choice".format(choice))
```
**run** method runs the code and lets the user to choose the section of the menu.
```python
def show_notes(self, notes=None):
    if not notes:
        notes = self.notebook.notes
    for note in notes:
        print("{0}: {1}\n{2}".format(note.id, note.tags, note.memo))
```
**show_notes** method shows all the users's notes(contents of Notebook class).
```python
def search_notes(self):
    filter = input("Search for: ")
    notes = self.notebook.search(filter)
    self.show_notes(notes)
```
**search_notes** method searches for notes. 
```python
def add_note(self):
    memo = input("Enter a memo: ")
    self.notebook.new_note(memo)
    print("Your note has been added.")
```
**add_note** method adds a new note(to the Notebook class)
```python
def modify_note(self):
    id = input("Enter a note id: ")
    memo = input("Enter a memo: ")
    tags = input("Enter tags: ")
    if memo:
        self.notebook.modify_memo(id, memo)
    if tags:
        self.notebook.modify_tags(id, tags)
```
**modify_note** method allows to modify the tags or content of the specific note with its id.
```python
def quit(self):
    print("Thank you for using your notebook today.")
    sys.exit(0)
```
**quit** method quits the program.
