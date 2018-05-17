# face-recognition
#Python Module For Computer Vision
#Dimas Yoga Pratama UNIVERSITAS MUHAMMADIYAH SURAKARTA
#May-18-2018
#credit for channel Youtube Bukalapak and Ebook Computer Vision 2nd from PACTKTUB
import cv2 
 
#detect face
face_cascade = cv2.CascadeClassifier('haarcascade_frontalface_default.xml')

#detect eyes (optional)
eye_cascade = cv2.CascadeClassifier('haarcascade_eye.xml') 
 
# capture frames from a camera
cap = cv2.VideoCapture('Engineers Life at GO-JE.mp4')
 
# looping terus jika objek(camera/video) sudah terinisiasi 
while 1: 
 
    # menangkap frame dari kamera / video
    ret, img = cap.read() 
 
    #konversi sebagian / seluruh frame ke dalam warna abu - abu u
    gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
 
    # deteksi wajah dengan beberapa kemungkinan ukuran wajah yang berbeda
    faces = face_cascade.detectMultiScale(gray, 1.3, 5)
 
    for (x,y,w,h) in faces:
        # Persegi deteksi wajah
        cv2.rectangle(img,(x,y),(x+w,y+h),(255,255,0),2) 
        roi_gray = gray[y:y+h, x:x+w]
        roi_color = img[y:y+h, x:x+w]
 
        # deteksi mata dengan berbagai kemungkinan ukuran
        eyes = eye_cascade.detectMultiScale(roi_gray) 
 
        #Presegi deteksi mata
        for (ex,ey,ew,eh) in eyes:
            cv2.rectangle(roi_color,(ex,ey),(ex+ew,ey+eh),(0,127,255),2)
 
    # menampilkan window 
    cv2.imshow('PROJECT AKHIR PRAKTIKUM',img)
 
    # Waktu tunggu saat keluar
    k = cv2.waitKey(30) & 0xff
    if k == 27:
        break
 
# Tutup Window
cap.release()
 
# dealokasikan memori yang sudah terpakai
cv2.destroyAllWindows() 
