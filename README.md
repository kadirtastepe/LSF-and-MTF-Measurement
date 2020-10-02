# Measurement-of-LSF-and-MTF-of-a-Digital-Camera

## Introduction
### Summary
In this work I tried to find Line Spread Function(LSF) and Modulation Transfer Function(MTF) of my smartphone. Objects are designed in Mathematica 12.1.1 program. For LSF I designed equidistant objects (binarized white and black stripes) with different widths and for MTF I designed equidistant objects (binarized white and black stripes) with same and various widths in actual size. Actual size means computer designs based on pixels, I designed objects in real life measure mm unit. Then I printed the objects, objects dimensions are in mm. Then I take pictures of the objects with my smartphone camera in Automatic mode, without using zoom or flashlight and I save images as RAW JPEG and transfered to my computer with data cable for eliminating data loss. In order to analyse the images I take a small samples from images by using paint. Because whole image contains lot of information and I do not have enough computer power for that. Samples analyzed in MATLAB R2020a. By plotting graphs intensities of pixels of grayscaled images versus pixels, I have calculated LSF and MTF.

## Line Spread Function(LSF)

### Methods of Experiment

A test image (Figure 1) is prepared in Mathematica 12.1.1. All objects are in actual size. This test image includes three vertical and horzontal lines with widths of 1mm, 0.5mm and 0.1mm and one rectangle 5mm × 3mm. First I created equally distant stripes in actual size, then changed the widths of the stripes.

### Mathematica Code For Real Size Object Generation
```Mathematica
mm = 7.2/2.54; (*Convert pixel to mm*)
a = {0, 5, 6, 7, 7.5, 8.5} mm; (*widths*)
c = {5, 6, 7, 7.5, 8.5, 8.6} mm;
b = 0 mm;
d = 10 mm;
color = {White, Black, White, Black, White, Black};
(*By using this method we can control widths of 
the stripes*)
graphics = 
 Show[Graphics[
   Table[Style[Rectangle[{Part[a, x], b}, 
   {Part[c, x], d}], Part[color, x]], {x, 1, 6}]]]
(*Export*)
(*Horizontal Stripes*)
Export["plot.png", 
Binarize@ImageResize[graphics,{8.6 mm, 10 mm}]] 
(*Vertical Stripes*)
Export["plot1.png", Rotate[Binarize@
ImageResize[graphics, {8.6 mm, 10 mm}], Pi/2]] 
(*Rectangle*)
Export["plot2.png", 
Binarize@ImageResize[Graphics[
Rectangle[]], {5 mm, 3 mm}]] 
```

Designed objects in [mm] dimensions pictures taken by camera. In this process dimensions has changed. Now image dimensions are in pixel. By using actual size(mm) of the object and pixel size of the object ratio, we can make conversion of dimensions. 

### Estimating Pixel to mm Conversion

Pixel to mm conversion estimated by using corner points of the rectangle in Figure 2. By using the ratio of actual size of the rectangle and pixels detected by camera pixel to mm conversion estimated as follows. 

![samples](https://github.com/kadirtastepe/LSF-and-MTF-Measurement/blob/main/samples.png)
Figure: Test Image Taken by Camera, Image Size 3120 x 4160 pixels

<img src="http://latex.codecogs.com/svg.latex?R_{pxmm,vertical}&space;=&space;\frac{2042-1917}{3mm}&space;\cong&space;41.67&space;px/mm" title="http://latex.codecogs.com/svg.latex?R_{pxmm,vertical} = \frac{2042-1917}{3mm} \cong 41.67 px/mm" />

<img src="http://latex.codecogs.com/svg.latex?R_{pxmm,horizontal}&space;=&space;\frac{1651-1451}{5mm}&space;=&space;40.00&space;px/mm&space;" title="http://latex.codecogs.com/svg.latex?R_{pxmm,horizontal} = \frac{1651-1451}{5mm} = 40.00 px/mm " />

<img src="http://latex.codecogs.com/svg.latex?R_{pxmm}&space;\cong&space;&space;40.84&space;px/mm&space;" title="http://latex.codecogs.com/svg.latex?R_{pxmm} \cong 40.84 px/mm " />

Which means there is an approximately 41 pixel per mm. With this ratio we can use both dimensions. I take a small sample(red region in Figure 2) with paint from the whole picture and using MATLAB analyzed it. Because I do not have enough equipment to analyse the whole picture. Of course in several methods the whole picture could be analyzed. But slice of a whole picture is enough to calculate the line spread function.

### Finding Intensity Profile of Images
Now we need information about intensities of pixels in sample image.

### Matlab Code for Finding Intensity and Pixels
Small samples taken as we see in Figure 2 from the Figure 1 by using paint. Plotting intensities of small samples of grayscaled image pixels in vertical and horizontal directions gives intensity profile of the image.

```Matlab
clear all, close all, clc

I = imread('verticaldata.png');
%I = imread('horizontaldata.png'); 

x = [0 size(I,2)];
y = [size(I,1)/2 size(I,1)/2];
%y = [0 size(I,1)];
%x = [size(I,2)/2 size(I,2)/2];

c = improfile(I,x,y);
figure
subplot(2,1,1)
imshow(I)
hold on
plot(x,y,'r')
subplot(2,1,2)
plot(-c(:,1,1)/max(c(:1,1))+1,'r') %Normalized
hold on
xlabel("Pixel Distance")
ylabel("Intensity")
title("Vertical Sample");grid on ;grid minor
```

### Output of the program

![LSFV](https://github.com/kadirtastepe/LSF-and-MTF-Measurement/blob/main/LSFV.png)

![LSFH](https://github.com/kadirtastepe/LSF-and-MTF-Measurement/blob/main/LSFH.png)






