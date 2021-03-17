
<b>Robotic Mapping: A Survey</b>

<b>Author</b> : Sebastian Thrun February 2002 CMU-CS-02-111 

<b>Reviewed by</b> : Samrat Pravin Patel

<i><b>Index</b></i>

&#8226; Broad Area Overview

&#8226; Problem Description

&#8226; Solution

&#8226; Comments

&#8226; Future insight and further work

<b>Broad Area Overview</b>

This paper gives one a comprehensive idea of robot mapping algorithms especially focusing on the indoor environment. Most of these algorithms are probabilistic and incremental so they can be run in real time whereas others require multiple passes through the data and added processing. There are some which require the actual pose and some used the odometry measurements for positioning, also some are capable of handling correspondence between data recorded at a different point in time whereas others require features to carry signatures that make the data points that are uniquely identifiable.

<b>Problem Description</b>

Robotic mapping research has a long history. Since the 1980s and early 1990s, the field of mapping has been widely divided into metric and topological approaches.Metric maps capture the geometric properties of the environment, whereas topological maps describe the connectivity of different places via arcs.  The distinction between the metric and topological approach is very fuzzy. In general one can say that the metric maps are finer grained than the topological maps hence one can say that  higher resolution comes at the cost of computational processing which are based on the data gathered through sensors which are difficult to build and to difficult to extrapolate from the individual measurements to the measurements of nearby unexplored locations especially when they look alike its very difficult for robot to differentiate due to lack of geometry in measurement space or some sort of a reference.

Different sensors generate measurementurement errors which are commonly termed as noise which is subject to the present environment in which the robot is operating . The sensor mismeasurement or the noise can also be due to the limitations due to the environment or due to the limited capabilities of the sensor.

Ther robotic mapping errors are statistically dependent as the errors accumulate overtime and affect the way future sensor measurements are interpreted. Accommodating the systemic errors is the key to successful robotic mapping. The errors in mapping can be also due to the higher dimensionality of the mapping space or the environment in which the robot is operating . Naturally higher the number of errors over time for a larger space will result in higher statistical error in dimensionality mapping.

Another problem with the robotic mapping measurement is the correspondence problem. Robot has to process enough numbers of points where it has to match the points with the data of the same location during different times. It can happen due to the change in the mapping environment overtime which can lead to the discrepancy in the data and ultimately lead to the accumulation error which may affect the accuracy and behaviour of the robot for that particular environment. Ultimately for the robot to navigate autonomously it must be able to deal with a dynamic environment and generate a real time map so for this reason robotic exploration poses a big challenge. Robotic mapping is largely considered most difficult perpetual problem in robotics

<b>Solution</b></i>

Majority of robot mapping algorithms employ a probabilistic approach due to the fact that robotic mapping is characterized by my uncertainty and sensor noise. Probability is often referred to as a perceptual model in robotics since it describes how sensor measurements are generated for different poses and maps. Probabilistic approach has standardized the solution for the perceptual inference solution  for uncertainty using Bayes Filter which is related to Kalman Filter and hidden Markov models which simplifies the approach for probabilistic inference where both map and robot pose have to be estimated together.

<b>Comments</b>

Below section summarizes various robotic mapping approaches approaches  along with key advantages and limitations

<b>Kalman filter :</b>

In Kalman filter approach mapping relies on 3 assumptions
Next State function must be linear with added Gaussian Noise 
Characteristics must apply to perceptual model
Initial uncertainty must be gaussian 

<b>Advantages</b>

Advantage of the Kalman filter approach is that it estimates the full posterior over maps in real time fashion which is helpful during encountering uncertainty  when using maps for the navigation purpose.

<b>Limitations</b> 
The most important limitation of Kalman filter approach lies in the Gaussian Noise assumption particularly that the measurement noise must be independent of the Gaussian noise. Kalman filter is unable to cope up with the correspondence problem which is the problem of associating measurement with the ambiguous features on the map. Kalam filter requires a sparse set of distinctive features either from the sensor measurements or from the location. There can be problems with respect to maximum likelihood data association like in a variant of Kalman Filter algorithm called as Lu/Milos Algorithm ,  in which the algorithm simply pairs with the nearby measurements for building maps from raw data from unknown correspondence which is done by guessing technique over fully calculating correspondence and the map which again imposes limitations especially when errors are large for example where the environment is cyclic which may ultimately lead to the failure of the maximum likelihood correspondence and ultimately lead to the wrong map when using the Kalman Filter.


<b>Expectation Maximization Algorithm:</b>

It's an alternative to Kalman Filter technique developed in context to Maximum Likelihood estimation of latent variables . It constitutes one of the best solutions for the problem of correspondence mapping. 

<b>Advantages</b>

Performs better in an environment where it is required to generate large scale cyclic maps even if the features do not look alike and cannot be distinguished perceptually. Solves the correspondence problem by repeatedly localizing the robot relative to the present map.

<b>Limitations</b> 

EM algorithm does not retain full notion of uncertainty and cannot create incremental map as seem in Kalman Filter approaches


<b>Hybrid Approach</b> 

It is an alternative approach for real time mapping where in basic idea is to incrementally build a single mao as sensor data arrives but without keeping the track of any residual uncertainty hence which simplifies the process of mapping to a very large extent

<b>Advantages</b> 

Hybrid approach overcomes various limitations of its predecessor by maintaining an explicit notion of uncertainty during mapping short of the full posterior over maps and poses maintained by Kalman filter. The idea is that by retaining the notion of the robot’s pose uncertainty conflits like one faced by the incremental maximum likelihood method can be identified and corrective measures can be taken. But unlike the incremental maximum likelihood method it also has the ability to correct its map backward in time wherever an inconsistency is detected.
Hybrid approach works better in a multi robot environment for mapping. Even though it's not a real time mapping algorithm , however practical implementations appear to work well in real time when used in offices or building types of environment

<b>Limitations</b> 

Rollback  to the earlier map can be catastrophic failure. Moreover the approach cannot cope with complex ambiguities such as uncertainties that arise when robot traverses multiple posted cycles. Hybrid approach strictly speaking is not a real time algorithm as the time it takes to correct the loop depends on the complexity and size of the loop.


<b>Occupancy Grid Maps :</b> 

Central problems addressed by occupancy grid mapping and related algorithms in the problem of generating consistent metric maps from noisy or incomplete sensor data.Even if the robot poses are known it is sometimes difficult to say whether a place in the environment is occupied or not due to ambiguities in sensor data. Hence the occupancy grid map resolves such ambiguities by generating probabilistic maps represented by grids in two dimensions. The Bayes filter is used to calculate the posterior over the occupancy over the grid cells.

<b>Advantages</b> 

Extremely robust and easy to implement. Sensor measurement Errors can be discarded until the robot comes in motion 

<b>Limitations</b> 

Lack of method for pose uncertainty. The other disadvantage is that the Bayes filter assumes independent noise, the sensor noise is strongly correlated hence can lead to erroneous maps especially when the robot is not in motion. Independent assumption of multiple grid cells by the Bayes filter , while convenient can lead to the erroneous maps

<b>Object Maps :</b> 

Basic maps of objects consisting of geometric shapes and sizes using lines, walls and so on. The object map overcomes the limitations of the occupancy grid which requires measuring  grid cells multiple times for integrating into Bayes filter by assuming that part of the environment consists of large flat surfaces. This assumption is highly helpful in corridor-like environments.

<b>Advantages</b> 

More compact than the occupancy grid maps especially if the environment is structured. Highly accurate. Efficient in dynamic environments applications. Can be mixed and matched with other mapping algorithms and techniques such as EM Algorithms or Hybrid Maps algorithm for maximum advantage for robot operations. #D Models of map generated from sensor data are much more smoother and accurate up to 95%


<b>Future insight and further work</b> 

The major goal was to survey various algorithms which include Kalman filter techniques which employ probabilistic approach for robotic mapping and emphasis was placed on relating each technique to each other to point out relative strengths and weaknesses as covered in the earlier sections. The paper does not focus on techniques that can be applied in dynamic scenarios where the environment constantly changes.
The main area of future research would be to develop a lifelong mapping robot that is capable of updating its maps over its lifetime which will be able to incorporate sensor fusion and utilizing data acquired from various sources for applications in explorations for extreme unstructured  earth and space environments. 

The paper has placed less emphasis on multi robot systems due to the problem of overlapping of the maps from various robots for locally acquired maps may be unknown. Finally none of the approach reviewed in the article address the issue of robot control

With the advent of the VTOLs and UAV drones for applications in transportation this paper has not covered the class of new emerging technologies which have potential for changing the future of mankind. 

<b>Recent Papers</b> 

&#8226;Cappel, H. F. (2021). A Hierarchical Multi-Robot Mapping Architecture Subject to Communication Constraints. arXiv preprint arXiv:2102.01641.

&#8226;Housein, A. A., & Xingyu, G. (2021, March). Simultaneous Localization and Mapping using differential drive mobile robot under ROS. In Journal of Physics: Conference Series (Vol. 1820, No. 1, p. 012015). IOP Publishing

&#8226;Shamsfakhr, F., Motroni, A., Palopoli, L., Buffi, A., Nepa, P., & Fontanelli, D. (2021). Robot Localisation Using UHF-RFID Tags: A Kalman Smoother Approach. Sensors, 21(3), 717.

&#8226;Panigrahi, P. K., & Bisoy, S. K. (2021). Localization Strategies for Autonomous Mobile Robots: A review. Journal of King Saud University-Computer and Information Sciences.
