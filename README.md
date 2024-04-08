# 3D Reconstruction from Stereo Pair

<img src="3d_visualization_of_image_points.jpg" alt="3d_visualization_of_image_points" width="200"/>

The objective of this program was to use an experimental methd to perform a 3D reconstruction from a stereo pair of images with known camera calibration parameters.

Another goal was to limit the use of libraries, with only OpenCV being used for basic computer vision functions.

The input left and right images are shown below:

<p float="left">
  <img src="imL.jpg" width="400" />
  <img src="imR.jpg" width="400" /> 
</p>


## Step 1: Compute initial transform
A homography matrix to roughly transform from the left to the right image was computed. This was done using SIFT detect features, FLANN to match them.

## Step 2: Feature matching
A tighly-spaced grid of overlapping feature templates was created on the left image. Smooth featureless surfaces were ignored. Next, the homography matrix was used roughly transform the template locations onto the right image. These locations were used to determine a search area in the right image for the template. The arrows in the figure below show where each feature was detected and where the search area was centered. The objects closer to the camera have the longest disparity as shown by the arrows.

![searches_plot](searches_plot.png)

## Step 3: Compute disparities and depth map
The disparitiy between each point's location in the two images was computed. The disparities were used to create a depth map as shown below.

![depth_map](depth_map.png)

The points were also colorized and plotted in 3d.

![3d_visualization_of_image_points](3d_visualization_of_image_points.png)

## Step 4: Convert image to projected coordinates
Finally, the points in image coordinates were converted to projected coordinates. The result is shown in the two figures below.

![front_view_out_point_cloud](front_view_out_point_cloud.png)

![3d_visualization_of_projected_points](3d_visualization_of_projected_points.png)