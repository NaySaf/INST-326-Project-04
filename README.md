# INST-326-Project-04

Improvement # 1
Add color to the background and the labels

Improvement # 2
Center the buttons on the pop up window and change the title to 'INST 326 Notebook'

Improvement # 3
Make the window smaller so the text fits appropriately

Print your notes
In the cell below, print or copy your ten notes.

add and run code here to print your ten notes
Title: Tips for Debugging in Python
Note: Debugging can be challenging when working with any type of program but here are some tips to improve the process in Python:

Use a Debugger: Using tools like 'pdb' can help guide you through the execution of your code and help you identify where things went wrong.
Logging: Logging progress and making notes throughout your code would help you capture your program during the developing stages at various points which is very helpful when it comes to tracing errors.
Links: Python Debugger (pdb): https://docs.python.org/3/library/pdb.html Python Logging: https://docs.python.org/3/library/logging.html

Tags: #Python #Debugging #ProgrammingTips #SoftwareDevelopment

Title: Loading Data from a CSV File using Pandas in Python Code: import pandas as pd
#Load data from a CSV file data = pd.read_csv('data.csv')

#Display the first five rows of the DataFrame print("First five rows of the DataFrame:") print(data.head())

Tags: #Python #DataScience #Pandas #DataLoading

Title: Creating python class and objects Code: #Define a class class MyClass:
#Constructor method def init(self, x, z): self.x = x self.z = z

#Method def my_method(self): return self.x + self.z

#Create an object of MyClass obj = MyClass(3, 7)

#Access attributes print(obj.x) print(obj.z)

Tags: Python, OOP, Classes, Objects

Title: Method overriding in python Code: #Define a parent class class Parent: def method(self): print("Parent's method")
#Define a child class inheriting from Parent class Child(Parent):

#Override the method def method(self): print("Child's method")

Tags: Python, OOP, Method Overriding, Inheritance

Title: Reading python files more efficiently Code: #open file in read mode with open('file.txt', 'r') as file:
#If the file is large, it's better to read it line by line for line in file: print(line.strip())

#for files without text, use binary mode with open('binary_file.bin', 'rb') as file:

Tags: #Python #FileIO #Efficiency

Title: Reading Multiple Notes In a TXT File Code: with open("FileName.txt", "r") as file:
#Read the lines from the file lines = file.readlines()

#Iterate through the lines for i in range(0, len(lines), number of lines each note has:

#Extract the attributes of the note from the lines
title = lines[i].strip()
text = lines[i + 1].strip()

#Add more attributes if note has more such as links and tags
#Print the note details
print(title)
print("Text:", text)
Tags: reading_txt_files

Title: Intro to Python Lists Code: # Creating a list fruits = ["apple", "banana", "cherry"]
#Adding an item to the end of the list fruits.append("orange")

#Adding an item at a specific position fruits.insert(1, "blueberry")

#Iterating through the list for fruit in fruits: print(fruit)

Links: https://docs.python.org/3/tutorial/datastructures.html Tags: #Python #Lists #ProgrammingBasics #DataStructures

Title: Using Python Dictionaries to Lookup Data Code: # Creating a dictionary contact_info = {'John': '555-0101', 'Mary': '555-0123', 'Sue': '555-0178'}
#Adding a new entry contact_info['Mike'] = '555-0222'

#Accessing a value print("John's contact number:", contact_info['John'])

#Iterating through the dictionary for name, number in contact_info.items(): print(f"{name}: {number}")

Links: https://docs.python.org/3/tutorial/datastructures.html#dictionaries Tags: #Python #Dictionaries #DataStructures #EfficientLookup

Title: Formatting Strings in Python with f-Strings Code: name = "Jane" age = 28
#Creating an f-string message = f"Hello, {name}. You are {age} years old."

print(message) #Output: Hello, Jane. You are 28 years old.

#Advanced usage: expressions within f-strings from math import pi print(f"Value of pi: {pi:.2f}") # Formats pi to 2 decimal places

Links: https://peps.python.org/pep-0498/ Tags: #Python #StringFormatting #fStrings #CodeEfficiency

Title: Looping Techniques in Python Using for-loops and List Comprehensions Code: # Example of a for-loop to iterate through a list fruits = ["apple", "banana", "cherry"] for fruit in fruits: print(fruit)
#Using a list comprehension to create a new list squares = [x**2 for x in range(10)] print(squares) # Output: [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]

#Conditional list comprehension even_squares = [x**2 for x in range(10) if x % 2 == 0] print(even_squares) # Output: [0, 4, 16, 36, 64]

Links: https://docs.python.org/3/tutorial/controlflow.html#for-statements https://docs.python.org/3/tutorial/datastructures.html#list-comprehensions

Tags: #Python #Loops #ListComprehensions #ProgrammingBasics #EfficientCoding

# CODE: 
#imports
import tkinter as tk
from tkinter import ttk
from tkinter import filedialog
import datetime # one module for working with dates and times
import json #this solution saves and opens json files. You may use a different file type and change the import accordingly

#The MainWindow class creates a custom GUI window based on the tkinter window (tk.Tk)
#It has an __init__() method, and three additional methods (new_note(), open_notebook(), and save_notebook())
#These methods correspond to new, open, and save buttons in the window.
#The new_note method calls the NoteForm class to create a new note form top level window.

class MainWindow(tk.Tk):
    def __init__(self):  #initialize the main window
        super().__init__() # initialize it as a tkinter window
        
        self.geometry("600x600") # set the default window size #Nayab improvement 3: change window size
        self.title('INST 326 Notebook') #set the default window title   #Nayab improvement 2: change window name
        self.notebook = [] # initialize an attribute named 'notebook' as an empty list
        self.notes = [] # list of note objects
        self.note = {}

        # create a frame called frame_main that covers the entire window.
        # not required for full credit
        # all other objects will be placed in frame_main instead of the window itself
        self.frame_main = tk.Frame(self)
        self.frame_main.pack(fill=tk.BOTH, expand=True)
        self.frame_main.config(bg='light blue') #Nayab improvement 1: change background color
        
        # create a frame in the new window that covers the entire window
        self.frame_notes = tk.Frame(self.frame_main)
        self.frame_notes.grid(row=1, column=3, rowspan=6, sticky='w')
        self.frame_notes.config(bg='gray') 
        
        #Nayab improvement 2: center the buttons
        self.frame_main.grid_rowconfigure(0, weight=1)
        self.frame_main.grid_rowconfigure(5, weight=1)
        self.frame_main.grid_columnconfigure(0, weight=1)
        self.frame_main.grid_columnconfigure(2, weight=1)
        
        #define some buttons and put them in a grid in frame_main
        # create new note button - opens a new note form
        btn01=tk.Button(self.frame_main, text='Create New Note', command=self.new_note)
        btn01.grid(padx=10, pady=10, row=1, column=1, sticky='nsew') #Nayab improvement 2: center the buttons
        
        # open notebook button - opens a notebook and displays its notes in the window
        btn02=tk.Button(self.frame_main, text='Open Notebook', command=self.open_notebook)
        btn02.grid(padx=10, pady=10, row=2, column=1, sticky='nsew')  #Nayab improvement 2: center the buttons
        
        # save notebook button - saves the notebook and refreshes the notes display
        btn03=tk.Button(self.frame_main, text='Save Notebook\nand Refresh', command=self.save_notebook)
        btn03.grid(padx=10, pady=10, row=3, column=1, sticky='nsew')  #Nayab improvement 2: center the buttons
        
        # quit button
        btn04=tk.Button(self.frame_main, text='Quit', command=self.destroy)
        btn04.grid(padx=10, pady=10, row=4, column=1, sticky='nsew') #Nayab improvement 2: center the buttons


    # define methods corresponding to the button commands
    
    # new_note opens a new toplevel window with a note form.
    # when the new note's submit button is pressed, the new note is added to the self.notebook
    # attribute in the main_window object.
     
       
    def new_note(self): # opens a new note form
        note_form = NoteForm(self, self.notebook, self.notes)
        return None

    def clear_frame(self, target_frame): # method for clearing old content from the frame
        for widgets in target_frame.winfo_children():
            widgets.destroy()

    def show_notes(self): # generates note objects and displays them in the main window
        self.clear_frame(self.frame_notes) # clears any previous display
        self.notes = [] # resets the notes object list
        for note in self.notebook: # create new note objects from the notebook and display them
            new_note = MakeNote(master=self.frame_notes, note_dict=note, notebook = self.notebook)
            self.notes.append(new_note)
            new_note.pack(padx=10, pady=10)
            new_note.config(height= 4, width=60, wraplength=300, justify=tk.LEFT)
        return None
    
    def open_notebook(self):
        # this opens json files. You may use different file types.
        filepath = filedialog.askopenfilename(initialdir="C:\\Users\\sdemp\\Documents\\GitHub\\Courses\\INST326\\test_files",
                                         filetypes=[("json files", "*.json"), 
                                                    ("csv files", ".csv"),
                                         ("all files", "*.*")])
        file = open(filepath, "r")
        self.notebook = json.load(file) # load the json file into self.notebook as a list of dictionaries
        file.close()
       
        self.show_notes() # once the file is loaded, call the method to display the notes in the window
        return None
    
    def save_notebook(self, notebook): #modifications to accomodate MakeNote.save_close() method
        self.notebook = notebook
        print('save notebook')
        print(self.notebook)
        # the following code saves the notebook as a json file. You  may use different file types
        file = filedialog.asksaveasfile(initialdir="C:\\Users\\sdemp\\Documents\\GitHub\\Courses\\INST326\\test_files",
                                              defaultextension=".json", 
                                        title="notebook01",
                                              filetypes=[("json file", ".json"),
                                             ("all files", ".*")])
        
        json_out = json.dumps(self.notebook, indent=2)
        file.write(json_out)
        
        self.show_notes() # this refreshes the notes display in the main window
        return None


#the NoteForm() class creates a Toplevel window that is a note form containing fields for
#data entry for title, text, link, and tags. It also calculates a meta field with date, time, and timezone
#the Noteform class has an __init__() method, and a submit() method that is called by a submit button
#the class may contain additional methods to perform tasks like calculating the metadata, for example

#PROJECT 03 MODIFICATIONS
#ADD NOTE_ID, AUTHOR, AND SNIPPET FIELDS TO NoteForm

class NoteForm(tk.Toplevel):
    
    def __init__(self, master, notebook, notes): # initialize the new object
        super().__init__(master) # initialize it as a toplevel window
        # set the new window's default parameters
        self.geometry("600x600") #Nayab improvement 3: change window size
        self.title('New INST 326 Note') #Nayab improvement 2: change window name
        
        # create a frame in the new window that covers the entire window
        self.frame_main = tk.Frame(self)
        self.frame_main.pack(fill=tk.BOTH, expand=True)
        self.frame_main.config(bg='light blue') #Nayab improvement 1: change background color

        #PROJECT 03 EDIT
        # moved the definition of self.notebook above the default note
        
        #define self.notebook as the notebook passed from the main window
        self.notebook = notebook
        #self.notes = notes (not necessary)
        
        # PROJECT 03 EDIT: ADD note_id
        self.last_id = len(self.notebook)
        

        
        #define default dummy text (for development purposes only)
        default_note = {"title":"new note title",
                     "text":"Lorem ipsum dolor sit amet, consectetur adipiscing elit. Etiam sit amet suscipit mi, non porttitor mauris. Aliquam in lorem risus. Proin mauris mauris, varius ac vulputate sed, tempor nec lacus. Morbi sodales turpis in placerat semper. Donec bibendum blandit ante sit amet hendrerit.", 
                    "link":"If there is a link with this note enter it here.",
                    "tags":"enter hashtags here",
                    "id":self.last_id + 1,
                    "author":"Scott Dempwolf",
                    "snippet":"# enter executable code snippet here \nprint('Hello World')",
                    "meta":"metadata added at submission"}
                    
        note = default_note # provided in anticipation of note editing functionality
        
        
        # create some labels and put them in the grid
        # we are using the grid layout. Notice the sticky='e' attribute. 
        # this causes the label to 'stick' to the 'east' side of the grid cell
        title_label = tk.Label(self.frame_main, bg='light green', fg='black', text='Note Title:') #Nayab improvement 1: change label color
        title_label.grid(padx=10, pady=10, row=1, column=0, sticky='e')

        text_label = tk.Label(self.frame_main, bg='light green', fg='black', text='Note Text:') #Nayab improvement 1: change label color
        text_label.grid(padx=10, pady=10, row=2, column=0, sticky='e')

        link_label = tk.Label(self.frame_main, bg='light green', fg='black', text='Note Link:') #Nayab improvement 1: change label color
        link_label.grid(padx=10, pady=10, row=3, column=0, sticky='e')

        tag_label = tk.Label(self.frame_main, bg='light green', fg='black', text='Note Tags:') #Nayab improvement 1: change label color
        tag_label.grid(padx=10, pady=10, row=4, column=0, sticky='e')
        
        tag_label = tk.Label(self.frame_main, bg='light green', fg='black', text='Note ID:') #Nayab improvement 1: change label color
        tag_label.grid(padx=10, pady=10, row=5, column=0, sticky='e')
        
        tag_label = tk.Label(self.frame_main, bg='light green', fg='black', text='Note Author:') #Nayab improvement 1: change label color
        tag_label.grid(padx=10, pady=10, row=6, column=0, sticky='e')
        
        tag_label = tk.Label(self.frame_main, bg='light green', fg='black', text='Snippet:') #Nayab improvement 1: change label color
        tag_label.grid(padx=10, pady=10, row=7, column=0, sticky='e')

        # create our note title entry field
        self.note_title = tk.Entry(self.frame_main, width=80)
        self.note_title.grid(padx=10, pady=10, row=1, column=1, sticky='w')
#         self.note_title.insert(0, note["title"]) # adds default text (useful during development)

        # create our note text field
        self.note_text = tk.Text(self.frame_main, height=10, width=60)
        self.note_text.grid(padx=10, pady=10, row=2, column=1)
        self.note_text.insert('1.0', note["text"]) # adds default text (useful during development)

        # create our note link entry field
        self.note_link = tk.Entry(self.frame_main, width=80)
        self.note_link.grid(padx=10, pady=10, row=3, column=1, sticky='w')
        self.note_link.insert(0, note["link"]) # adds default text (useful during development)

        # create our note tags entry field
        self.note_tags = tk.Entry(self.frame_main, width=80)
        self.note_tags.grid(padx=10, pady=10, row=4, column=1, sticky='w')
        self.note_tags.insert(0, note["tags"]) # adds default text (useful during development)

        # create our note id entry field
        self.note_id = tk.Entry(self.frame_main, width=80)
        self.note_id.grid(padx=10, pady=10, row=5, column=1, sticky='w')
        self.note_id.insert(0, note["id"]) # adds default text (useful during development)

        # create our note author entry field
        self.note_author = tk.Entry(self.frame_main, width=80)
        self.note_author.grid(padx=10, pady=10, row=6, column=1, sticky='w')
        self.note_author.insert(0, note["author"]) # adds default text (useful during development)

        # create our note snippet field
        self.snippet = tk.Text(self.frame_main, height=10, width=60)
        self.snippet.grid(padx=10, pady=10, row=7, column=1)
        self.snippet.insert('1.0', note["snippet"]) # adds default text (useful during development)        
        
        # create our note meta field if you want to add edit functionality
        #self.note_meta = tk.Entry(self.frame_main, width=80)
        #self.note_meta.grid(padx=10, pady=10, row=5, column=1, sticky='w')
        #self.note_meta.insert(0, note["meta"]) # adds default text (useful during development)
        

        # note that the parameters for the Entry box and Text box are slightly different.
        # The user can create multiple notes with the same note form. Each time the 'submit'
        # button is pressed, a new note is added to the notebook.

        b1 = tk.Button(self.frame_main, text='submit', command=self.submit)
        b1.grid(padx=10, pady=10, row=9, column=1, sticky='w')

        b5 = tk.Button(self.frame_main, text='close', command=self.destroy)
        b5.grid(padx=10, pady=10, row=9, column=0) 
       

    
    def submit(self):
        # calculate the date and time information for the meta field
        now = datetime.datetime.now() # gets the current date and time
        local_now = now.astimezone() # shows the local time and the GMT offset
        local_tz = local_now.tzinfo 
        created = datetime.datetime.now()
        
        # get all the input values and put them into a dictionary along with the metadata
        title = self.note_title.get()
        text = self.note_text.get('1.0', 'end').strip('\n')
        link = self.note_link.get()
        tags = self.note_tags.get()
        note_id = self.note_id.get()
        author = self.note_author.get()
        snippet = self.snippet.get('1.0', 'end').strip('\n')
        meta = f'note_id {note_id} created {created}, {local_tz} by {author}'
        note_dict = {'title':title, 'text':text, 'link':link, 'tags':tags, 'note_id':note_id, 'author':author, 'snippet':snippet, 'meta':meta}
        
        # add the dictionary to the notebook
        self.notebook.append(note_dict)
        self.last_id = self.last_id + 1
        self.note_id.delete(0, tk.END)
        self.note_id.insert(0, self.last_id + 1)
        
        return None

#The MakeNote class creates a new note object.
#The MakeNote class is a subclass of the tk.Button class, 
#which means each note instance has tk.Button functionality

class MakeNote(tk.Button):
    def __init__(self, master=None, note_dict=None, notebook=None): # the arguments on this line
        # are inbound, meaning we pass them when we instantiate the object
        super().__init__(master) # on this line we call the __init__ method of tk.Button and pass
        # the master attribute to it. This gives us all the button attributes and functionality
        
        self.notebook = notebook
        
        # define note attributes
        self.title = note_dict['title']
        self.text = note_dict['text']
        self.link = note_dict['link']
        self.tags = note_dict['tags']
        self.note_id = note_dict['note_id']
        self.author = note_dict['author']
        self.snippet = note_dict['snippet']
        self.meta = note_dict['meta']

        # configure note button; this creates a button with two lines of text
        self.config(bg='light gray', text=f"{self.title}\n{self.meta}")
        
        # Bind mouse events
        self.bind("<Enter>", self.on_hover)
        self.bind("<Leave>", self.on_leave)
        self.bind("<Button-1>", self.note_open)

    def save_close(self):
        self.note_window.destroy()
        main_window.save_notebook(notebook=self.notebook)
       

    def on_hover(self, event): # change the background when the cursor hovers over it
        self.config(bg="lightblue")  

    def on_leave(self, event): # change back when not hovering
        self.config(bg="light gray")  # Restore original color
        
    def note_open(self, event): # on mouse click, open note in new top window
        
        # create a new top window
        self.note_window = tk.Toplevel(main_window, bg="light gray", height=600, width=600)
        self.note_window.title(self.title)
        
        # create a frame in the new window that covers the entire window
        self.frame_main = tk.Frame(self.note_window)
        self.frame_main.pack(fill=tk.BOTH, expand=True)
        self.frame_main.config(bg='light gray')
        
        # create labels in the frame
        title_label = tk.Label(self.frame_main, bg='light green', fg='black', text='Note Title:') #Nayab improvement 1: change label color
        title_label.grid(padx=10, pady=10, row=1, column=0, sticky='e')
        title_content = tk.Label(self.frame_main, bg='light gray', text=self.title, wraplength=400, justify=tk.LEFT)
        title_content.grid(padx=10, pady=10, row=1, column=1, sticky='w')        

        text_label = tk.Label(self.frame_main, bg='light green', fg='black', text='Note Text:') #Nayab improvement 1: change label color
        text_label.grid(padx=10, pady=10, row=2, column=0, sticky='e')
        text_content = tk.Label(self.frame_main, bg='light gray', text=self.text, wraplength=400, justify=tk.LEFT)
        text_content.grid(padx=10, pady=10, row=2, column=1, sticky='w')

        link_label = tk.Label(self.frame_main, bg='light green', fg='black', text='Note Link:') #Nayab improvement 1: change label color
        link_label.grid(padx=10, pady=10, row=3, column=0, sticky='e')
        link_content = tk.Label(self.frame_main, bg='light gray', text=self.link, wraplength=400, justify=tk.LEFT)
        link_content.grid(padx=10, pady=10, row=3, column=1, sticky='w')
        
        tag_label = tk.Label(self.frame_main, bg='light green', fg='black', text='Note Tags:') #Nayab improvement 1: change label color
        tag_label.grid(padx=10, pady=10, row=4, column=0, sticky='e')
        tag_content = tk.Label(self.frame_main, bg='light gray', text=self.tags, wraplength=400, justify=tk.LEFT)
        tag_content.grid(padx=10, pady=10, row=4, column=1, sticky='w')

        note_id_label = tk.Label(self.frame_main, bg='light green', fg='black', text='Note ID:') #Nayab improvement 1: change label color
        note_id_label.grid(padx=10, pady=10, row=5, column=0, sticky='e')
        note_id_content = tk.Label(self.frame_main, bg='light gray', text=self.note_id, wraplength=400, justify=tk.LEFT)
        note_id_content.grid(padx=10, pady=10, row=5, column=1, sticky='w')

        author_label = tk.Label(self.frame_main, bg='light green', fg='black', text='Note Author:') #Nayab improvement 1: change label color
        author_label.grid(padx=10, pady=10, row=6, column=0, sticky='e')
        author_content = tk.Label(self.frame_main, bg='light gray', text=self.author, wraplength=400, justify=tk.LEFT)
        author_content.grid(padx=10, pady=10, row=6, column=1, sticky='w')

        snippet_label = tk.Label(self.frame_main, bg='light green', fg='black', text='Snippet:') #Nayab improvement 1: change label color
        snippet_label.grid(padx=10, pady=10, row=7, column=0, sticky='e')
        snippet_content = tk.Label(self.frame_main, bg='light gray', text=self.snippet, wraplength=400, justify=tk.LEFT)
        snippet_content.grid(padx=10, pady=10, row=7, column=1, sticky='w')
        
        meta_label = tk.Label(self.frame_main, bg='light green', fg='black', text='Note Meta:') #Nayab improvement 1: change label color
        meta_label.grid(padx=10, pady=10, row=8, column=0, sticky='e')
        meta_content = tk.Label(self.frame_main, bg='light gray', text=self.meta, wraplength=400, justify=tk.LEFT)
        meta_content.grid(padx=10, pady=10, row=8, column=1, sticky='w')        

        # create a button to close the note window
        b10 = tk.Button(self.frame_main, text='save and close', command=self.save_close)
        b10.grid(padx=10, pady=10, row=9, column=0)

        # create a button to edit the note
        b11 = tk.Button(self.frame_main, text='edit note', command=self.note_edit)
        b11.grid(padx=10, pady=10, row=9, column=1)

    def save_edits(self):
        # calculate the date and time information for the meta field
        now = datetime.datetime.now() # gets the current date and time
        local_now = now.astimezone() # shows the local time and the GMT offset
        local_tz = local_now.tzinfo 
        edited = datetime.datetime.now()
        
        # get all the input values and put them into a dictionary along with the metadata
        self.title = self.title_content.get()
        self.text = self.text_content.get('1.0', 'end').strip('\n')
        self.link = self.link_content.get()
        self.tags = self.tag_content.get()
        self.note_id = self.note_id_content.get()
        self.author = self.author_content.get()
        self.snippet = self.snippet_content.get('1.0', 'end').strip('\n')
        
        # modify the metadata to track edits
        self.meta = self.meta + f', edited {edited}, {local_tz}'
        note_dict = {'title':self.title, 'text':self.text, 'link':self.link, 'tags':self.tags, 'note_id':self.note_id, 'author':self.author, 'snippet':self.snippet, 'meta':self.meta}

        new_notebook = []
        for note in self.notebook:
            if note['note_id'] != self.note_id:
                new_notebook.append(note)
            else:
                new_notebook.append(note_dict)
        self.notebook = new_notebook
        
        # destroy the edit window
        self.edit_window.destroy()
        self.note_window.destroy()
        event = None
        self.note_open(event)
        
        
    def note_edit(self):
        # loads note into an editable window
        # create a new top window
        self.edit_window = tk.Toplevel(main_window, bg="light gray", height=700, width=600)
        self.edit_window.title(self.title)


        
        # create a frame in the new window that covers the entire window
        self.frame_main = tk.Frame(self.edit_window)
        self.frame_main.pack(fill=tk.BOTH, expand=True)
        self.frame_main.config(bg='light gray')
        
        # create labels in the frame
        title_label = tk.Label(self.frame_main, bg='light green', fg='black', text='Note Title:') #Nayab improvement 1: change label color
        title_label.grid(padx=10, pady=10, row=1, column=0, sticky='e')
        self.title_content = tk.Entry(self.frame_main, width=80)
        self.title_content.grid(padx=10, pady=10, row=1, column=1, sticky='w')
        self.title_content.insert(0, self.title)

        text_label = tk.Label(self.frame_main, bg='light green', fg='black', text='Note Text:') #Nayab improvement 1: change label color
        text_label.grid(padx=10, pady=10, row=2, column=0, sticky='e')
        self.text_content = tk.Text(self.frame_main, height=8, width=60)
        self.text_content.grid(padx=10, pady=10, row=2, column=1, sticky='w')
        self.text_content.insert('1.0', self.text)

        link_label = tk.Label(self.frame_main, bg='light green', fg='black', text='Note Link:') #Nayab improvement 1: change label color
        link_label.grid(padx=10, pady=10, row=3, column=0, sticky='e')
        self.link_content = tk.Entry(self.frame_main, width=80)
        self.link_content.grid(padx=10, pady=10, row=3, column=1, sticky='w')
        self.link_content.insert(0, self.link)
        
        tag_label = tk.Label(self.frame_main, bg='light green', fg='black', text='Note Tags:') #Nayab improvement 1: change label color
        tag_label.grid(padx=10, pady=10, row=4, column=0, sticky='e')
        self.tag_content = tk.Entry(self.frame_main, width=80)
        self.tag_content.grid(padx=10, pady=10, row=4, column=1, sticky='w')
        self.tag_content.insert(0, self.tags)

        note_id_label = tk.Label(self.frame_main, bg='light green', fg='black', text='Note ID:') #Nayab improvement 1: change label color
        note_id_label.grid(padx=10, pady=10, row=5, column=0, sticky='e')
        self.note_id_content = tk.Entry(self.frame_main, width=80)
        self.note_id_content.grid(padx=10, pady=10, row=5, column=1, sticky='w')
        self.note_id_content.insert(0, self.note_id)

        author_label = tk.Label(self.frame_main, bg='light green', fg='black', text='Note Author:') #Nayab improvement 1: change label color
        author_label.grid(padx=10, pady=10, row=6, column=0, sticky='e')
        self.author_content = tk.Entry(self.frame_main, width=80)
        self.author_content.grid(padx=10, pady=10, row=6, column=1, sticky='w')
        self.author_content.insert(0, self.author)

        snippet_label = tk.Label(self.frame_main, bg='light green', fg='black', text='Snippet:') #Nayab improvement 1: change label color
        snippet_label.grid(padx=10, pady=10, row=7, column=0, sticky='e')
        self.snippet_content = tk.Text(self.frame_main, height=8, width=60)
        self.snippet_content.grid(padx=10, pady=10, row=7, column=1, sticky='w')
        self.snippet_content.insert('1.0', self.snippet)
        
        meta_label = tk.Label(self.frame_main, bg='light green', fg='black', text='Note Meta:') #Nayab improvement 1: change label color
        meta_label.grid(padx=10, pady=10, row=8, column=0, sticky='e')
        self.meta_content = tk.Label(self.frame_main, bg='light gray', text=self.meta, wraplength=400, justify=tk.LEFT)
        self.meta_content.grid(padx=10, pady=10, row=8, column=1, sticky='w')        

        # create a button to close the edit window
        b10 = tk.Button(self.frame_main, text='close', command=self.edit_window.destroy)
        b10.grid(padx=10, pady=10, row=9, column=0)

        # create a button to edit the note
        b11 = tk.Button(self.frame_main, text='save edits', command=self.save_edits)
        b11.grid(padx=10, pady=10, row=9, column=1)
        
        
#main execution

if __name__ == '__main__':
    
    main_window = MainWindow() # this creates a notebook / main window called main_window. You may change the name if you want

    main_window.mainloop()
