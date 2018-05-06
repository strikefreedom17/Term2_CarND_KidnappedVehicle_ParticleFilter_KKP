[image1]: ParticleFilter_Pass.png
[image2]: ParticleFilter_Running.png

# Kidnapped Vehicle Project Overview
This repository contains all the code for the Vehicle Localization by applying Particle Filter technique. The main script that describes the particle filter algorithm is 'particle_filter.cpp' located in the 'src' folder. In order to pass the rubric criteria, the algorithm must be run successfully witin specified time of 100 seconds. The main script includes following functions (in C++):

1. "init": Initialize particle position (x,y) and heading (theta),

2. "prediction": Predict the vehicle position and heading using kinematics equation of motion,

3. "dataAssociation": Find the predicted measurement that is closest to each observed measurement and assign the observed measurement to this particular landmark,

4. "updateWeights": Update the weights of each particle using a mult-variate Gaussian distribution,

5. "resampple": Resample particles with replacement with probability proportional to their weight,

6. "SetAssociations": reset particle information (associations, sense_x, sense_y), and

7. "getAssociations", "getSenseX", "getSenseY"

If the particle filter algorithm is successfully implemented, the simulation result displays as follows:
![image1_name][image1] 


## Project Introduction
The robot has been kidnapped and transported to a new location! Luckily it has a map of this location, a (noisy) GPS estimate of its initial location, and lots of (noisy) sensor and control data.

In this project, a 2 dimensional particle filter algorithm is implemented in C++. The particle filter will be given a map and some initial localization information (analogous to what a GPS would provide). At each time step your filter will also get observation and control data. 

## Running the Code
This project involves the Term 2 Simulator which can be downloaded [here](https://github.com/udacity/self-driving-car-sim/releases)

This repository includes two files that can be used to set up and intall uWebSocketIO for either Linux or Mac systems. For windows you can use either Docker, VMware, or even Windows 10 Bash on Ubuntu to install uWebSocketIO.

Once the install for uWebSocketIO is complete, the main program can be built and ran by doing the following from the project top directory.

1. mkdir build
2. cd build
3. cmake ..
4. make

Here is the main protcol that main.cpp uses for uWebSocketIO in communicating with the simulator.

INPUT: values provided by the simulator to the c++ program

// sense noisy position data from the simulator

["sense_x"] 

["sense_y"] 

["sense_theta"] 

// get the previous velocity and yaw rate to predict the particle's transitioned state

["previous_velocity"]

["previous_yawrate"]

// receive noisy observation data from the simulator, in a respective list of x/y values

["sense_observations_x"] 

["sense_observations_y"] 


OUTPUT: values provided by the c++ program to the simulator

// best particle values used for calculating the error evaluation

["best_particle_x"]

["best_particle_y"]

["best_particle_theta"] 

//Optional message data used for debugging particle's sensing and associations

// for respective (x,y) sensed positions ID label 

["best_particle_associations"]

// for respective (x,y) sensed positions

["best_particle_sense_x"] <= list of sensed x positions

["best_particle_sense_y"] <= list of sensed y positions


The main task in this project is to build out the methods in `particle_filter.cpp` until the simulator output says:

```
Success! Your particle filter passed!
```

# Implementing the Particle Filter
The directory structure of this repository is as follows:

```
root
|   build.sh
|   clean.sh
|   CMakeLists.txt
|   README.md
|   run.sh
|
|___data
|   |   
|   |   map_data.txt
|   
|   
|___src
    |   helper_functions.h
    |   main.cpp
    |   map.h
    |   particle_filter.cpp
    |   particle_filter.h
```

The main file needed to be modified is `particle_filter.cpp` in the `src` directory. The file contains the scaffolding of a `ParticleFilter` class and some associated methods. Read through the code, the comments, and the header file `particle_filter.h` to get a sense for what this code is expected to do.

The `src/main.cpp` file contains the code that will actually be running your particle filter and calling the associated methods.

## Inputs to the Particle Filter
The inputs to the particle filter in the `data` directory. 

#### The Map*
`map_data.txt` includes the position of landmarks (in meters) on an arbitrary Cartesian coordinate system. Each row has three columns
1. x position
2. y position
3. landmark id

### All other data the simulator provides, such as observations and controls.

> * Map data provided by 3D Mapping Solutions GmbH.


