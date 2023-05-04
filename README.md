Download Link: https://assignmentchef.com/product/solved-csci5980-assignment4-fundermental-matrix
<br>
<h1>1             VLFeat Installation</h1>

One of key skills to learn in computer vision is the ability to use other open source code, which allow you not to re-invent the wheel. We will use VLFeat by A. Vedaldi and B. Fulkerson (2008) for SIFT extraction given your images. Install VLFeat from following:

<a href="http://www.vlfeat.org/install-matlab.html">http://www.vlfeat.org/install-matlab.html</a>

Run vl demo sift basic to double check the installation is completed.

(NOTE) You will use this library only for SIFT feature extraction and its visualization. All following visualizations and algorithms must be done by your code.

<h1>2             SIFT Feature Extraction</h1>

Figure 1: Given your two cellphone images (left and right), you will extract SIFT descriptors and visualize them using VLFeat.

You will extract David Lowe’s SIFT (Scale Invariant Feature Transform) features from your cellphone images as shown in Figure 1. First, take a pair of pictures with your calibrated camera (intrinsic parameter, <strong>K</strong>, and radial distortion parameter, <em>k</em>, are precalibrated.) as follow:

<ol>

 <li>Take the first picture and another one after moving one step right (1m).</li>

 <li>Common 3D objects across different depths, e,g., buildings, ground plane, and tree, appear in both images.</li>

 <li>Two images have to be similar enough so that the appearance based image matching can be applied, i.e., SIFT feature does not break, while maintaining the baseline between cameras (at least 1 m), i.e., similar camera orientation and sufficient translation.</li>

 <li>Avoid a 3D scene dominated by one planar surface, e.g., looking at ground plane.</li>

</ol>

<strong>Write-up:</strong>

(SIFT visualization) Use VLFeat to visualize SIFT features with scale and orientation as shown in Figure 1. You may want to plot up to 500 feature points. You may want to follow the following tutorial:

<a href="http://www.vlfeat.org/overview/sift.html">http://www.vlfeat.org/overview/sift.html</a>

<h1>3             SIFT Feature Matching</h1>

Figure 2: You will match points between I<sub>1 </sub>and I<sub>2 </sub>using SIFT features.

(NOTE) From this point, you cannot use any function provided by VLFeat.

The SIFT is composed of scale, orientation, and 128 dimensional local feature descriptor (integer), <strong>f </strong>∈ Z<sup>128</sup>. You will use the SIFT features to match between two images, I<sub>1 </sub>and I<sub>2</sub>.

<strong>Write-up:</strong>

<ul>

 <li>(Nearest neighbor search) Let two sets of features be {<strong>f</strong><sub>1</sub><em>,</em>·· <em>,</em><strong>f</strong><em><sub>N</sub></em><sub>1</sub>} from I<sub>1 </sub>and {<strong>g</strong><sub>1</sub><em>,</em>··· <em>,</em><strong>g</strong><em><sub>N</sub></em><sub>2</sub>} from I<sub>2 </sub>where <em>N</em><sub>1 </sub>and <em>N</em><sub>2 </sub>are the number of features in image 1 and 2, respectively. Compute nearest neighbor per feature and visualize ({<strong>f</strong><sub>1</sub><em>,</em>··· <em>,</em><strong>f</strong><em><sub>N</sub></em><sub>1</sub>} → {<strong>g</strong><sub>1</sub><em>,</em>··· <em>,</em><strong>g</strong><em><sub>N</sub></em><sub>2</sub>} and {<strong>g</strong><sub>1</sub><em>,</em>··· <em>,</em><strong>g</strong><em><sub>N</sub></em><sub>2</sub>} → {<strong>f</strong><sub>1</sub><em>,</em>··· <em>,</em><strong>f</strong><em><sub>N</sub></em><sub>1</sub>}) as shown in Figure 2(a) and Figure 2(b). Note that the distance between two features is defined as <em>d </em>= k<strong>f </strong>− <strong>g</strong>k. You may use knnsearch function in MATLAB.</li>

 <li>(Ratio test) Filter out matches using the ratio test, i.e., keep the match if <em>d<sub>ij</sub></em><sub>1</sub><em>/d<sub>ij</sub></em><sub>2 </sub><em>&lt; </em>0<em>.</em>7 and discard otherwise, where <em>d<sub>ij</sub></em><sub>1 </sub>and <em>d<sub>ij</sub></em><sub>2 </sub>are the first and second nearest neighbors for the <em>i</em><sup>th </sup>feature, respectively. Visualize the matches after the ratio test as shown Figure 2(d) and Figure 2(c).</li>

 <li>(Bidirectional match) Visualize bidirectionally consistent matches as shown Figure 2(e). Compare the number of matches from (1) to (3).</li>

</ul>

<h1>4             Fundamental matrix</h1>

Figure 3: You will visualize epipole and epipolar lines for each image.

Compute a fundamental matrix between I<sub>1 </sub>and I<sub>2</sub>.

<strong>Write-up:</strong>

(1) (Fundamental matrix) Complete the following function to compute a fundamental matrix, linearly:

<strong>F </strong>= ComputeFundamentalMatrix(<strong>u</strong>, <strong>v</strong>)

Input: <strong>u </strong>and <strong>v </strong>are <em>N<sub>f </sub></em>×2 matrices of 2D correspondences where the <em>N<sub>f </sub></em>is the number of 2D correspondences, <strong>u </strong>&#x2194; <strong>v</strong>.

Output: <strong>F </strong>∈ R<sup>3×3 </sup>is a rank 2 fundamental matrix.

(2) (Epipole and epipolar line) Pick 8 random correspondences, <strong>u</strong><em><sub>r </sub></em>&#x2194; <strong>v</strong><em><sub>r</sub></em>, compute the fundamental matrix, <strong>F</strong><em><sub>r </sub></em>and visualize epipole and epipolar lines for the rest of feature points in both images as shown in Figure 3. Pick different sets of correspondences and visualize different epipolar lines.

<h1>5             Robust Fundamental Matrix Estimation</h1>

Estimate the fundamental matrix using RANSAC.

<strong>Write-up:</strong>

(1) (RANSAC with fundamental matrix) Write a RANSAC algorithm for the fundamental matrix estimation given <em>N </em>matches from Section 4 using the following pseudo code:

<strong>Algorithm 1 </strong>GetInliersRANSAC

1: <em>n </em>← 0

2: <strong>for </strong><em>i </em>= 1 : <em>M </em><strong>do</strong>

3:              Choose 8 correspondences, <strong>u</strong><em><sub>r </sub></em>and <strong>v</strong><em><sub>r</sub></em>, randomly from <strong>u </strong>and <strong>v</strong>.

4:                     <strong>F</strong><em><sub>r </sub></em>= ComputeFundamentalMatrix(<strong>u</strong><em><sub>r</sub></em>, <strong>v</strong><em><sub>r</sub></em>)

5:               Compute the number of inliers, <em>n<sub>r</sub></em>, with respect to F.

6:                <strong>if </strong><em>n<sub>r </sub>&gt; n </em><strong>then</strong>

7:          <em>n </em>← <em>n<sub>r </sub></em>8:              <strong>F </strong>= <strong>F</strong><em><sub>r</sub></em>

9:              <strong>end if</strong>

10: <strong>end for</strong>

<ul>

 <li>(Epipole and epipolar line) Using the fundamental matrix, visualize epipole and epipolar lines.</li>

</ul>

-0.6       -0.4       -0.2         0         0.2        0.4       0.6        0.8          1         1.2

Figure 4: Four configurations of camera pose from a fundamental matrix.

<ul>

 <li>(Camera pose estimation) Compute 4 configurations of relative camera poses:</li>

</ul>

[R1 C1 R2 C2 R3 C3 R4 C4] = CameraPose(<strong>F</strong>, <strong>K</strong>)

Input: <strong>F </strong>is the fundamental matrix and <strong>K </strong>is the intrinsic parameter.

Output: R1 C1 ··· R4 C4 are rotation and camera center (represented in the world coordinate system).

<ul>

 <li>Visualize the 4 configuration in 3D as shown in Figure 4.</li>

</ul>

<h1>6             Triangulation</h1>

Given four configurations of relative camera pose, you will find the best camera pose by verifying through 3D point triangulation.

<strong>Write-up:</strong>

(1) (Linear triangulation) Write a code that computes the 3D point given the correspondence, <strong>u </strong>&#x2194; <strong>v</strong>, and two camera projection matrices:

[<strong>X</strong>] = LinearTriangulation(<strong>P</strong><sub>1</sub>,<strong>u</strong>,<strong>P</strong><sub>2</sub>,<strong>v</strong>)

Input: <strong>P</strong><sub>1</sub><em>,</em><strong>P</strong><sub>2 </sub>∈ R<sup>3×4 </sup>are two camera projection matrices, and <strong>u </strong>&#x2194; <strong>v </strong>∈ R<sup>2 </sup>are their 2D correspondence.

Output: <strong>X </strong>∈ R<sup>3 </sup>is the triangulated 3D point.

<em>Hint: </em>Use the triangulation method by linear solve, i.e.,

<ul>

 <li>(Cheirality) Write a code that computes the number of 3D points in front of two cameras. The condition of a 3D point being in front of camera is called <em>cheirality</em>: idx = CheckCheirality(<strong>Y</strong>,<strong>C</strong><sub>1</sub>,<strong>R</strong><sub>1</sub>,<strong>C</strong><sub>2</sub>,<strong>R</strong><sub>2</sub>)</li>

</ul>

Input: <strong>Y </strong>is a <em>n </em>× 3 matrix that includes <em>n </em>3D points, and <strong>C</strong><sub>1</sub>,<strong>R</strong><sub>1</sub>/<strong>C</strong><sub>2</sub>,<strong>R</strong><sub>2 </sub>are the first and second camera poses (camera center and rotation).

Output: idx is a set of indices of 3D points that satisfy cheirality.

<em>Hint: </em>the point must satisfy <strong>r</strong><sub>3</sub>(<strong>X </strong>− <strong>C</strong>) <em>&gt; </em>0 where <strong>r</strong><sub>3 </sub>is the 3rd row of the rotation matrix (z-axis of the camera), <strong>C </strong>is the camera position and <strong>X </strong>is the 3D point.

<ul>

 <li>(Camera pose disambiguation) Based on cheirality, find the correct camera pose.</li>

</ul>

Visualize 3D camera pose and 3D points together as shown in Figure 5. <em>Hint: </em>Use plot3 and DisplayCamera.m to visualize them.

Figure 5: You will visualize four camera pose configurations with point cloud.

<ul>

 <li>(Reprojection) Project 3D points to each camera and visualize reprojection, <strong>u </strong>and b</li>

</ul>

measurement, <strong>u </strong>onto the image as shown in Figure 6, i.e.,

<strong> KR</strong> <strong>I </strong>

where <strong>X </strong>is the reconstructed point.

Figure 6: Visualization of measurements and reprojection.