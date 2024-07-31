# GUI-based-simple-calculator-App
import tkinter as tk

class Calculator:
    def __init__(self, root):
        self.root = root
        self.root.title("Simple Calculator")
        self.root.geometry("400x400")

        self.expression = ""
        self.input_text = tk.StringVar()

        self.input_frame = tk.Frame(self.root)
        self.input_frame.pack()

        self.input_field = tk.Entry(self.input_frame, textvariable=self.input_text, font=('lucida', 20, 'bold'), bd=10, insertwidth=4, width=14, borderwidth=4)
        self.input_field.grid(row=0, column=0)
        self.input_field.pack(ipady=10)

        self.buttons_frame = tk.Frame(self.root)
        self.buttons_frame.pack()

        self.create_buttons()

    def create_buttons(self):
        buttons = [
            '7', '8', '9', '/', 'C',
            '4', '5', '6', '*', 'CE',
            '1', '2', '3', '-', 
            '+', '0', '.', '=',
        ]

        row = 0
        col = 0

        for button in buttons:
            if button == "=":
                btn = tk.Button(self.buttons_frame, text=button, fg="black", width=37, height=3, bd=0, bg="#eee", cursor="hand2", command=self.evaluate)
                btn.grid(row=row, column=col, columnspan=4)
            else:
                btn = tk.Button(self.buttons_frame, text=button, fg="black", width=10, height=3, bd=0, bg="#eee", cursor="hand2", command=lambda x=button: self.click(x))
                btn.grid(row=row, column=col)

            col += 1
            if col > 4:
                col = 0
                row += 1

    def click(self, item):
        if item == 'C':
            self.expression = ""
        elif item == 'CE':
            self.expression = self.expression[:-1]
        else:
            self.expression += str(item)
        self.input_text.set(self.expression)

    def evaluate(self):
        try:
            result = str(eval(self.expression))
            self.input_text.set(result)
            self.expression = result
        except:
            self.input_text.set("Error")
            self.expression = ""

if __name__ == "__main__":
    root = tk.Tk()
    calculator = Calculator(root)
    root.mainloop()
