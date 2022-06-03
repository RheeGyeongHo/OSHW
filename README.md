# OSHW
GitHub remote repository for RheeGyeongHo
import cv2

cap = cv2.VideoCapture(0)

width = int(cap.get(3)) 
height = int(cap.get(4))
fps = 20

face_cascade = cv2.CascadeClassifier('haarcascade_frontface.xml')
fcc = cv2.VideoWriter_fourcc('M', 'J', 'P', 'G')
out = cv2.VideoWriter('cctv.avi', fcc, fps, (width, height), isColor=False)
print(out.isOpened())
while (True) :
    ret, frame = cap.read()
    gray = cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY)
    faces = face_cascade.detectMultiScale(gray, 1.3, 5)

    print(len(faces))

    for (x,y,w,h) in faces:
         cv2.rectangle(frame,(x,y),(x+w,y+h),(255,0,0),2)
         
    if ret :
        gray = cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY)
        out.write(gray)
        cv2.imshow('frame', frame)

        if cv2.waitKey(1) & 0xFF == ord('q') : break

cap.release()
out.release()
cv2.destroyAllWindows()
