---
layout : default
title  : Dolly Effect
date   :  2018/09/08  
categories:  homework
math : true
permalink : /dolly_zoom/
---
{%include mathjax.html%}
## Introduction ##

In this lab, we will implement **Dolly Zoom** effect used by film-makers to create a sensation of *vertigo*, a `falling-away-from-oneself feeling`. This lab is fairly simple and is meant to introduce you to the concepts of **projection** and **focal length**. It keeps the size of an object of interests constant in the image, while making the foreground and background objects appear larger or smaller by adjusting focal length and moving the camera. You will simulate the **Dolly Zoom** effect with a synthetic scene as shown in next Figure, which illustrates two cubes and one pyramid seen from the top view.


![alt](/assets/camera.png)

## Dolly Zoom Effect ##

A point in $3D$ is projected onto the image plane through the pinhole (center of projection, **COP**):

$$
u= f\dfrac{X}{Z} \quad v = f \dfrac{Y}{Z}
$$

where $(u,v)$ is the image coordinate of the projection, $(X,Y,Z)$ is the $3D$ point, and $f$ is the focal length of the camera. When the camera moves along with its $Z$-axis, the depth, $Z$, changes and therefore, the projection,$(u,v)$ , changes. In our paticular case the $Z$ of interest is $d_{ref}$, the depth of the objects in the scene. In the following discussion we will only mention the $u$ coordinate to simplify the equations, as we are focused mainly on height.

$$
\begin{equation}
u = f_{ref}\dfrac{X}{d_{ref}}= f^{'}\dfrac{X}{d_{ref}-pos}
\end{equation}
$$

where $pos$ is the movement of the camera along its $Z$ axis ( direction indicates approaching to objects) and $f^{'}$ is the modified focal length. $f_{ref}$ and  $d_{ref}$ are the focal length and depth of an object in the original image, respectively. Dolly zoom effect exploits the compensation between depth and focal length, which produces depth sensation. The relationship between all the variable names as given in the code is described in the next figure, and when implementing the description in the code you should reference it.

![displacment](/assets/illustration_camera_deplacment.png "Illustration")
Finally, the next figure illustrates the focal length/depth compensation: the camera moves away from the object while changing its focal length such that the height of the object A,$h_1=400$ , in both original and moved images remains constant. Note that the heights of the other background objects are changed due to this effect.

![pic alt](/assets/illustration_camera2.png)

## Implementation ##

For the first part of this lab, you need to implement the function `compute_focal_length`. Given the depth of the object of interest $d_{ref}$, and the focal length $f_{ref}$ of the camera for the original image, you need to estimate the modified focal length $f^{'}$ , such that the height of the object remains constant as the camera moves in the $Z$-axis (different input $pos$  values). When you have implemented the function, you can demonstrate the dolly soom effect in the synthetic scene above by using the `run_dolly_zoom.m`.

{% highlight matlab %}
function [ f ] = compute_focal_length( d_ref, f_ref, pos )
% compute camera focal length using given camera position
%
% Input:
% - d_ref: 1 by 1 double, distance of the object whose size remains constant
% - f_ref: 1 by 1 double, previous camera focal length
% - pos: 1 by n, each element represent camera center position on the z axis.
% Output:
% - f: 1 by n, camera focal length

% Put your CODE here
f = (f_ref/d_ref).*(d_ref - pos); 

end
{% endhighlight %}


## Compute focal length and position ##


For the second part of this lab, you need to implement the function `compute_f_pos`. This time you are given the distances of two objects ( $d_1$ and $d_2$ ) and their corresponding heights in the physical world ( $H_1$ and $H_2$  respectively), and for a specified original focal length $f_{ref}$, you need to estimate the modified focal length $f$ such that the ratio of the heights of the two objects in the image $\dfrac{h_1}{h_2}$ is the same as the input value $ratio$ , while the height  of the first object remains constant. The description and the notation of the problem is the same as the one presented in the previous part, so you can use it as reference.


{%highlight matlab%}
function [ f, pos ] = compute_f_pos( d1_ref, d2_ref, H1, H2, ratio, f_ref )
% compute camera focal length and camera position to achieve centain ratio
% between objects
%
% Input:
% - d1_ref: distance of the first object
% - d2_ref: distance of the second object
% - H1: height of the first object in physical world
% - H2: height of the second object in physical world
% - ratio: ratio between two objects (h1/h2)
% - f_ref: 1 by 1 double, previous camera focal length
% Output:
% - f: 1 by 1, camera focal length
% - pos: 1 by 1, camera position

% Put your CODE here
% constructing the system


A = [ d1_ref, f_ref ; d1_ref*ratio*H2, f_ref*H1];
b= [d1_ref*f_ref; d2_ref*f_ref*H1];

%solving the system
X= A\b;
f = X(1);
pos = X(2);


{%endhighlight%}


