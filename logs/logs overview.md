| Log               | Purpose              | Question it answers        |
| ----------------- | -------------------- | -------------------------- |
| **Build Journal** | System state changes | “What changed in the lab?” |
| **Homelab Log**   | Operational activity | “What did I do today?”     |

## 🚫 What You Should NOT Log

Do **not** add entries for:
- Individual Git commands
- Minor typo fixes
- Viewing files
- Pulling updates
- Reading documentation

If nothing changed **structurally or conceptually**, do **not** create a log entry.

> **Restraint is a skill.**

---

## 🧠 Logging Rule of Thumb (Lock This In)

Before logging, ask yourself:

> *“If I read this six months from now, will it explain a decision or state change?”*

Use the answer to choose the log:

- **Yes → Build Journal**  
- **It just describes what I did today → Homelab Log**  
- **It explains something I learned or understood → Learning Log**
