import tkinter
import cv2
import PIL.Image, PIL.ImageTk
from functools import partial
import threading
import imutils
import time
stream=cv2.VideoCapture("clip.mp4")

flag=True
def play(speed):
    global flag
    print(f"You have clicked on Play.Speed is: {speed}")
        # Play the video in reverse mode
    frame1=stream.get(cv2.CAP_PROP_POS_FRAMES)
    stream.set(cv2.CAP_PROP_POS_FRAMES, frame1+speed)
    grabbed,frame=stream.read()
    if not grabbed:
        exit()
    frame=imutils.resize(frame, width= SET_WIDTH, height=SET_HEIGHT)
    frame=PIL.ImageTk.PhotoImage(image=PIL.Image.fromarray(frame))
    canvas.image=frame
    canvas.create_image(0,0,image= frame, anchor=tkinter.NW)
    if flag:
        canvas.create_text(170,26,fill="green",front="Times,20,bold", text="Decision Pending!!")
    flag=not flag

def pending(decision):
    # Display Decision Pending Image
    frame=cv2.cvtColor(cv2.imread("Dession pending.png"),cv2.COLOR_BGR2RGB)
    frame=imutils.resize(frame, width= SET_WIDTH, height= SET_HEIGHT)
    frame=PIL.ImageTk.PhotoImage(image=PIL.Image.fromarray(frame))
    canvas.image=frame
    canvas.create_image(0,0,image= frame, anchor=tkinter.NW)
    # Wait for 1 second
    time.sleep(1.5)
    # Display Sponsor Image
    frame=cv2.cvtColor(cv2.imread("Sponsor.png"),cv2.COLOR_BGR2RGB)
    frame=imutils.resize(frame, width= SET_WIDTH, height= SET_HEIGHT)
    frame=PIL.ImageTk.PhotoImage(image=PIL.Image.fromarray(frame))
    canvas.image=frame
    canvas.create_image(0,0,image= frame, anchor=tkinter.NW)
    # Wait for 2 second
    time.sleep(2)
    # Display Decision
    if decision=='out':
        decisionImg="OUT.png"
    else:
        decisionImg="NOT OUT.png"
    frame=cv2.cvtColor(cv2.imread(decisionImg),cv2.COLOR_BGR2RGB)
    frame=imutils.resize(frame, width= SET_WIDTH, height= SET_HEIGHT)
    frame=PIL.ImageTk.PhotoImage(image=PIL.Image.fromarray(frame))
    canvas.image=frame
    canvas.create_image(0,0,image= frame, anchor=tkinter.NW)
def Not_out():
    thread=threading.Thread(target=pending, args=('not out',))
    thread.daemon=1
    thread.start()
    print("Player is Not Out")
def out():
    thread=threading.Thread(target=pending, args=('out',))
    thread.daemon=1
    thread.start()
    print("Player is Out")
SET_WIDTH =800
SET_HEIGHT= 500

window=tkinter.Tk()
window.title("Goutam's Third umpair Decision Review Kit")
cv_img=cv2.cvtColor(cv2.imread("WELCOME TO GOUTAM'S DRS KIT.png"),cv2.COLOR_BGR2RGB)
cv_img=imutils.resize(cv_img, width= SET_WIDTH, height= SET_HEIGHT)
canvas=tkinter.Canvas(window,width=SET_WIDTH,height=SET_HEIGHT)
photo=PIL.ImageTk.PhotoImage(image=PIL.Image.fromarray(cv_img))
image_on_canvas=canvas.create_image(0,0,ancho=tkinter.NW,image=photo)
canvas.pack()



btn=tkinter.Button(window,text="<<Previous(fast)",width=50,command=partial(play,10))
btn.pack()

btn=tkinter.Button(window,text="<<Previous(slow)",width=50,command=partial(play,-10))
btn.pack()

btn=tkinter.Button(window,text="Next(fast)>>",width=50,command=partial(play,15))
btn.pack()

btn=tkinter.Button(window,text="Next(slow)>>",width=50,command=partial(play,-30))
btn.pack()

btn=tkinter.Button(window,text="Give Notout",width=50,command=Not_out)
btn.pack()

btn=tkinter.Button(window,text="Give Out",width=50,command=out)
btn.pack()

window.mainloop()
