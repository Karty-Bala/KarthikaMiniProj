from tkinter import *
import phonenumbers
from phonenumbers import carrier
from phonenumbers import geocoder
from PIL import ImageTk
from tkinter import messagebox


class Login:
    def __init__(self, root):
        self.root = root
        self.root.title("Sim Info Display")
        self.root.geometry("1199x600+100+50")
        self.root.resizable(False, False)

        # Image Background
        self.bg = ImageTk.PhotoImage(file='imag.jpg')
        self.bg_image = Label(self.root, image=self.bg).place(x=0, y=0, relwidth=1, relheight=1)

        # Login frame
        frame = Frame(self.root, bg='white')
        frame.place(x=325, y=150, height=340, width=500)

        title = Label(frame, text="Sim Information", font=("Impact", 35, "bold"), fg="#d77337", bg='white').place(x=90, y=30)
        lbl_phn_num = Label(frame, text="Phone Number", font=("Goudy old style", 15, "bold"), fg="gray", bg='white').place(x=90, y=140)
        self.phn_num = Entry(frame, font=('times new roman', 15), bg='lightgray')
        self.phn_num.place(x=90, y=170, width=350, height=35)

        login_btn = Button(self.root, command=self.login_function, cursor='hand2', text="PROCEED", fg='white', bg='#d77337', font=('times new roman', 20)).place(x=475, y=470, width=180, height=40)

    def login_function(self):
        str_num = self.phn_num.get()
        service_number = phonenumbers.parse(str_num, "RO")
        isp_name = carrier.name_for_number(service_number, "en")
        ch_number = phonenumbers.parse(str_num, "CH")
        state = geocoder.description_for_number(ch_number, "en")
        messagebox.showinfo("Welcome", f"Welcome {state}\nYour Password {isp_name}")


root = Tk()
obj = Login(root)
root.mainloop()
