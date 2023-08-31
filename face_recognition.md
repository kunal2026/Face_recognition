import face_recognition
import cv2
import numpy as np
import csv
import os
from datetime import datetime
 
video_capture = cv2.VideoCapture(0)
 
ayush = face_recognition.load_image_file("ayush.jpg")
ayushe = face_recognition.face_encodings(ayush)[0]
 
punish = face_recognition.load_image_file("punish.jpg")
punishe = face_recognition.face_encodings(punish)[0]
 
kunal = face_recognition.load_image_file("myphoto.jpg")
kunale = face_recognition.face_encodings(kunal)[0]
 
faculty = face_recognition.load_image_file("karthikeyan.jpg")
facultye = face_recognition.face_encodings(faculty)[0]
 
known_face_encoding = [
ayushe,
punishe,
kunale,
facultye
]
 
known_faces_names = [
"AYUSH RANA",
"PUNISH MIDHA",
"KUNAL MUKHERJEE",
"Dr. KARTHIKEYAN SIR"
]
 
students = known_faces_names.copy()
 
face_locations = []
face_encodings = []
face_names = []
s=True
 
 
now = datetime.now()
current_date = now.strftime("%Y-%m-%d")
 
 
 
f = open(current_date+'.csv','w+',newline = '')
lnwriter = csv.writer(f)
 
while True:
    _,frame = video_capture.read()
    small_frame = cv2.resize(frame,(0,0),fx=0.5,fy=0.5)
    rgb_small_frame = small_frame[:,:,::-1]
    if s:
        face_locations = face_recognition.face_locations(rgb_small_frame)
        face_encodings = face_recognition.face_encodings(rgb_small_frame,face_locations)
        face_names = []
        for face_encoding in face_encodings:
            matches = face_recognition.compare_faces(known_face_encoding,face_encoding)
            name=""
            face_distance = face_recognition.face_distance(known_face_encoding,face_encoding)
            best_match_index = np.argmin(face_distance)
            if matches[best_match_index]:
                name = known_faces_names[best_match_index]
 
            face_names.append(name)
            if name in known_faces_names:
                font = cv2.FONT_HERSHEY_SIMPLEX
                bottomLeftCornerOfText = (100,100)
                fontScale              = 1.5
                fontColor              = (255,0,0)
                thickness              = 3
                lineType               = 2
 
                cv2.putText(frame,name+' PRESENT', 
                    bottomLeftCornerOfText, 
                    font, 
                    fontScale,
                    fontColor,
                    thickness,
                    lineType)
 
                if name in students:
                    students.remove(name)
                    print(students)
                    current_time = now.strftime("%H-%M-%S")
                    lnwriter.writerow([name,current_time])
    cv2.imshow("DSA PROJECT ATTENDANCE MARKING SYSTEM USING FACE DETECTON",frame)
    if cv2.waitKey(1) & 0xFF == ord('q'):
        break
 
video_capture.release()
cv2.destroyAllWindows()
f.close()
