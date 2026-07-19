# Python runs shell
#python #shell #programming #tech
## this is /home/rachel/.nb/home/tech/python_runs_shell.md

```code python
run command "ls -la", capturue the output, prints it:

import subprocess

cmd = ["ls", "-la"]
res = subprocess.run(cmd, capture_output=True, text=True)

print("Output:")
print(res.stdout)
print(f"Exit code: {res.returncode}")
```

# catching terminal errors
## catches terminal errors. forces python to stop and show the error message if
the terminal command breaks or a file is missing.
```code python
import subprocess

try:
    cmd = ["ls", "/missing/folder"]
    subprocess.run(cmd, check=True, capture_output=True, text=True)
except subprocess.CalledProcessError as e:
    print(f"Failed! Code: {e.returncode}")
    print(f"Error: {e.stderr.strip()}")
```

# using pipes and shell features
## use shell=True to pipe or use wildcards inside a string
```code python
import subprocess

# This looks for any active python processes
my_string = "ps aux | grep python"
res = subprocess.run(my_string, shell=True, capture_output=True, text=True)

print(res.stdout)
```

# handing control to terminal apps
## omit capture_even and the python script steps aside and lets the program do its thing
```code python
import subprocess

# This opens htop interactively in your shell
subprocess.run(["htop"])
print("Returned to Python!")
```
