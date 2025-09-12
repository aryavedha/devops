Installations of python project and needed packages 
1.install python 3.
```
sudo apt install python3
```
Verify the installation: You can check the installed Python version.
```
python3 --version
```

2.Install pip (Python Package Installer):
pip is crucial for installing and managing Python packages.
```
sudo apt install python3-pip
```
3. Install venv (Virtual Environment Tool):
venv allows you to create isolated Python environments for your projects, preventing conflicts between package versions.
```
sudo apt install python3-venv
```
4. one go three python pip venv
```
sudo apt update
sudo apt install python3 python3-pip python3-venv
```

# install venv if not present
```
sudo apt install python3-venv -y
```
# create venv
```
python3 -m venv venv
```
# activate it
```
source venv/bin/activate
```

# install dependencies
```
pip install -r requirements.txt
```


4.Install the desired Python version (e.g., Python 3.11):
```
sudo apt install python3.11
```

---
🔹 1. Create a virtual environment

If not created yet:
```
python -m venv venv
```

This makes a folder venv/ with your isolated Python environment.

🔹 2. Activate the environment
```
Linux / macOS (bash/zsh)
```
source venv/bin/activate
```
🔹 3. Verify

Once activated, your shell prompt will show the environment name, e.g.:
```
(venv) user@machine:~$
```

Check Python:
```
python --version
which python   # Linux/macOS
where python   # Windows
```
🔹 4. Deactivate

To exit the environment:
```
deactivate
```

