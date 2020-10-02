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

![projectile-motion](https://github.com/kadirtastepe/Measurement-of-LSF-and-MTF-of-a-Digital-Camera/blob/main/samples.png)






