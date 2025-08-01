# Calculator
this a calculator replica which is made using python
import tkinter as tk

def click(event):
    global expression
    text = event.widget.cget("text")

    if text == "=":
        try:
            result = str(eval(expression))
            display_var.set(result)
            expression = result  # Continue from result
        except:
            display_var.set("Error")
            expression = ""
    elif text == "C":
        expression = ""
        display_var.set("")
    elif text == "±":
        if expression.startswith("-"):
            expression = expression[1:]
        else:
            expression = "-" + expression
        display_var.set(expression)
    elif text == "%":
        try:
            result = str(eval(expression)/100)
            display_var.set(result)
            expression = result
        except:
            display_var.set("Error")
            expression = ""
    else:
        expression += text
        display_var.set(expression)

root = tk.Tk()
root.title("Python Calculator")
root.geometry("320x450")
root.resizable(0, 0)

expression = ""
display_var = tk.StringVar()


entry = tk.Entry(root, textvar=display_var, font="Arial 24", bd=10, relief=tk.RIDGE, justify="right")
entry.pack(fill="both", ipadx=8, pady=10, padx=10)


buttons = [
    ["C", "%", "±", "/"],
    ["7", "8", "9", "*"],
    ["4", "5", "6", "-"],
    ["1", "2", "3", "+"],
    ["0", ".", "="]
]


frame = tk.Frame(root)
frame.pack()

for row in buttons:
    row_frame = tk.Frame(frame)
    row_frame.pack(expand=True, fill="both")
    for item in row:
        btn = tk.Button(row_frame, text=item, font="Arial 18", relief=tk.RIDGE, height=2, width=5)
        btn.pack(side="left", expand=True, fill="both", padx=2, pady=2)
        btn.bind("<Button-1>", click)

root.mainloop()
