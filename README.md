# cogntiv Ex

## How to run me code:
My entire code is in the jupyter notebook in this repository. It should run easily on google colab using the GPU runtime.
My Bulding blocks and way of thinking are inside tha tab: "Cogntiv Ex Version" and the images' files must be uploaded first to the root folder of the session (without their folders).
I have a tab with utils function, loading the data, and the research process.

## Qustions:
### 1
I tested 3 methosds of generalizing the paper code to more images: introducing the image number in a couple of different coordinate systems:
**I**: Setting all images on one axis, like a "video" wit ha new axis "t", meaning the inmput to the model is a (x,y,t), where t is the image number.
This result a slow learning curve, with the "assumption" that image 2, and 3 have something in common - which they dont. and so at the begining of learning one can see the images 1 and 2 look alike, but the model learns to fit them right at the end.
I tested enlarging this model before trying another coordinate, which made a better fit.
**II**: Setting thew images on a one-hot-encoding, where each image get an axis, leaving all the images equally close to each other. This wasn't efficient memmory wise, so an example of 10 images training is available in display.
**III**": Setting the images on a binary representation, using each axis twice, using log2(N) dimensions to represent the images location. this was much more efficient in dimensions, keeping the images densed in space, allowing interpolation for later required tasks (preventing the line situation, where on the way to some image, we will bump into another image).
 **Generalization** was define in this case by the ability of the model to infere the image values for higher resolution, when trained on lower resolution.
 Graphs of generalization for 96 px size from 48 are present and can be re-generated in the notebook. Generalization using this method for 100 images doesn't look great, but for few images the results are very promising.

### 2
- Higer resolution is demonstrated using the "upsample" function, using existing models to show result.
- I expected the dense representation to work best for interpolation, and chose 3 pairs of iamges, where only one bit in representation needs to be chanegd (like 00 and 10) and show the interpolation of them, but the results where poor.
It seems strange that it did generelize in that manner when trained on 3 imnages, but for 10 or 100 it didn't. Trying smaller networks didn't change the outcome.

I didn't quite understand the selection part, because the way I tried to solve this ex. I chose the images representations. I'm not sure I understand what you ment by using the network re represent the images themselvs. because the image recieve all iamges together, from coordinated, there is no one layer that can be said to have a specific image representation. And so I don't understand the normal notation of "embedding" or image representation in this case. 
Getting the images closer to each other in the dense representation, compared to the spatial XY coordinates, so it wont be able to get so "crazy" in between the images, like seen in this case.

This only means changing the distance in the new subspace of image location, compared with the -1->1 scale of the pixels. hopfully not allowing the output to change so drasticallly when moving from image to image in that space.
