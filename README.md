# UNO-Q

## Exploring the Arduino UNO-Q

The **Arduino UNO-Q** is a surprisingly powerful board that bridges the familiar Arduino ecosystem with a **Linux-capable quad-core system-on-chip**. While it preserves the simplicity of Arduino-style development, it adds a far more capable processing layer suitable for **image analysis, data processing, and networked applications**.

At its core, the UNO-Q combines:
- A **classic Arduino-compatible microcontroller** for real-time I/O and deterministic tasks  
- A **quad-core ARM-based Linux processor** (Qualcomm-derived) running a full Linux distribution  

This hybrid architecture allows integration between low-level hardware control and high-level Linux applications.

Despite this complexity, the board is remarkably quick to get running out of the box, even for users without prior Linux-on-embedded experience.

## Arduino App Lab

The official development environment, **Arduino App Lab**, is still under active development (we used **version 0.3.2 in January 2026**), but it already works reasonably well. All provided example applications ran successfully without modification.

An interesting design choice appears when pressing **“Run”**:  
application files are **added** to the board rather than replacing existing projects. Earlier projects are not immediately deleted, which likely reduces iteration time when switching back and forth between experiments. It remains unclear whether older projects are automatically removed later when storage becomes constrained.

---

## Linux Side & Containers

On the Linux side, **Docker is preinstalled**, enabling containerized workflows directly on the board. There is no strict one-to-one mapping between so-called *“bricks”* and Docker containers, but conceptually, bricks seem to be based on docker containers.


## Opening the Hood

Although **Arduino App Lab** is a relatively closed system and abstracts away many implementation details, gaining direct access to the underlying Linux system is trivial.

You can simply open a **remote shell via SSH** (either using standard SSH commands or by clicking the SSH option in the bottom-left corner of the main window). Once connected, you have full access to the Linux environment, including system services, Docker containers, and the filesystem.

On first connection, the board is assigned a hostname (for example, `Danuno` in our case), which can then be used for subsequent SSH sessions.

---

Overall, the UNO-Q feels less like a traditional Arduino and more like a **compact, developer-friendly embedded Linux system with Arduino DNA**—a combination that opens the door to far more advanced applications than typical UNO-class boards.

Frequently used commands:
```zsh
ssh arduino@192.168.1.167
ssh arduino@Danuno.local

echo "copy main folder on arduino UNO-q"
scp -rp arduino@192.168.1.167:ArduinoApps .

echo "copy main python file for detectobjcam app"
scp -rp arduino@192.168.1.167:ArduinoApps/detectobjcam/python/main.py .


```