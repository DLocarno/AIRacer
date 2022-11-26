Original work Copyright (c) 2021 David Locarno

# GAME DESCRIPTION

AI RACER started as a simple 2D racing game built in the Pygame framework. A player can easily add/modify game levels and race a number of NPCs around a track.  
Later, Deep-Q Reinforcment Learning via the PyTorch framework, was added to the game to allow a player to test, tune, train, and play with a Deep Q Learning Network.

# PURPOSE

Learning about both simple game designs and the practical application of a Deep Reinforcement Learning Algorithm. 
Unlike the majority of pre-constructed game environments (such as those available in openai/gym) which abstract 
critical aspects of Deep Q Learning from the user, this program is stand-alone.  Other than using Pytorch to 
create the neural network, the game's custom AiAgent performs the observations of its environmenet and reward
calculations, therefore, the user gets a more complete "grasp" of implementing a Deep Reinforcement Algorithm.

# GETTING STARTED

## Quick Installtion Guide (for Windows OS):
1. Verify Python3 and Python Package Installer (pip) are both installed on your system.

* To check installed Python version, opend cmd prompt and enter:
	* python - V
* Or, to install Python, download at: 
	* https://www.python.org/downloads/
* If pip is not installed, open cmd prompt and install pip on windows with:
	* curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py 
	* python get-pip.py
* Or, to update to the newest version of pip, enter:
	* python -m pip install --upgrade pip

2. Move into programs main folder and run the install.py script to install all modules and dependencies:
* Open a cmd prompt and enter:
	cd [/path/to/game]
	install.bat

3. Run the game:
* After successful install, open cmd prompts & enter:
	python main.py

## Complete list of dependencies and Package Requirements (these should install automatically via install.py script):
Python3 (ver 3.9.4 was used)
pygame  (ver 2.0.1 was used)
math
random
os
sys
time
scipy
numpy
pytorch
pickle
copy

Optional Modules (install is required to enable use of the game's development tools):
pillow
tkinter (ver 8.6)
 
Notes:
*To see a list of all Python modules currently installed:
	* Open a command prompt and enter: idle
	* In the idle shell, type: help("modules")

* If program fails to locate dependencies after all modules are installed:
	* Ensure the full file path of every folder/directory which contains the neccessary modules are added to the PATH environmental variable

* If program fails to run due to PyTorch dependency issue:
	* Ensure the correct package install command was used for your specific system OS and platform.
	* To verify which install command to use, go to:
	* https://pytorch.org/get-started/locally/

## Hardware & System Requirements:

The minimum hardware requirements for this game have not been determined.  
But, it was developed, tested, and ran successfully on the following:
OS:	Microsoft Windows 10, 64-bit
CPU:	Intel Core i7-9700k, 3.6GHz
GPU:	NVDIA GeForce RTX 2080 Super
Memory:	32 GB RAM

## Final notes on game performance:

Training a Deep Q Neural Network is inherently computationally expensive.  The  source code will attempt to perform these computations on the devices GPU via use of the PyTorch framework.
If a GPU is not available, the CPU is then selected as the device. How quickly the DQN trains will be dependent on the performance of the underlying hardware performing the backpropegation calculations.

It was observed that game levels created over a certian size would significantly reduce performance during play. If attempts are made to make a new level (racetrack) for the game, care must be taken to limit the maximum size (pixels) of the level image.  
Additionally, attempting to render a level with too much detail or number of colors could also impact perfomance to the point of making the game unplayable.

# OTHER NOTEWORTHY DIRECTORIES, FEATURES, & TOOLS
1. The /game/race/levels/ directory contains each of the game's levels and associated level configuration files.
	* These configuration files (for example, track_1_init_data.txt) contain critical information required to load each level.
	* The user can change the configuration data to adjust how the level is loaded, but, must take care to maintain the syntax and order.
	* Alternatively, new init files may be generated with an associated level image (.png) file to create new levels.
	* Note: If you elect to create a new level, be aware that the image size and color detail will impact overall performance.
2. The /game/race/levels/ directory also contains a script module 'image_plotter_tool.py'
	* This is used to easily create and append any NPC way-points which may need to be generated for a new level image file
	* This waypoint data is then parsed by the NPCs which enables their psuedo-random control to navigate the level
	* To use the tool, open a cmd prompt, cd to the directory and enter: python image_plotter_tool.py [level_image_file.png]
	* The Tkinter GUI tool will open a thumbnail of the image and allow you to generate waypoints by simply using the left and right mouseclick
	* When you are satisfied with waypoint generation for the level, press 'Enter' and it will write them to a file in the levels folder
	* Open the file and copy/paste the waypoints into the level's corresponding track_#_init_data.txt file at the end
3. The /game/race/car_sprite_images/ directory contains a script module '_sprite_generator.py'
	* This is needed if its desired to add a new car sprite .png file to the game (such as a new color car)
	* The script takes a single .png file and rotates it 360 deg, creating a new image file at each orientation which are required by the program
	* To use the tool, open a cmd prompt, cd to the directory and enter: python _sprite_generator.py [car_sprite_image_file.png]
4. The /game/race/dqn_model_data directory contains both the current DQN's state and wieght values and the AI Agent's replay memory state.
	* If the data stored in this directory is deleted, the AiAgent will initialize a 'new' neural network in its place.
	* The new network will require the Agent to perform new training on the network.
	* After a network is successfully trained, 'training mode' can be switched OFF at the game's Title sequence, but, the player can still be controlled.