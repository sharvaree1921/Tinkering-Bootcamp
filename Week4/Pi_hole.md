## Pi-hole
- We have seen many adds popping up while surfing internet.To stop those adds from showing,we use add-blocker to stop them from being displayed.
- Rpi is powerful to control and set itself as add-blocker.
- Pi-hole puts Rpi present at our home in place of the default DNS server
- The Pi-hole acts as a Domain Name System (DNS) server, something that sits in-between you and the internet. This allows the Pi-hole to intercept any 
outgoing or incoming DNS requests and can block or pass certain domains from accessing your device, keeping your computer and other devices safe from ads.
- Rpi(now acting as DNS sever) will send IP of only URL,but not IP of Adds.Hence on a website,we see only blank spaces instead of adds popping up.

![dns](https://github.com/tinkererslaboratory/Tinkering_Bootcamp_TSS/blob/master/Week%204%20resources/Week%204%20Session%202/how-dns-works.jpg)

- As in the figure,our Rpi will replace the DNS server and itself become the DNS server.
- Web Admin Interface:Decides what to show and what to not.
- Log queries: keeps record of all commands and hence we can see that which adds are actually blocked by our RPI as DNS server.

Now,we will have a brief overview of certain python libraries used in writing code in Rpi-
1. **Pillow** : Library dealing with image processing 
2. **Pytesseract** : Library dealing with optical character recognition (For text extraction)
3. **gTTS** : Library dealing with text to speech(google)

### 1.Pillow
We can have multiple features of Pillow library ti play with images and videos.
we will see the codes one by one.
1.
```python
from PIL import Image
img=Image.open('abc.jpg')
print(img) # gives basic info about image-RGB format,shape,etc 
Image._show(img)  #displayes image
a=img.copy() #copies the image into another variable a
map.save('img.jpg')  #saves image
```
2.
```python
from PIL import Image
from PIL import ImageFilter
img=Image.open('abc.jpg')
blurred=img.filter(ImageFilter.BLUR)  #blurrs the image
help(ImageFilter)  #If we dont know about the functions used in ImageFilter,just run this command
Image._show(img)
Image.show(blurred)
```
3.
```python
from PIL import Image
a=Image.open('abc.jpg')
print('{}x{}'.format(a.width,a.height))  #to print w and h of image
a=a.crop((0,100),(500,600))  #to crop the image with top-left and bottom-right coordinates
Image._show(a)
```
4.
```python
from PIL import Image
from PIL mport ImageEnhancer
a=Image.open('abc.jpg')
enhancer=ImageEnhance.Brightness(a)  #created object of ImageEnhance
Image._show(enhancer.enhance(0.3))  #0.3 is the argument which should be in between 0(dark) to 1(bright)
```
5.This code prints the a series of images in incresing brightness level
```python
from PIL import Image
from PIL import ImageFilter
from PIL import ImageDraw
from PIL import ImageEnhance
can= Image.open("can.jpg")
can=can.convert('RGB')
print(can.width,can.height)
ecan=ImageEnhance.Brightness(can)
bunch=[]
for i in range(0,10):
    bunch.append(ecan.enhance(i/10))
fimage=bunch[0]
sheet=Image.new(fimage.mode,(fimage.width,10*fimage.height)) #this creates a new blank sheet of mentioned size
x=0
y=0
for p in bunch:
    sheet.paste(p,(x,y))
    y=y+5000
sheet=sheet.resize((400,5000))
Image._show(sheet)
```

### 2.Pytesseract
- Optical Character Recognition library(text extraction)

1. for image containg simple text
```python
from PIL import Image
import pytesseract as tess
tess.pytesseract.tesseract_cmd=r'D:\Python\Tesseract\tesseract.exe'  #this is additional step for using pytesseract library directly
name=input("Name of the image:")   #taking inut of image through text
img=Image.open(name)
Image._show(img)
text=tess.image_to_string(img)  #prints the extracted text
print(text)
```

2.What if we have image which is noisy,and hence it is difficult to extract text.So,first we convert it into RGB 
format and then apply threshold to get rid of noise.And the apply tess to extract text as normal.
```python
from PIL import Image
import pytesseract as tess
tess.pytesseract.tesseract_cmd=r'D:\Python\Tesseract\tesseract.exe'  #this is additional step for using pytesseract library directly
name=input("Name of the image:")   #taking inut of image through text
img=Image.open(name)
img=img.convert('L') #convert into gray scale
def binarize(img_to_transform,threshold):
   output_img=img_to_transform.convert('L')
   for x in range(output_image.width):
      for y in range(output_image.height):
         if output_image.getpixel((x,y))<threshold:
            output_image.putpixel((x,y),0)
         else:
            output_image.putpixel((x,y),255)
    return output_image
binarize(img,127)
Image._show(img)
text=tess.image_to_string(img)  #prints the extracted text
print(text)
```

### GTTS (Google Text To Speech)

1.
```python
from gtts import gTTS
import os

text ="Hello World"
output=gTTS(text)
output.save("out.mp3")
os.system("start out.mp3")
```

So,now we have three powerful libraries to solve an innovative problem statement-
Read the image,extract the text and read aloud that text so that blind people can hear it.

Like ,we can have Rpi,its camera module and attach a button.When a button is pressed,a picture a clicked and further processing takes place.
