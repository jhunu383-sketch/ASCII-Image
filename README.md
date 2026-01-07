# ASCII-Image
Turning images into ASCII portraits using pure Python logic, loops, and conditional statements.

# ASCII Image Generator from BMP (Pure Python)

##  Project Overview
This project converts a **BMP image file** into a **grayscale ASCII art representation** using **pure Python**.  
It does **not use any external libraries** like PIL, OpenCV, NumPy, or image converters.

The program directly **reads raw BMP binary data**, processes pixel brightness, and maps it to ASCII characters to recreate the image visually in the terminal.

This project demonstrates:
- File handling
- Binary data parsing
- Loops and conditional logic
- Mathematical image scaling
- ASCII visualization techniques

  ##  Project Purpose
The main objectives of this project are:

- To understand how **BMP image files are structured internally**
- To convert **RGB pixels into grayscale brightness**
- To map pixel brightness values to **ASCII characters**
- To generate an **ASCII-style portrait/image** using only core Python
- To avoid any external libraries and rely purely on logic and loops

This makes the project ideal for:
- Python core concepts
- Academic Minor/Mini projects
- Understanding low-level image processing

---


> Note: The image must be converted to BMP format before uploading to Google Colab.

---

## ⚙️ How the Code Works (High Level)
1. Reads BMP image in binary mode
2. Extracts width, height, and pixel data
3. Converts RGB pixels to grayscale
4. Maps brightness values to ASCII characters
5. Resizes the image logically
6. Prints ASCII art in the output console

---

##  How to Run on Google Colab

### Step 1: Upload Image
from google.colab import files
files.upload()
Upload:
darshan.bmp

Step 2: Set Configuration
import sys
FILE_PATH = "darshan.bmp"
WIDTH_OUT = 100

Step 3: Brightness to ASCII Mapping
def get_char(val):
    if val > 230:   return " "
    elif val > 200: return "."
    elif val > 180: return ":"
    elif val > 160: return "-"
    elif val > 140: return "="
    elif val > 120: return "+"
    elif val > 100: return "*"
    elif val > 80:  return "#"
    elif val > 60:  return "%"
    elif val > 40:  return "@"
    else:           return "$"

Step 4: Read BMP Image (Binary)
with open(FILE_PATH, 'rb') as f:
    f.seek(18)
    w_in = int.from_bytes(f.read(4), 'little')
    h_in = int.from_bytes(f.read(4), 'little')

   f.seek(10)
    offset = int.from_bytes(f.read(4), 'little')
    f.seek(offset)

   padding = (4 - (w_in * 3) % 4) % 4
    pixels = []
  for y in range(h_in):
        row = []
        for x in range(w_in):
            b = int.from_bytes(f.read(1), 'little')
            g = int.from_bytes(f.read(1), 'little')
            r = int.from_bytes(f.read(1), 'little')
      gray = int(0.299*r + 0.587*g + 0.114*b)
            row.append(gray)
  f.read(padding)
        pixels.append(row)
pixels = pixels[::-1]

Step 5: Resize and Print ASCII Art
h_out = int(WIDTH_OUT * (h_in / w_in) * 0.55)

for y in range(h_out):
    line = ""
    for x in range(WIDTH_OUT):
        src_x = int(x * (w_in / WIDTH_OUT))
        src_y = int(y * (h_in / h_out))

   pixel_brightness = pixels[src_y][src_x]
        line += get_char(pixel_brightness)

  print(line)


 Folder Structure
  project/
│── darshan.bmp
│── ascii_image.py
│── README.md


