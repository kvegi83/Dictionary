from tkinter import *
from tkinter import messagebox

import json
from difflib import get_close_matches
data=json.load(open("C:\\Users\\RAMC\\Downloads\\pjdata.json.json"))
def meanings(event):
    word=e1.get()
    temp=get_close_matches(word,data.keys())
    if word in data:
        out_put=data[word]
        if(type(out_put)==list):
            temp1=""
            for i in out_put:
                temp1=temp1+i+"\n"
            t1.insert(END,temp1)
        else:
            t1.insert(END,out_put)
    elif(len(temp)>0):
        yn=messagebox.askyesnocancel("confirm","do u mean %s ?" %temp[0])
        if(yn==1):
            t1.insert(END,data[temp[0]])
        elif(yn==0):
            t1.insert(END,"Please double check your entry")
        else:
            t1.insert(END,"we dint understand your entry!")
    else:
        t1.insert(END,"no such word found!")
T=Tk()

T.title("Dictionary")

l1=Label(text="enter word:")
l1.grid(column=0,row=0)

e1=Entry(T)
e1.grid(column=1,row=0)

t1=Text(T,height=6,width=23)
t1.grid(column=0,row=1,rowspan=6,columnspan=2)

e1.bind("<Return>",meanings)

sb1=Scrollbar(T)
sb1.grid(row=1,column=3,rowspan=6)
t1.configure(yscrollcommand=sb1.set)
sb1.configure(command=t1.yview)

def clear_text():
    t1.delete(0.0,END)
b=Button(text="clear screen",command=clear_text)
b.grid(column=1,row=7)
T.mainloop

