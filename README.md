# Finding_Lane_lines

## 1.Pipeline


![solidYellowLeft](https://user-images.githubusercontent.com/45247795/62015654-17b46600-b1e0-11e9-828d-35257c7f7b3a.jpg)


### (1) Transform the image into grayscale
use cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)

![gray_img](https://user-images.githubusercontent.com/45247795/62017748-5cdd9580-b1ea-11e9-9626-7b547ab152e8.jpg)


### (3) Blur the image using a 7*7 kernel
blur = cv2.GaussianBlur(gray, (7, 7), 0)
![blur](https://user-images.githubusercontent.com/45247795/62017789-8a2a4380-b1ea-11e9-8d53-6817ade5072f.jpg)

### (4) Use canny edge detection to find all edges in the image

![canny](https://user-images.githubusercontent.com/45247795/62017796-8c8c9d80-b1ea-11e9-95a5-98c25c333dea.jpg)


### (5) Crop the image with a triangle
the triangle size is:
[(int(0.08 * width), height), (int(0.92 * width), height), (int(0.5 * width), int(height * 0.3))]

![cropped](https://user-images.githubusercontent.com/45247795/62017800-90202480-b1ea-11e9-9e54-87a031bb2892.jpg)


### (6) Using Hough to extract straight lines
  Here are my settings:
   minLineLength = 60
   maxLineGap = 10
   lines = cv2.HoughLinesP(lineImg, 1, np.pi / 120, 100, minLineLength, maxLineGap)
  These are the lines found by HoughLinesP:
  ![Hough](https://user-images.githubusercontent.com/45247795/62018179-3587c800-b1ec-11e9-805b-76e9c180133d.jpg)
  
### (7) separate left and right lines, calculate the slope, and draw green lines with the points found by getCoor()

![finalimg](https://user-images.githubusercontent.com/45247795/62018186-3882b880-b1ec-11e9-820c-48eec07ab040.jpg)


## 2.Shortcomings and future improvement
1. The green line disappears periodically in the output video.
  
  
2. This model assumes road being straight
  If the road bends, the triangle in this model will no longer be able to detect appropriate lane area.
  To imporve this, it needs to be broaden, maybe with a trapazoid
  If the road bends, the triangle in this model will no longer be able to detect appropriate lane area.





