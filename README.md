#Код одягае людыну на фото у сукню

import cv2
from PIL import Image

bro_img_path = 'bro.jpg'
dress_img_path = 'dress.png'
bro_in_dress_img_path = 'bro_in_dress.png'

image = cv2.imread(bro_img_path)

cv2.imshow("Bro", image)
cv2.waitKey()

bro_body_cascade = cv2.CascadeClassifier('haarcascade_fullbody.xml')
bro_body = bro_body_cascade.detectMultiScale(image)

x, y, w, h = bro_body[0]

cv2.rectangle(image, (x, y), (x+w, y+h), (15, 255, 127), 3)

cv2.imshow("Bro", image)
cv2.waitKey()

bro = Image.open(bro_img_path)
dress = Image.open(dress_img_path)
bro = bro.convert("RGBA")
dress = dress.convert("RGBA")

dress = dress.resize((w, h-x))
bro.paste(dress, (x, y), dress)
bro.save(bro_in_dress_img_path)
br_in_dress = cv2.imread(bro_in_dress_img_path)

cv2.imshow("bro_in_dress", bro_in_dress)
cv2.waitKey()
