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
_________________________________________________________________________________________________________________________________________
(PROJECT no-3:PASSWORD GENERATOR)
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
_______________________________________________________________________________________________________________________________________
(PROJECT NO -4:)
from tkinter import *
from tkinter import ttk
import requests
def data_get():
    city =city_name.get()
    data=requests.get("https://api.openweathermap.org/data/2.5/weather?q="+ city +"&appid=ffc5bbc8882420c14e38be49e4e1b30b").json()
    w_label1.config(text=data["weather"][0]["main"])
    wd_label1.config(text=data['weather'][0]['description'])
    temp_label1.config(text=str(int(data['main']['temp']-273.15)))
    per_label1.config(text=data['main']['pressure'])


base=Tk()
base.title("WEATHER FORECAST")
base.config(bg="#8470FF")
base.geometry("600x570+450+50")

title_label=Label(base,text="WEATHER FORECAST ",font=("Brush Script MT", "30",'bold'),background="orange")
title_label.place(x=25,y=50,height=50,width=450)
city_name=StringVar()
list_name=["Andhra Pradesh","Arunachal Pradesh ","Assam","Bihar","Chhattisgarh",
           "Goa","Gujarat","Haryana","Himachal Pradesh","Jammu and Kashmir",
           "Jharkhand","Karnataka","Kerala","Madhya Pradesh","Maharashtra",
           "Manipur","Meghalaya","Mizoram","Nagaland","Odisha","Punjab",
           "Rajasthan","Sikkim","Tamil Nadu","Telangana","Tripura","Uttar Pradesh",
           "Uttarakhand","West Bengal","Andaman and Nicobar Islands","Chandigarh",
           "Dadra and Nagar Haveli","Daman and Diu","Lakshadweep","National Capital Territory of Delhi","Puducherry"]
com=ttk.Combobox(base,text="WEATHER FORECAST",values=list_name,font=("Time new roman",20,"bold"),textvariable=city_name,background="#FFA500")
com.place(x=115,y=120,height=50,width=370)

title_label.place(x=75,y=50,height=50,width=450)

w_label=Label(base,text="WEATHER CLIMATE",font=("Time new roman",20,"bold"),background="#DA70D6")
w_label.place(x=20,y=260,height=50,width=300)

w_label1=Label(base,text="",font=("Time new roman",18,"bold"),background="#FF83FA")
w_label1.place(x=350,y=260,height=50,width=230)


wd_label=Label(base,text="WEATHER DESCRIPTION",font=("Time new roman",19,"bold"),background="#DA70D6")
wd_label.place(x=20,y=330,height=50,width=300)

wd_label1=Label(base,text="",font=("Time new roman",18,"bold"),background="#FF83FA")
wd_label1.place(x=350,y=330,height=50,width=230)


temp_label=Label(base,text="TEMPERATURE",font=("Time new roman",19,"bold"),background="#DA70D6")
temp_label.place(x=25,y=400,height=50,width=210)

temp_label1=Label(base,text="",font=("Time new roman",18,"bold"),background="#FF83FA")
temp_label1.place(x=350,y=400,height=50,width=230)

per_label=Label(base,text="PRESSURE",font=("Time new roman",19,"bold"),background="#DA70D6")
per_label.place(x=25,y=470,height=50,width=210)

per_label1=Label(base,text="",font=("Time new roman",18,"bold"),background="#FF83FA")
per_label1.place(x=350,y=470,height=50,width=230)

go_button=Button(base,text="GO",font=("Time new roman",20,"bold"),command=data_get,background="#98FB98")
go_button.place(x=240,y=190,height=50,width=100)

base.mainloop()
_________________________________________________________________________________________________________________________________________________________________________________________
(PROJECT NO-5)
import tkinter as tk
from tkinter import StringVar

base = tk.Tk()
base.title("QUIZ GAME")
base.geometry("500x600+450+50")

questions=["who is the founder of dell?","The basic unit of excel____.","who started the concept of app","who  is ceo of tesla","what is the capital of France?"]
options=[["Michael Dell","Larry Dell","James Dell","Howard Dell","Michael Dell"],
         ["cell","tables","column","rows","cell"],
         ["Apple","Nokia","google","Microsoft","Apple"],
         ["Bill Gates","Elon Musk","Mark Zukerberg","Tim Cook","Elon Musk"],
         ["London","Berlin","Madrid","Paris","Paris"]]
frame=tk.Frame(padx=10,pady=10,bg="#43CD80")
question_label=tk.Label(frame,height=5,width=28,font=("Verdana",20),wraplength=500)

v1=StringVar(frame)
v2=StringVar(frame)
v3=StringVar(frame)
v4=StringVar(frame)


option1=tk.Radiobutton(frame,bg="#43CD80",variable=v1,font=("Verdana",20),command=lambda:checkAnswer(option1))
option2=tk.Radiobutton(frame,bg="#43CD80",variable=v2,font=("Verdana",20),command=lambda:checkAnswer(option2))
option3=tk.Radiobutton(frame,bg="#43CD80",variable=v3,font=("Verdana",20),command=lambda:checkAnswer(option3))
option4=tk.Radiobutton(frame,bg="#43CD80",variable=v4,font=("Verdana",20),command=lambda:checkAnswer(option4))

button_next=tk.Button(frame,text="NEXT",bg="yellow",font=("Verdana",20),command=lambda:displayNextQuestion())
frame.pack(fill="both",expand="true")
question_label.grid(row=0,column=0)

option1.grid(sticky="W",row=1, column=0)
option2.grid(sticky="W",row=2, column=0)
option3.grid(sticky="W",row=3, column=0)
option4.grid(sticky="W",row=4, column=0)

button_next.grid(row=6, column=0)

index=0
correct=0

def disablebuttons(state):
    option1['state']=state
    option2['state']=state
    option3['state']=state
    option4['state']=state

def checkAnswer(radio):
    global correct,index
    
    if radio["text"]== options[index][4]:
        correct+=1
    index+=1  
    disablebuttons("disable")  
    
def displayNextQuestion():   
    global index,correct
    
    if button_next["text"]== "Restart the quiz":
        correct=0
        index=0
        question_label['bg']="grey"
        button_next['text']='Next'    
    if index==len(options):
        question_label["text"]=str(correct)+"/"+str(len(options))
        button_next["text"]= "Restart the quiz"
        if correct >=len(options)/2:
            question_label['bg']="#79CDCD"
        else:
            question_label['bg']="red"
    else:
        question_label['text']=questions[index]
    
        disablebuttons("normal") 
        opts=options[index]
        option1['text']= opts[0]
        option2['text']= opts[1]
        option3['text']= opts[2]
        option4['text']= opts[3]
        v1.set(opts[0])
        v2.set(opts[1])
        v3.set(opts[2])
        v4.set(opts[3])
        if index == len(options)-1:
            button_next["text"]="Check the results"

displayNextQuestion()



base.mainloop()

