
# Finding Lane Lines on the Road

## Writeup Template

You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.



**Finding Lane Lines on the Road**

The goals / steps of this project are the following:

（1）Make a pipeline that finds lane lines on the road 

（2）Reflect on your work in a written report

## Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps：

    (1) Converting the images to grayscale.

    (2) Dealing with the grayscaled images using Gassian Blur.

    (3) Getting edges based on Canny Edge Detection.

    (4) Limiting the intested region.

    (5) Finding and drawing lines based on Hough Transform. 

To get some ideal effect, some special parameters were adjusted for many times. 

    (1) For Gaussian Blur, it almost showed little change when the kernel size equals 3 at first. After trying 
        for serval times, I set it to 7.

    (2) For Canny Edge Detection, I referred to the experience of adjusting parameter in the video exercise. 
        Based on the ratio(1:3), I set low thresholds 50 and high_thresholds 150.

    (3) For Hough Transform, I took(1, numpy.pi/180, 30, 5, 10) as ( rho, theta, threshold, min_line_len, max_line_gap).

In order to draw a single line on the left and right lanes, I modified the draw_lines() function 
by combining a fuction draw_fitting_lines() with draw_lines(). 

To solve the problem of extrapolating line segments, My basic logical thinking is as following:
    
    (1) Try to draw only two lines among the left and right lanes. 
    
    (2) The slope of lines must be limited to a certain range, which can mask most of irrelevant lines.
        (i.e., absoulte(slope)>0.5 and absolute(slope) <0.8) 
        
    (3) The two end points can obtained according to the parameter of images coordinate. And use the function polyfit(), 
        we can easily get the adjusted slope and intercept. The latter can be used to help obtain the x value of 
        coodinate. Based on them, real-time lines can be draw properly.

Some results are as following:


```python
%%html
<img src="test_images_output/whiteCarLaneSwitch.jpg" width=40%>  
<img src="test_images_output/solidWhiteRight.jpg" width=40%>  
```


<img src="test_images_output/whiteCarLaneSwitch.jpg" width=40%>  
<img src="test_images_output/solidWhiteRight.jpg" width=40%>  


### 2. Identify potential shortcomings with your current pipeline

    (1) The parameters. I adjusted the relevant parameters a lot to match six image given. It must need more time to 
        process massive date of images, and we cannot ensure the perfomance for everyone.

    (2) As is shown in challenged video, the line will disappears or cannot predicate when encounting some situations
        like shadow and urgent sharp curve road. This causes uncertain results, and should be taken in account.

### 3. Suggest possible improvements to your pipeline

    One improvement would be sovle the shadow or sharp curve road situation. By combining some other methods,though I 
    don't know now, we should create more accurate pipeline to sovle these problem.

    The other possible improvement I think should be focused on the parameters seting work.Get some algorithm from deep
    learning, and make it more easy and efficient.
