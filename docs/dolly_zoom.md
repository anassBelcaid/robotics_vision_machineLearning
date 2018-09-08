---
layout : default
title  : Dolly Effect
date   :  2018/09/08  
categories:  homework
permalink : /dolly_zoom/
---


## Introduction ##

In this lab, we will implement **Dolly Zoom** effect used by film-makers to create a sensation of *vertigo*, a `falling-away-from-oneself feeling`. This lab is fairly simple and is meant to introduce you to the concepts of **projection** and **focal length**. It keeps the size of an object of interests constant in the image, while making the foreground and background objects appear larger or smaller by adjusting focal length and moving the camera. You will simulate the **Dolly Zoom** effect with a synthetic scene as shown in next Figure, which illustrates two cubes and one pyramid seen from the top view.


![alt]( " Camera Model")

## Dolly Zoom Effect ##

A point in 3D is projected onto the image plane through the pinhole (center of projection, **COP**):

$$
u = f\dfrac{X}{Z} \quad v = f \dfrac{Y}{Z}
$$

