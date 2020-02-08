# gear-teeth-inspection

## Code:

clc;
close all;

f=imread('C:\Users\T.SHELBY\Desktop\gear inspection\gear_raw.png');
f=im2bw(f,0.3);          %original%
f1=imfill(f,'holes');     %holes filled%
mask=strel('disk',5);
h=[-1 -1 -1;-1 8 -1;-1 -1 -1];
c = imfilter(f1,h,'replicate');

f2=imerode(f1,mask);
f3=imdilate(f2,mask);
d=f1-f3;                  %only teeth%
mask1=strel('disk',5);
f4=imdilate(d,mask1);      %dilated teeth%
mask0=strel('disk',3);
f41=imdilate(d,mask0);
g=c-f4;
mask2=strel('disk',12);
f5=imdilate(g,mask2);
f6=f41+f5;                %with defects highlighted%
[L num]=bwlabel(d);       %getting total no of teethss in gear we got%

subplot(2,3,1),imshow(f),title('Original');
subplot(2,3,2),imshow(f1),title('Filled Holes');
subplot(2,3,3),imshow(d),title('Only Teeth');
subplot(2,3,4),imshow(f4),title('Dilated Teeth');
subplot(2,3,5),imshow(f6),title('With defects highlighted');
subplot(2,3,6),imshow(f),title(['No.of Teeth present::',num2str(num)]);









## Original image:

 ![gear_raw](/images/gear_raw.png)

=> converting this image to binary image and filling the holes.

## Filled holes:

![FILLED_HOLES](/images/FILLED_HOLES.png)
 

=> now getting only the teeth to find the missing teeth.




Only Teeth:

 ![only_teeth](/images/only_teeth.png)

=> dilating the image to get clear insight. And making the defects highlighted .

With defects highlighted:

![with_defects](/images/with_defects.png)
 	 


=> Now getting the no of teeth from only teeth image.





No of teeth present in given image:

 

![total](/images/total.png)




Total OUTPUT:

 ![FINAL_SUB](/images/FINAL_SUB.png)
