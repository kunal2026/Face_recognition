Project: Attendance Marking System using Face Detection

This GitHub documentation provides an overview and explanation of a Python script that implements an attendance marking system using face detection. The script captures video from a webcam and identifies faces in the video frame. When a known face is detected, the system marks the person as present and records the attendance in a CSV file.

Prerequisites
Before running the code, make sure you have the following libraries installed:

face_recognition
OpenCV (cv2)
NumPy
CSV
os
datetime
You can install these libraries using pip:

bash
Copy code
pip install face_recognition opencv-python numpy
Usage
Clone the GitHub repository or download the script to your local machine.
Create a folder for storing images of known individuals (e.g., "known_faces").
Place images of the individuals you want to recognize in the "known_faces" folder. Ensure that each image is named with the person's name (e.g., "ayush.jpg").
Modify the script to include the correct image filenames and corresponding names in the known_face_encoding and known_faces_names lists.
Run the script using a Python interpreter:
bash
Copy code
python attendance_marking.py
The script will open a window displaying the webcam feed. When a known person's face is detected, their name and "PRESENT" will be displayed on the video frame. The attendance data will be recorded in a CSV file with the current date as the filename.

To exit the program, press the 'q' key.

Code Explanation
Here's an explanation of the important parts of the code:

The script captures video from the webcam using OpenCV.

It loads images of known individuals and encodes their faces using the face_recognition library.

The names and face encodings of known individuals are stored in known_face_encoding and known_faces_names lists.

The script continuously processes frames from the webcam feed, identifies faces, and compares them to the known faces using face_recognition.

When a known face is detected, the person's name is displayed on the video frame, and their attendance is recorded in a CSV file with the current date.

The script continues running until you press the 'q' key, at which point it releases the webcam and closes the video window.

The students list keeps track of students who have not yet been marked present.

Output
The script will print the list of students who are present and update the CSV file with the attendance data.
