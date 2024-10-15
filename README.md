# Mujoco and Mujoco-py Installation Instructions for Ubuntu 22

### Steps
1. Install Anaconda. Download it from this [link](https://repo.anaconda.com/archive/Anaconda3-2021.11-Linux-x86_64.sh).
```
cd Downloads/
sudo chmod +x Anaconda3-2021.11-Linux-x86_64.sh
./Anaconda3-2021.11-Linux-x86_64.sh
```

2. Install git.
```
sudo apt install git
```

3. Install the Mujoco library.

    * Download the Mujoco library from this [link](https://mujoco.org/download/mujoco210-linux-x86_64.tar.gz).
    * Create a hidden folder :
    ```
    mkdir /home/user-name/.mujoco
    ```
    * Extract the library to the .mujoco folder.
    ```
    tar -xvf mujoco210-linux-x86_64.tar.gz -C ~/.mujoco/
    ```
    * Include these lines in .bashrc file.
    ```
    # Replace user-name with your username
    echo -e 'export LD_LIBRARY_PATH=/home/user-name/.mujoco/mujoco210/bin 
    export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/lib/nvidia 
    export PATH="$LD_LIBRARY_PATH:$PATH" 
    export LD_PRELOAD=/usr/lib/x86_64-linux-gnu/libGLEW.so' >> ~/.bashrc
    ```
    * Source bashrc.
    ```
    source ~/.bashrc
    ```
    * Test that the library is installed.
    ```
    cd ~/.mujoco/mujoco210/bin
    ./simulate ../model/humanoid.xml
    ```

4. Install mujoco-py.
```
conda create --name mujoco_py python=3.8
conda activate mujoco_py
sudo apt update
sudo apt-get install patchelf
sudo apt-get install python3-dev build-essential libssl-dev libffi-dev libxml2-dev  
sudo apt-get install libxslt1-dev zlib1g-dev libglew1.5 libglew-dev python3-pip

# Clone mujoco-py.
cd ~/.mujoco
git clone https://github.com/openai/mujoco-py
cd mujoco-py
pip install -r requirements.txt
pip install -r requirements.dev.txt
pip3 install -e . --no-cache
```
5. Reboot your machine.
```
sudo reboot
```
6. After reboot, run these commands to install additional packages.
```
conda activate mujoco_py
sudo apt install libosmesa6-dev libgl1-mesa-glx libglfw3
sudo ln -s /usr/lib/x86_64-linux-gnu/libGL.so.1 /usr/lib/x86_64-linux-gnu/libGL.so
# If you get an error like: "ln: failed to create symbolic link '/usr/lib/x86_64-linux-gnu/libGL.so': File exists", it's okay to proceed
pip3 install -U 'mujoco-py<2.2,>=2.1'
pip install "cython<3"
```
7. Check if mujoco-py is properly installed.
```
cd ~/.mujoco/mujoco-py/examples
python3 setting_state.py
```
8.  RL environment - Open new terminal
```
cd
git clone https://github.com/Asad-Shahid/RL-Project-D5041E.git
cd /RL-Project-D5041E/panda
conda env create -f environment.yml
conda activate rl-project
python -m rl.main
