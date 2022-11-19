1] Feature Detection And Matching

a) Here we create an ORB feature detector, to generate max keypoints(10000) find keypoints and descriptors in the given image. The SIFT feature detector is not used because it can be patented in future and they may break the code.

b) Then, we use a Brute Force/ FLANN based matcher to find the best matches in the keypoints between 2 input images based on hamming distance.

c) Finally, the matches are sorted based on distance and 30 best matches are selected from the total matches.

d) To fill the final list of feature points, points are extracted from the matches and the matches are plotted simultaneously on both images to visualize them.

2] Calculating Fundamental matric using RANSAC

a) Here we calculate the Fundamental matrix using the least squares method. We have 8 equations and we input exactly 8 points to form the A matrix from them.

b) Here, the RANSAC algorithm is applied to choose the best F matrix. 8 random points are sampled and fed into the calculate_F_matrix function iteratively and we calculate the error in estimating the points. Comparing this with a predefined threshold, we can classify the inlier points and choose the Best F matrix based on the max_inliers criteria.

3] Calculate the Essesntial Matrix Here, the Essential matrix is calculated using the Fundamental matrix and the intrinsic camera parameters.

4] Camera Pose Estimation

a) The extract_camera_pose function is used to extract the 4 camera pose solutions form the E matrix by calculating the svd of the E matrix as U Σ VT:

b) The disambiguate_camerapose function is used to shortlist the best camera pose based on the triangulation check for the chirelity condition.
