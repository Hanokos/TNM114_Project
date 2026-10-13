# TNM114 — Godot Project

This project contains a 3D drone simulation built with Godot and a Python-based reinforcement learning setup used to train the drone.

## 1. Download Godot

Download the Godot Engine for Windows from the official website:

https://godotengine.org/download/windows/

Download a version compatible with the project. If the project was created with Godot 4, use a Godot 4 release.

## 2. How to Open the Godot Project

1. **Download the ZIP** containing the project.
2. **Extract the ZIP** to a location of your choice, for example:
   `Documents/TNM114/`
3. **Open Godot Engine.**
4. Click **Import**.
5. Navigate to the extracted folder and select the folder containing `project.godot`.
6. Click **Import & Edit** to open the project.
7. Once the project is open, click the **▶ Play Project** button to run it.

### Troubleshooting

If Godot does not recognize the project, make sure you selected the folder that directly contains the `project.godot` file, rather than the ZIP file itself.

If Godot reports script errors, check the error message and make sure you are using a compatible Godot version.

---

## 3. Install Python

The reinforcement learning training code runs through Python in the Visual Studio Code terminal. Python must be installed separately from Godot.

1. Download Python for Windows from the official website:

   https://www.python.org/downloads/windows/

2. Run the installer.
3. **Important:** Enable **Add Python to PATH** during installation.
4. Complete the installation.
5. Open Visual Studio Code.
6. Open the project folder in Visual Studio Code.
7. Open the integrated terminal using **Terminal → New Terminal**.

Check that Python is installed correctly by running:

```powershell
python --version
```

If that command does not work, try:

```powershell
py --version
```

You should see the installed Python version.

## 4. Create a Python Virtual Environment

A virtual environment keeps the project's Python packages separate from other Python projects on your computer.

In the Visual Studio Code terminal, navigate to the folder containing the Python training code.

For example:

```powershell
cd Documents/TNM114
```

Use the actual path to your extracted project if it is different.

Create the virtual environment:

```powershell
python -m venv .venv
```

Activate it in the Windows PowerShell terminal:

```powershell
.\.venv\Scripts\Activate.ps1
```

If you are using Command Prompt instead of PowerShell, activate it with:

```cmd
.venv\Scripts\activate.bat
```

When the environment is active, the terminal should display `(.venv)` before the command prompt.

If PowerShell blocks activation because of its execution policy, you can use Command Prompt instead, or activate the environment using the appropriate PowerShell permissions for your computer.

Update pip:

```powershell
python -m pip install --upgrade pip
```

## 5. Install the Python Dependencies

The training code uses Python libraries for reinforcement learning and numerical computation.

### Option A — If the project contains `requirements.txt`

Check whether a `requirements.txt` file exists in the project folder.

If it does, install the listed dependencies with:

```powershell
python -m pip install -r requirements.txt
```

This is the preferred method because the file can specify the packages and versions intended for the project.

### Option B — Install the main packages manually

If there is no `requirements.txt`, activate the virtual environment and install the common packages used by a PPO-based reinforcement learning setup:

```powershell
python -m pip install stable-baselines3 gymnasium numpy torch tensorboard
```

These packages provide:

- **Stable-Baselines3:** Reinforcement learning algorithms, including PPO.
- **Gymnasium:** An environment interface for reinforcement learning.
- **NumPy:** Numerical calculations and array operations.
- **PyTorch:** The neural network framework used by Stable-Baselines3.
- **TensorBoard:** Tools for visualizing training metrics, if logging is configured.

Depending on the Python scripts, additional packages may be necessary. Check the imports at the beginning of the training files and install any missing third-party libraries.

For example, if the code imports a package that is not installed, Python may report `ModuleNotFoundError`. Install the corresponding package in the active virtual environment.

**Note:** These manual installation commands provide a starting point. They do not guarantee that every dependency or exact version required by the project has been covered.

## 6. Run the Python Training Code

1. Open the project folder in Visual Studio Code.
2. Open **Terminal → New Terminal**.
3. Activate the virtual environment if it is not already active:

   ```powershell
   .\.venv\Scripts\Activate.ps1
   ```

4. Locate the Python training script in the project.
5. Run the correct script using Python. For example, if the file is named `train.py`:

   ```powershell
   python train.py
   ```

   Replace `train.py` with the actual filename of the training script.

6. Follow the terminal output to monitor training progress, episode statistics, and any error messages.

The training process may take time depending on the computer, the training configuration, and the difficulty of the environment.

If the project uses saved models or normalization statistics, keep the required files in the expected locations. Do not delete model checkpoints or training data unless you intend to start training again.

## 7. Select the Correct Python Interpreter in Visual Studio Code

To make sure Visual Studio Code uses the packages installed in your virtual environment:

1. Press `Ctrl + Shift + P`.
2. Search for **Python: Select Interpreter**.
3. Select the interpreter located at:

   ```text
   .venv\Scripts\python.exe
   ```

4. Open a new terminal and activate the environment if necessary.

You can check which Python executable is being used with:

```powershell
python -c "import sys; print(sys.executable)"
```

The output should point to the project's `.venv` directory.

## 8. Recommended Workflow

For normal use, follow this order:

1. Open the project in Godot.
2. Run the simulation to verify that the environment works.
3. Open the same project folder, or the folder containing the training scripts, in Visual Studio Code.
4. Activate the Python virtual environment.
5. Install the required dependencies if they have not already been installed.
6. Run the Python training script.
7. Monitor the training statistics in the terminal.
8. Use the trained model in the simulation according to the project's implementation.

The exact order may differ if the project starts the simulation and training through separate processes or uses a particular communication method between Godot and Python.

## 9. Troubleshooting

### Python is not recognized

Make sure Python is installed and added to PATH. Restart Visual Studio Code after installing Python and try:

```powershell
py --version
```

### A Python module is missing

Activate the virtual environment and install the missing dependency. If the project contains `requirements.txt`, install its dependencies first.

### The wrong Python environment is being used

Select `.venv\Scripts\python.exe` through **Python: Select Interpreter** in Visual Studio Code.

### The training script cannot find the Godot project or model files

Check the paths used in the Python scripts. Run the script from the expected project directory and verify that the required model and configuration files exist.

### The drone does not appear to learn

Check that training is actually running, that the reward and episode statistics are being updated, and that model checkpoints are being saved where expected. Reinforcement learning performance can vary between training runs.

### Godot and Python work separately but not together

Check how the project connects the Python training process to the Godot simulation. Verify that any required connection settings, executable paths, and startup steps match the project configuration.

---

## 10. Useful Official Resources

- **Godot for Windows:** https://godotengine.org/download/windows/
- **Python for Windows:** https://www.python.org/downloads/windows/
- **Visual Studio Code:** https://code.visualstudio.com/
- **Python virtual environments:** https://docs.python.org/3/library/venv.html
- **Stable-Baselines3 documentation:** https://stable-baselines3.readthedocs.io/
- **Gymnasium documentation:** https://gymnasium.farama.org/
- **PyTorch installation guide:** https://pytorch.org/get-started/locally/

## Summary

To run the project, you need Godot 4 for the 3D simulation and Python with the required dependencies for the reinforcement learning code. Godot handles the simulation, while Python handles the training process. Make sure both environments are configured correctly before running the complete project.
