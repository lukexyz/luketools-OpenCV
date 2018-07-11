# Computer Vision
:mount_fuji:  Misc OpenCV code for working with images and video streams.

### Background Subtraction

`Background subtraction` is the removal of dynamic elements from a static
background image. In this example we have a fixed-camera video of cars
driving along a highway. We wish to isolate a single clear image of the
background.

Five segmentation algorithms are explored:

    1. KadewTraKuPong and Bowden segmentation mask
    2. Gaussian Mixture segmentation by Zoran Zuvkovic
    3. Godbeher, Matsukawa, and Goldberg
    4. Counting by Sagi Zeevi
    5. KNN Nearest Neighbors (best)

<p align="center">
  <img src="figures/Background_subtraction_2.PNG">
</p>

File [005_background_subtraction.py](005_background_subtraction.py)

### Interactive Perspective Fix

OpenCV app to recalculate perspective based on user inputs.

An image is loaded and displayed, and a `mouse_callback` event is
tracked to evaluate the coordinates of the corners. Once four corners
are selected they are passed to the `cv2.getPerspectiveTransform`
function and the images perspective is fixed. Finally, both the
original image and new image are displayed side by side.

<p align="center">
  <img width="350" height="163" src="figures/004_img_interactive_perspective_fix.PNG">
</p>
<p align="center">
  <img src="figures/Camera_to_scanned_perspective.png">
</p>

File [004_img_interactive_perspective.py](004_img_interactive_perspective.py)

### Inception NN Object Detection

Deep learning models trained on the `ImageNet` database
are loaded into Caffe and used to classify images in a video stream.

Classification function for the neural network works as follows:

        1. Gets frame from video,
        2. Transform them into tensors,
        3. Forward feed into neural network,
        4. Selects the highest probability out of five categories,
        5. Add prediction to frame.

<p align="center">
  <img src="figures/Realtime_object_detection_RESNET.PNG">
</p>
<p></p>

Other neural nets can be loaded from the `cv2.dnn.readNetFromCaffe` function.

```

resnet_cafferesnet_  = cv2.dnn.readNetFromCaffe('../data/resnet_50.prototxt',
                                           '../data/resnet_50.caffemodel')

mean = np.load('../data/resnet_50_mean.npy')
classify('../data/shuttle.mp4', resnet_caffe, 'data', 'prob', mean, class_names)
```


File [notebooks/DL_googlenet_inception_caffe.ipynb](notebooks/DL_googlenet_inception_caffe.ipynb)


### OpenCV Panorama

