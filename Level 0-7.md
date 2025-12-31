# 🔐 **OverTheWire — Leviathan Writeups (Levels 0–7)**

### 🔸 **Level 0 → Level 1**

**Objective**
Locate hidden content in backup files to obtain the password for leviathan1.

**Commands Used**
`ls -la`, `cd`, `cat`, `grep`

**Step-by-step**

1. `ls -la`
   Listed files and identified `.backup`
2. `cd .backup`
   Navigated into backup directory
3. `ls -la`
   Found `bookmarks.html`
4. `cat bookmarks.html | grep leviathan1`
   Extracted password reference from the file

***Result:*** Password successfully retrieved

---

### 🔸 **Level 1 → Level 2**

**Objective**
Analyze a binary to discover a hardcoded password, then use it to gain access.

**Commands Used**
`ls -la`, `ltrace`, `./check`, `strcmp`, `cat`

**Step-by-step**

1. `ls -la` → saw binary `check`
2. `ltrace ./check` and entered a test password (e.g., `test`)
   ltrace revealed comparison: `strcmp("test","sex") = 1`
3. Correct password: `sex`
4. `./check` and enter `sex` to get a shell as leviathan2
5. `cat /etc/leviathan_pass/leviathan2`
   Retrieved password

***Result:*** Password successfully retrieved

---

### 🔸 **Level 2 → Level 3**

**Objective**
Exploit filename handling and symbolic links to access a protected password file.

**Commands Used**
`ltrace`, `mkdir`, `touch`, `ln -s`, `./printfile`

**Step-by-step**

1. `ltrace ./printfile /etc/passwd`
   Confirmed it prints files passed as arguments
2. `mkdir /tmp/lev2 && cd /tmp/lev2`
3. `ln -s /etc/leviathan_pass/leviathan3 file1`
4. `touch "file1 file2"` (space confusion → exploit)
5. `~/printfile "file1 file2"`
   Program follows symlink → prints password

***Result:*** Password successfully retrieved

---

### 🔸 **Level 3 → Level 4**

**Objective**
Use dynamic library call tracing to locate a hardcoded password inside a binary.

**Commands Used**
`ls -la`, `ltrace`, `strcmp`, `./level3`, `cat`

**Step-by-step**

1. `ltrace ./level3` and enter any password (test)
   Output shows: `strcmp("test","snlprintf")`
2. Correct password: `snlprintf`
3. `./level3` → enter `snlprintf`
4. `cat /etc/leviathan_pass/leviathan4`

***Result:*** Password successfully retrieved

---

### 🔸 **Level 4 → Level 5**

**Objective**
Decode binary output to extract the next password.

**Commands Used**
`cd`, `ls -la`, Python decoding or binary→ASCII conversion

**Step-by-step**

1. `cd .trash && ls -la && ./bin`
   Binary output shown as raw binary bits
2. Convert binary to ASCII using script:

   ```python
   text = ''.join(chr(int(binary_string[i:i+8],2)) for i in range(0,len(binary_string),8))
   print(text)
   ```

   *(or online converter)*

***Result:*** Password successfully retrieved

---

### 🔸 **Level 5 → Level 6**

**Objective**
Exploit symbolic link behavior in a SUID program to read a protected password file.

**Commands Used**
`ltrace`, `echo`, `ln -s`, `cat`

**Step-by-step**

1. `echo "hello" > /tmp/file.log`
2. `ln -s /etc/leviathan_pass/leviathan6 /tmp/file.log`
3. `./leviathan5`
   Program follows symlink → prints password

***Result:*** Password successfully retrieved

---

### 🔸 **Level 6 → Level 7**

**Objective**
Determine the correct 4-digit password through brute force or reverse engineering, then obtain a shell to read leviathan7’s password.

**Commands Used**
`./leviathan6`, bash loop, optionally `gdb`, `strings`, `ltrace`, `strace`

**Step-by-step**

1. Tried static analysis (`strings`, `ltrace`, `strace`) — no direct leak
2. Ran brute-force loop:

   ```bash
   for i in {0000..9999}; do ./leviathan6 $i; done
   ```
3. Correct code grants a shell as leviathan7
4. `cat /etc/leviathan_pass/leviathan7`

***Result:*** Password successfully retrieved

---

### 🔸 **Level 7 — The End**

**Objective**
Retrieve final password after reaching highest privilege level.

**Commands Used**
`cat`

**Step-by-step**

1. Already escalated from previous step
2. `cat /etc/leviathan_pass/leviathan7`

***Result:*** All Leviathan levels completed successfully!

### **Key Learning**

* Gained practical exposure to **SUID binaries** and how insecure implementations lead to privilege escalation
* Learned to use **ltrace / strace** to observe runtime behavior, revealing hidden passwords and logic flaws
* Discovered that **hardcoded credentials in binaries** can be extracted through tracing function calls (`strcmp`, etc.)
* Understood **symbolic link attacks** to redirect program file access toward protected files
* Learned how **filenames with spaces or special characters** can bypass input validation checks in binaries
* Strengthened skills in **enumerating binary behavior instead of guessing**
* Performed **controlled brute force attacks** on small keyspaces (4-digit PIN) to obtain access
* Explored the importance of **input sanitization** and how missing checks create exploitation paths
* Observed how **binary inspection tools (`strings`)** can reveal meaningful strings, logic hints, and data leaks
* Developed early **reverse engineering intuition**, transitioning from shell tasks (Bandit) to binary behavior (Leviathan)
* Learned to **manipulate execution flow** by replacing or redirecting inputs/environment paths
* Understood that **when static analysis fails, runtime analysis or brute force succeeds**
* Internalized escalation logic: *find a binary → observe behavior → redirect execution → gain access*
* Built confidence in **interpreting vulnerabilities conceptually**, not just solving levels mechanically


