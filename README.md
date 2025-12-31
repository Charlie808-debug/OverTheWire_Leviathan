![GitHub repo size](https://img.shields.io/github/repo-size/Charlie808-debug/OverTheWire_Leviathan)
![GitHub stars](https://img.shields.io/github/stars/Charlie808-debug/OverTheWire_Leviathan)
![GitHub issues](https://img.shields.io/github/issues/Charlie808-debug/OverTheWire_Leviathan)

# OverTheWire — Leviathan Writeups & Concepts

This repository contains my complete writeups for the **Leviathan wargame**, the next step after Bandit in OverTheWire.  
Leviathan focuses on early-stage binary exploitation, privilege escalation, symbolic link attacks, and brute-force automation.

> 🔧 Levels solved: `leviathan0 → leviathan7`  
> 🎯 Goal: bridge the gap between shell fundamentals (Bandit) and binary exploitation basics

---

## 🛠 Skills Demonstrated

- SUID binary behavior & misuse
- Tracing binaries using **`ltrace`** and **`strace`**
- Extracting embedded secrets with **`strings`**
- Symbolic link exploitation (`ln -s`) to redirect access
- Handling tricky filenames to bypass logic
- Brute-forcing limited keyspaces (4-digit password)
- Restricted shell → privilege escalation progression
- Reading password files via escalated execution context

---

## 🧪 Core Cybersecurity Concepts

| Concept | Explanation |
|---------|------------|
| **SUID privilege execution** | Binaries can run as another user, including privileged users |
| **Symbolic link attacks** | Re-routing file operations through symlinks to expose secrets |
| **Hardcoded passwords** | Credentials embedded in binaries are discoverable via tracing |
| **Input handling weaknesses** | Spaces in paths & missing validations lead to escalation risks |
| **Brute force feasibility** | Small search spaces (~10k combos) are computationally trivial |
| **Binary observation** | Behavior analysis often reveals more than static analysis |

---

## 📌 Why Leviathan matters

| From | To |
|------|----|
| Shell comfort (Bandit) | Binary exploitation awareness |
| Command execution | Program behavior analysis |
| Reading files | Manipulating execution flow |
| Theory of privilege escalation | Practical escalation & exploitation |

This progression is extremely relevant for:
- **CTFs**
- **reverse engineering**
- **privilege escalation labs**
- **junior pentesting roles**

---

## 🤝 Contributions / Feedback

If you're working through Leviathan and want help:
- open an issue 📌
- suggest improvements 💡
