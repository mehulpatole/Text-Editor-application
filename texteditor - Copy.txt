from tkinter import *
from tkinter.filedialog import askopenfile ,askopenfilename, asksaveasfilename

def newfile():
    global currentfile
    currentfile = None
    textarea.delete(1.0, END)
def openexisting():
    global currentfile 
    currentfile = askopenfilename(defaultextension= ".txt")
    textarea.delete(1.0, END)
    f= open(currentfile,"r")
    
    textarea.insert(1.0,f.read())
    f.close

def savefile():
    global currentfile
    if currentfile == None:
        currentfile= asksaveasfilename(initialfile= "untitled.txt",defaultextension= ".txt")
        f=  open(currentfile,"w")
        f.write(textarea.get(1.0,END))
        f.close()
    else:
        f=  open(currentfile,"w")
        f.write(textarea.get(1.0,END))
        f.close()



def exitfile():
    a.destroy()
def copytext():
    textarea.event_generate(("<<Copy>>"))
def pastetext():
    textarea.event_generate(("<<Paste>>"))
def cuttext():
    textarea.event_generate(("<<Cut>>"))

a= Tk()
a.title("Text Editor by MehulPatole")
currentfile  = None
textarea= Text(a)
textarea.pack(expand= True, fill= BOTH)

menubar= Menu(a)
filemenu = Menu(menubar, tearoff= 0) 
filemenu.add_command(label="new",command= newfile)

filemenu.add_command(label="open",command= openexisting)

filemenu.add_command(label="save",command= savefile)

filemenu.add_command(label="exit",command= exitfile)

menubar.add_cascade(label="File",menu= filemenu)


editmenu= Menu(menubar,tearoff= 0)
editmenu.add_command(label="copy",command= copytext)

editmenu.add_command(label="paste",command= pastetext)

editmenu.add_command(label="cut",command= cuttext)

menubar.add_cascade(label="Edit",menu= editmenu)

a.config(menu= menubar)





a.mainloop()
