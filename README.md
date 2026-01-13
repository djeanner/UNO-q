# UNO-q

Exploration of the arduino UNO-q

Arduino UNO-Q is a surprising powerful arduino bridged to a Quadcom core with 4-core linux capabable of image analysis that is surprisingly powerful and quickly to get working out-of-the-box.

The official application, `Arduino App Lab`, is still under development (ee used Ver 0.3.2 in Jan 2026) but works reasonably well. All Example apps worked immediately well.

Intrestingly when pressing "run" the files are add to the board. The other projects are not deleted, which is probably saving time when returning to early projects. (is it deleting them later when space is tight?)

On the linux side, dockers are installed. There is no one-to-one relation between so-called "bricks" and dockers, but bricks are bradly speaking dockers.

Since the `Arduino App Lab` is quite closed sysrtem, it is difficult to understand what realy goes on under the hood, but opening the hood is trivial. Simply open a remote shell using `ssh` (see commands below or click at the bootom left of the main window).

At the initial connection, a board is given a name (`Danuno` in our case).

Frequently used commands:
```zsh
ssh arduino@192.168.1.167
ssh arduino@Danuno.local

echo "copy main folder on arduino UNO-q"
scp -rp arduino@192.168.1.167:ArduinoApps .

echo "copy main python file for detectobjcam app"
scp -rp arduino@192.168.1.167:ArduinoApps/detectobjcam/python/main.py .


```