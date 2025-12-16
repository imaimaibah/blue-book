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

