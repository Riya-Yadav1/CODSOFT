# CODSOFT
python internship projects alloted by CODSOFT
(PROJECT NO -1:TO-DO LIST)
import tkinter as tk            
from tkinter import ttk
from tkinter import messagebox
import sqlite3 as sql
  
def add_task():
    task_words = entry_field.get()
    if len(task_words)!=0:
        tasks.append(task_words)
        cursor.execute("insert into tasks values(?)",(task_words,))
        list_update()
        entry_field.delete(0,'end')
    else:
        messagebox.showinfo("Mistaken","field is blank ")
        
def list_update():
    clear_list()
    for task in tasks:
        tasks_listbox.insert('end',task)
def delete_task():
    try:
        value=tasks_listbox.get(tasks_listbox.curselection())
        if value in tasks:
            tasks.remove(value)
            list_update()
            cursor.execute('delete from tasks where title=?',(value,))
            
    except: 
         messagebox.showinfo('MISTAKEN!','No Task Selected. cannot vanish ')      
def remove_all_tasks():
    message_box=messagebox.askyesno('Delete All ','Are you sure?')
    if message_box==True:
        while (len(tasks)!=0):
            tasks.pop()
        cursor.execute('delete from tasks')
        list_update()
def clear_list():
    tasks_listbox.delete(0,'end')
    
def close():
    print(tasks)
    guiWindow.destroy()
    
def bring_database():
    while(len(tasks)!=0) :
        tasks.pop()
    for row in cursor.execute('select title from tasks'):
            tasks.append(row[0])
if __name__=="__main__":
    guiWindow=tk.Tk()
    guiWindow.title("TO DO LIST ")
    guiWindow.geometry("600x600+850+350")     
    guiWindow.resizable(0,0)
    guiWindow.configure(bg="#F0F8FF")
    connection=sql.connect('listoftasks.db')
    cursor=connection.cursor()
    cursor.execute('create table if not exists tasks(title text)')
    tasks=[] 
    top_frame=tk.Frame(guiWindow,bg="#6CA6CD")
    function_frame=tk.Frame(guiWindow,bg="#79CDCD")
    listbox_frame=tk.Frame(guiWindow,bg="#87CEEB") 
    top_frame.pack(fill="both")
    function_frame.pack(side="left",expand=True,fill="both")
    listbox_frame.pack(side="right",expand=True,fill="both")
    head_label=ttk.Label(
        top_frame,
        text="TO-Do LIST",
        font=("ariel","39"),
        background="#B0E0E6",
        foreground="black"
)       
    head_label.pack(padx=30,pady=30)
    task_label=ttk.Label(
        function_frame,
        text="Enter the task",
        font=("ariel","19","bold"),
        background="#FFF5EE",
        foreground="#000000"
    
)   

    task_label.place(x=40,y=50)
    entry_field= ttk.Entry(
        function_frame,
        font=("ariel","12"),
        width=22,
        background="#43CD80",
        foreground="#00CD66"
  )
    entry_field.place(x=40,y=90)
    add_button=ttk.Button(
        function_frame,
        text="Add",
        width=34,
        command=add_task
)
    del_button=ttk.Button(
        function_frame,
        text="Delete",
        width=34,
        command=delete_task
    
)
    remove_all_button=ttk.Button(
        function_frame,
        text="Delete All Tasks",
        width=34,
        command=remove_all_tasks
    
)            
    exit_button=ttk.Button(
        function_frame,
        text="EXIT",
        width=34,
        command=close
    
)
    add_button.place(x=30,y=120)
    del_button.place(x=30,y=160)
    remove_all_button.place(x=30,y=200)
    exit_button.place(x=30,y=240)
    tasks_listbox=tk.Listbox(
        listbox_frame,
        width=36,height=23,
        selectmode='SINGLE',
        background="#F0FFFF", foreground="blue",
        selectbackground="#CD853F",
        selectforeground="#FFFFFF"
    
)
    tasks_listbox.place(x=10,y=20)
    bring_database()
    list_update()
    guiWindow.mainloop()
    connection.commit()
    cursor.close()
________________________________________________________________________________________________________________________________________
(PROJECT NO -2: GUI BASED CALCULATOR)

import tkinter
from tkinter import*
from tkinter import messagebox
variable=""
A=0
operator=""

def button_1():
    global variable
    variable=variable+"1"
    data.set(variable)

def button_2():
    global variable
    variable=variable+"2"
    data.set(variable)  

def button_3():
    global variable
    variable=variable+"3"
    data.set(variable)  

def button_4():
    global variable
    variable=variable+"4"
    data.set(variable)       

def button_5():
    global variable
    variable=variable+"5"
    data.set(variable)    

def button_6():
    global variable
    variable=variable+"6"
    data.set(variable)    

def button_7():
    global variable
    variable=variable+"7"
    data.set(variable)

def button_8():
    global variable
    variable=variable+"8"
    data.set(variable)    

def button_9():
    global variable
    variable=variable+"9"
    data.set(variable)

def button_0():
    global variable
    variable=variable+"0"
    data.set(variable)    

def button_Add():
    global variable
    global A
    global operator
    A=float(variable)
    operator ="+"
    variable=variable+"+"
    data.set(variable)

def button_subtract():
    global variable
    global A
    global operator
    A=float(variable)
    operator ="-"
    variable=variable+"-"
    data.set(variable)    

def button_multiple():
    global variable
    global A
    global operator
    A=float(variable)
    operator ="*"
    variable=variable+"*"
    data.set(variable)    

def button_divide():
    global variable
    global A
    global operator
    A=float(variable)
    operator ="/"
    variable=variable+"/"
    data.set(variable)    

def button_equal():
    global variable
    global A
    global operator
    A=float(variable)
    operator ="="
    variable=variable+"="
    data.set(variable)   

def button_C():
    global variable
    global A
    global operator
    A=0
    operator=""
    variable=""
    data.set(variable)

def result():
    global variable
    global A
    global operator
    variable2=variable
    if operator=="+":
        a=float((variable2.split("+")[1]))
        X= A + a
        data.set(X)
        variable=str(X)
    elif operator=="-":
        a=float((variable2.split("-")[1]))
        X= A - a
        data.set(X)
        variable=str(X)   
    elif operator=="*":
        a=float((variable2.split("*")[1]))
        X= A * a
        data.set(X)
        variable=str(X)  
    elif operator=="/":
        a=float((variable2.split("/")[1]))
        if a==0:
            messagebox.showerror("Division with zero not allowed.") 
            A==""
            variable=""
            data.set(variable)
        else:
            X = float(A/a)
            data.set(X)
            variable=str(X)
guiWindow=tkinter.Tk()
guiWindow.geometry("400x600+500+85")
guiWindow.resizable(0,0)
guiWindow.title("CALCULATOR")
data=StringVar()
guiLabel=Label(
    guiWindow,
    text="Label",
    anchor=SE,
    font=("ariel",20),
    textvariable=data,
    background="black",
    fg="white"
)
guiLabel.pack(expand=True,fill="both")
frameOne=Frame(guiWindow,bg="#79CDCD")
frameOne.pack(expand=True,fill="both")
frameTwo=Frame(guiWindow,bg="#79CDCD")
frameTwo.pack(expand=True,fill="both")
frameThree=Frame(guiWindow,bg="#79CDCD")
frameThree.pack(expand=True,fill="both")
frameFour=Frame(guiWindow,bg="#79CDCD")
frameFour.pack(expand=True,fill="both")
buttonNINE=Button(
    frameOne,
    text="9",
    font=("cambria",22),
    relief=GROOVE,
    border=1,
    bg="#79CDCD",
    command=button_9
)
buttonNINE.pack(side=LEFT,expand=True,fill="both")
buttonEIGHT=Button(
    frameOne,
    text="8",
    font=("cambria",22),
    relief=GROOVE,
    border=1,
    bg="#79CDCD",
    command=button_8
)
buttonEIGHT.pack(side=LEFT,expand=True,fill="both")
buttonSEVEN=Button(
    frameOne,
    text="7",
    font=("cambria",22),
    relief=GROOVE,
    border=1,
    bg="#79CDCD",
    command=button_7
)
buttonSEVEN.pack(side=LEFT,expand=True,fill="both")
buttonC=Button(
    frameOne,
    text="C",
    font=("cambria",22),
    relief=GROOVE,
    border=1,
    bg="#F08080",
    command=button_C
)
buttonC.pack(side=LEFT,expand=True,fill="both")

buttonSIX=Button(
    frameTwo,
    text="6",
    font=("cambria",22),
    relief=GROOVE,
    border=1,
    bg="#79CDCD",
    command=button_6
)
buttonSIX.pack(side=LEFT,expand=True,fill="both")
buttonFIVE=Button(
    frameTwo,
    text="5",
    font=("cambria",22),
    relief=GROOVE,
    border=1,
    bg="#79CDCD",
    command=button_5
)
buttonFIVE.pack(side=LEFT,expand=True,fill="both")
buttonFOUR=Button(
    frameTwo,
    text="4",
    font=("cambria",22),
    relief=GROOVE,
    border=1,
    bg="#79CDCD",
    command=button_4
)
buttonFOUR.pack(side=LEFT,expand=True,fill="both")
buttonADD=Button(
    frameTwo,
    text="+",
    font=("cambria",22),
    relief=GROOVE,
    border=1,
    bg="#98F5FF",
    command=button_Add
)
buttonADD.pack(side=LEFT,expand=True,fill="both")
buttonTHREE=Button(
    frameThree,
    text="3",
    font=("cambria",22),
    relief=GROOVE,
    border=1,
    bg="#79CDCD",
    command=button_3
)
buttonTHREE.pack(side=LEFT,expand=True,fill="both")
buttonTWO=Button(
    frameThree,
    text="2",
    font=("cambria",22),
    relief=GROOVE,
    border=1,
    bg="#79CDCD",
    command=button_2
)
buttonTWO.pack(side=LEFT,expand=True,fill="both")
buttonONE=Button(
    frameThree,
    text="1",
    font=("cambria",22),
    relief=GROOVE,
    border=1,
    bg="#79CDCD",
    command=button_1
)
buttonONE.pack(side=LEFT,expand=True,fill="both")
buttonSUB=Button(
    frameThree,
    text="-",
    font=("cambria",22),
    relief=GROOVE,
    border=1,
    bg="#98F5FF",
    command=button_subtract
)
buttonSUB.pack(side=LEFT,expand=True,fill="both")
buttonZERO=Button(
    frameFour,
    text="0",
    font=("cambria",22),
    relief=GROOVE,
    border=1,
    bg="#79CDCD",
    command=button_0
)
buttonZERO.pack(side=LEFT,expand=True,fill="both")
buttonMUL=Button(
    frameFour,
    text="*",
    font=("cambria",22),
    relief=GROOVE,
    border=1,
    bg="#98F5FF",
    command=button_multiple
)
buttonMUL.pack(side=LEFT,expand=True,fill="both")
buttonDIV=Button(
    frameFour,
    text="/",
    font=("cambria",22),
    relief=GROOVE,
    border=1,
    bg="#98F5FF",
    command=button_divide
)
buttonDIV.pack(side=LEFT,expand=True,fill="both")
buttonEQUAL=Button(
    frameFour,
    text="=",
    font=("cambria",22),
    relief=GROOVE,
    border=1,
    bg="#00FA9A",
    command=result
)
buttonEQUAL.pack(side=LEFT,expand=True,fill="both")
guiWindow.mainloop()
_________________________________________________________________________________________________________________________________________(PROJECT no-3:PASSWORD GENERATOR)
import pyperclip
from tkinter import *
import random
base=Tk()
base.geometry("700x300")
paswrd=StringVar()
paslen=IntVar()
paslen.set(0)
def generating():
    list1=['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j',
             'k', 'l', 'm', 'n', 'o', 'p', 'q', 'r', 's', 't',
             'u', 'v', 'w', 'x', 'y', 'z', 'A', 'B', 'C', 'D',
             'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M', 'N',
             'O', 'P', 'Q', 'R', 'S', 'T', 'U', 'V', 'W', 'X',
             'Y', 'Z', '1', '2', '3', '4', '5', '6', '7', '8',
             '9', '0', ' ', '!', '@', '#', '$', '%', '^', '&',
             '*', '(', ')','~','`','{','}','[',']',';',':','.',
             ',','/','?','|']
    password=""
    for i in range(paslen.get()):
        password=password+random.choice(list1)
        paswrd.set(password)
def clipboardcopy():
    random_password= paswrd.get()    
    pyperclip.copy(random_password)
 
Label(
    base,
    text="PASSWORD GENERATOR",
    font="ariel 20 bold",   
    fg="#DB7093"
).pack()


Label(
    base,
    text="Enter The Length Of Password",
    fg="#43CD80"  
).pack(pady=3)
 
Entry(
    base,
    textvariable= paslen,
    bg=	"#DC143C"
).pack(pady=3) 

Button(
    base,
    text="CLICK",
    fg="#698B69",
    bg="#9BCD9B",
    command=generating,
).pack(pady=7)
Entry(
    base, 
    textvariable=paswrd,
    bg="#FFB90F",
    width=20,
    ).pack(pady=3)
Button(
    base,
    text="CLICK TO COPY CLIPBOARD",
    command=clipboardcopy,
    fg="#556B2F",
    bg='#A2CD5A'
).pack(pady=3)
base.mainloop()
_________________________________________________________________________________________________________________________________________(PROJECT NO -4:)

