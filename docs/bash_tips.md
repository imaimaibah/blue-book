---
title: Bash Snippets
date: 20251214
author: imaimaibah
---

# Loop through multiple elements per line

```bash
# Open file descriptor 3
while IFS='|' read -r i j rest <&3; do
  {
    printf '%s\n' "something with $i and $j"
    # Close file descriptor 3 for the child process
  } 3<&-
done 3< <(kubectl get --no-headers po -A |awk '{print $1"|"$2}')
```


# Replace the shell file descriptors.

The following example replaces file descriptors in the shell.

```shell
#!/bin/bash

exec > >(tee file.log) 2>&1

ls -l
pwd
```

# Manage background processes with timeouts.

To avoid zombie processes with timeout and PID monitoring.

```shell
my_long_task &
pid=$!
timeout 60s tail --pid=$pid -f /dev/null || {
  echo "Task timed out "
  kill $pid
}
```

# Parameter expansion

# Array expansion

# printf

# date format

# regex
BASH_REMATCH[@]
