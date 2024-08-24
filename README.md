# encreiptador-de-texto-alura-2024
import tkinter as tk
from tkinter import messagebox

def caesar_cipher(text, shift):
    encrypted_text = ''.join(chr((ord(char) - 32 + shift) % 95 + 32) for char in text)
    return encrypted_text

def encrypt():
    shift = int(shift_entry.get())
    text = text_entry.get("1.0", tk.END).strip()
    encrypted = caesar_cipher(text, shift)
    result_var.set(encrypted)

def decrypt():
    shift = -int(shift_entry.get())
    text = text_entry.get("1.0", tk.END).strip()
    decrypted = caesar_cipher(text, shift)
    result_var.set(decrypted)

def copy_to_clipboard():
    root.clipboard_clear()
    root.clipboard_append(result_var.get())
    messagebox.showinfo("Copied", "Text copied to clipboard!")

root = tk.Tk()
root.title("Text Encryptor/Decryptor")

frame = tk.Frame(root)
frame.pack(padx=10, pady=10)

text_entry_label = tk.Label(frame, text="Enter text:")
text_entry_label.pack()
text_entry = tk.Text(frame, height=10, width=50)
text_entry.pack()

shift_label = tk.Label(frame, text="Shift (integer):")
shift_label.pack()
shift_entry = tk.Entry(frame)
shift_entry.pack()

encrypt_button = tk.Button(frame, text="Encrypt", command=encrypt)
encrypt_button.pack(pady=5)

decrypt_button = tk.Button(frame, text="Decrypt", command=decrypt)
decrypt_button.pack(pady=5)

copy_button = tk.Button(frame, text="Copy", command=copy_to_clipboard)
copy_button.pack(pady=5)

result_var = tk.StringVar()
result_label = tk.Label(frame, text="Result:")
result_label.pack()
result_entry = tk.Entry(frame, textvariable=result_var, width=50)
result_entry.pack()

root.mainloop()
