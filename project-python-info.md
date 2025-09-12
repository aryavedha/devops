Installations of python project and needed packages 
1.install python 3.
```
sudo apt install python3
```

2.Install pip (Python Package Installer):
pip is crucial for installing and managing Python packages.
```
sudo apt install python3-pip
```
3. Install venv (Virtual Environment Tool):
venv allows you to create isolated Python environments for your projects, preventing conflicts between package versions.
```
sudo apt install python3-venv -y
```
4. one go 3 packages python3 pip3 venv
```
sudo apt update
sudo apt install python3 python3-pip python3-venv -y
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

# run application
```
pthon run.py
```

4.Install the desired Python version (e.g., Python 3.11):
```
sudo apt install python3.11
```

---

- Verify

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

- Deactivate

To exit the environment:
```
deactivate
```
```

