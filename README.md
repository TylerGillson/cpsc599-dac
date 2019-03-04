# cpsc599-dac
## Overview
DAC is an Android app that is currently being developed by Morshed ul Islam for the purpose of his PHD thesis. It utilizes behavioural 2nd factor authentication technology in order to verify the identities of its users. Its primary advantage over other 2nd factor authentication systems is that behaviour, unlike phone numbers, is non-transferable and therefore ensures that users are unable to delegate access to their information.

Users begin by creating a profile, which is accomplished by completing 10 registration rounds. Each round consists of two phases. In the first phase, users trace three circles which are visible on the screen throughout the tracing process. In the second phase, a circle is flashed on the screen for 3 seconds and the user traces where they think it was after it has disappeared.

Upon completion of the registration rounds, a matrix consisting of 40 vectors (each of which represents a single circle and contains 65 elements) is stored on a server - becoming the 'profile' for that particular user. Users authenticate themselves via 5 verification rounds, which are conducted identically to the registration rounds. The 20x65 verification matrix is then compared to the 40x65 registration matrix using a generalized k-NN Divergence Estimator with pre-defined thresholds in order to decide profile matches.

## Notes on the Data
Each time a circle is drawn by a user, speed, error, pressure, event size, and orientation data are collected at 10 different points around its circumference. Therefore, 60 out of 65 of the features for each circle vector belong to one of the following feature groups:
- Error relative to the ideal circle at each point
- X component of speed at each point
- Y component of speed at each point
- Pressure at each point 
- Event size at each point (contact surface area of finger)
- Orientation in x, y, and z axes (represented as a single value) at each point 

And the last five features are not point-specific:
- eStart: deviation of initial contact point from the nearest point on the ideal circle
- eCenter: deviation of the drawn circle's centroid relative to the ideal circle's centroid
- eRadius: difference in radii between drawn & ideal circles
- direction: 1 for clockwise, -1 for anti-clockwise
- timediff: time taken to begin drawing the circle after being prompted by the app

<strong>A Note on Units:</strong> All errors and were recorded in pixels, all speeds in pixels per second, orientation in degrees (X: -180 to 180, Y: -90 to 90, Z: 0 to 360), and times in seconds. Pressures and event sizes were recorded as real values in the range (0,1). All direction values were either -1 or 1, as stated above.

## Draw A Circle (DAC) 1.1.ipynb
Contains all the data munging and preliminary analysis used to derive my research questions.

## Draw A Circle (DAC) 1.2.ipynb
Contains all data analysis and visualizations pertaining to answering the research questions.
