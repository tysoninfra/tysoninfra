## Tyson! Cyber Infrastructure Specialist 👋
<h1>Infrastructure Overview Topology<h1>
  <h2>   ![Infra_Topology_by_Tyson](https://github.com/user-attachments/assets/cbe98372-623b-4bdd-84cc-a02fd1c55007)
   <h2>
    <h3># Active Directory(AD/DC) Setup Guide<h3>
      <body>Active Directory is the major component of the Windows base IT Infrastructure<body>

<h4># Python Source Code for the own screen recorder program for windows x64bit <h4>
  <body>
    # Tyson's own screen recorder source code#
    import pyautogui
import cv2
import numpy as np
import time
import tkinter as tk
from threading import Thread
from tkinter import messagebox

import os

# Get the path to the Videos folder
videos_folder = os.path.join(os.environ['USERPROFILE'], 'Videos')

# Define the new folder name
new_folder_name = "Tyson_Recording_Folder"

# Create the full path for the new folder
new_folder_path = os.path.join(videos_folder, new_folder_name)

# Create the folder (if it doesn't exist already)
if not os.path.exists(new_folder_path):
    os.makedirs(new_folder_path)
    print(f"Folder created: {new_folder_path}")
else:
    print(f"Folder already exists: {new_folder_path}")

# Screen recording parameters
resolution = (1920, 1080)
codec = cv2.VideoWriter_fourcc(*"XVID")
filename = os.path.join(new_folder_path, "Tyson_Recording.avi")  # Full path for saving the video file
fps = 10.0
capture_delay = 1 / fps  # Delay between frames

# Initialize the VideoWriter object
out = None
recording = False  # Flag to check if recording is active

def start_recording():
    global recording, out

    if recording:
        messagebox.showinfo("Recording", "Already recording!")
        return

    # Initialize the VideoWriter
    out = cv2.VideoWriter(filename, codec, fps, resolution)
    recording = True

    # Change the button color to red
    start_button.config(bg="red", text="Recording... Stop Recording")

    # Start the recording in a separate thread
    Thread(target=record_screen).start()

def stop_recording():
    global recording

    if not recording:
        messagebox.showinfo("Recording", "Recording is not active.")
        return

    recording = False  # Stop the recording

    # Change the button color back to default
    start_button.config(bg="green", text="Start Recording")

def record_screen():
    global recording, out

    cv2.namedWindow("Kaytolive", cv2.WINDOW_NORMAL)
    cv2.resizeWindow("Kaytolive", 480, 270)

    while recording:
        start_time = time.time()

        # Capture the screen
        img = pyautogui.screenshot()
        frame = np.array(img)
        frame = cv2.cvtColor(frame, cv2.COLOR_BGR2RGB)

        # Write the frame to the output file
        out.write(frame)

        # Show the live recording preview
        cv2.imshow("Kaytolive", frame)

        # Control the frame rate
        elapsed_time = time.time() - start_time
        time.sleep(max(0, capture_delay - elapsed_time))

    # Release resources
    out.release()
    cv2.destroyAllWindows()

# Set up the Tkinter interface
root = tk.Tk()
root.title("Screen Recorder")

# Set the default button color to green
start_button = tk.Button(root, text="Start Recording", bg="green", command=start_recording)
start_button.pack(pady=10)

stop_button = tk.Button(root, text="Stop Recording", command=stop_recording)
stop_button.pack(pady=10)

# Add minimize functionality
def minimize_window():
    root.iconify()

minimize_button = tk.Button(root, text="Minimize", command=minimize_window)
minimize_button.pack(pady=10)

# Run the Tkinter main loop
root.mainloop()

    <body>
<!--
**tysoninfra/tysoninfra** is a ✨ _special_ ✨ repository because its `README.md` (this file) appears on your GitHub profile.

Here are some ideas to get you started:

- 🔭 I’m currently working on ...
- 🌱 I’m currently learning ...
- 👯 I’m looking to collaborate on ...
- 🤔 I’m looking for help with ...
- 💬 Ask me about ...
- 📫 How to reach me: ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...
-->
