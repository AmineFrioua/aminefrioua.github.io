---
layout: page
title: Human Detection
description: Guardin the plants from Huoooman
img: assets/img/5.jpg
importance: 3
category: work
---
## Mandatory Fun Intro: Open CV and human detection

Have you ever wanted to feel like a superhero with the ability to detect humans around you? Well, with OpenCV, I can do just that! In this post, I'll take you on a fun journey of using OpenCV to detect humans in images and videos.

Let's start by talking about OpenCV. It's an open-source computer vision library that contains hundreds of algorithms for various computer vision tasks. From object detection to image processing, OpenCV is a powerful tool that's widely used in the industry.

Now, let's dive into the exciting world of human detection! OpenCV offers several methods to detect humans, but one of the most popular approaches is using a technique called HOG (Histogram of Oriented Gradients) + SVM (Support Vector Machines). HOG is a feature descriptor that captures the shape and texture of an object, while SVM is a machine learning algorithm that can classify objects based on their features.

To harness the power of HOG + SVM in OpenCV, I first create a HOG descriptor and set its parameters. Using the cv2.HOGDescriptor() function, I can define parameters like the window size, block size, cell size, and more. Once the HOG descriptor is ready, I load a pre-trained SVM model using the cv2.HOGDescriptor().setSVMDetector() function. OpenCV provides a default SVM model for human detection, but I can also train my own model if I have a custom dataset.

With the HOG descriptor and SVM model in place, I'm all set to detect humans in images and videos. To detect humans in an image, I resize it to a fixed size and use the cv2.HOGDescriptor().detectMultiScale() function. This function returns a list of rectangles representing the detected human regions. To make the detection visually appealing, I draw these rectangles on the image using the cv2.rectangle() function.

When it comes to videos, the process is quite similar. I iterate over each frame of the video using a loop and apply the same HOG descriptor and SVM model to detect humans in each frame. To enhance the accuracy of human detection, I can incorporate additional features, such as using a background subtraction algorithm to remove the background from the video and focus only on detecting moving humans.

Human detection using OpenCV is not only useful but also a fun and exciting task. It finds applications in surveillance, robotics, and more. With the power of OpenCV and the HOG + SVM method, I can truly experience what it's like to have the superhuman ability to detect humans around me!

## Real Motive

So the real motive for this project is to create a script on a Jetson Nano hooked with a camera that will detect if any human have entered a forbidden section in the factory. but for a professional settings the Hog open cv detector will not be fast of effective enough, we might have some wrong reading so it is best use to wire a tensorflow human detector models after fine tuning it and make sure it works properly. 

## Tools used in this project
- Jetson nano as our brain 
- Any kind of Camera would work: we will resize and touch up the resolution that match our best performance
- Python for coding
- Open Cv
- Tensor flow ( will provide us with the model)



