import tkinter as tk
import random
import winsound

def clean_tiles():
    global cleaning_index
    cleaning_index = -1

def start_cleaning():
    global cleaning_index
    cleaning_index += 1
    if cleaning_index < len(tiles):
        tile = tiles[cleaning_index]
        tile.config(bg="white")
        tile.update()
        winsound.PlaySound("beep.wav", winsound.SND_FILENAME)
        root.after(500, start_cleaning)

def create_tiles(width, height):
    global tiles_frame, tiles, cleaning_index
    if tiles_frame:
        tiles_frame.destroy()

    tiles_frame = tk.Frame(root)
    tiles_frame.grid(row=0, column=2, rowspan=height, columnspan=width)

    tiles = []
    for row in range(height):
        for col in range(width):
            tile = tk.Label(tiles_frame, width=4, height=2, relief="solid")
            tile.grid(row=row, column=col)
            tiles.append(tile)
            tile.config(bg=random.choice(["purple", "white"]))
    cleaning_index = -1
def get_room_dimensions():
    width = int(width_entry.get())
    height = int(height_entry.get())
    create_tiles(width, height)
root = tk.Tk()
root.title("jaro barqi narges")
width_label = tk.Label(root, text="عرض اتاق:")
width_label.grid(row=0, column=0)
width_entry = tk.Entry(root)
width_entry.grid(row=0, column=1)
height_label = tk.Label(root, text="طول اتاق:")
height_label.grid(row=1, column=0)
height_entry = tk.Entry(root)
height_entry.grid(row=1, column=1)
dimensions_button = tk.Button(root, text="نمایش اتاقها *", command=get_room_dimensions)
dimensions_button.grid(row=2, column=0, columnspan=2)
clean_button = tk.Button(root, text="روشن کردن جاروبرقی", command=start_cleaning)
clean_button.grid(row=3, column=0, columnspan=2)
stop_button = tk.Button(root, text="خاموش کردن جاروبرقی", command=clean_tiles)
stop_button.grid(row=4, column=0, columnspan=2)

tiles_frame = None
tiles = []
cleaning_index = -1

root.mainloop()
این کد به ما در ساخت یک جارو برقی کمک میکند در پایتون 
