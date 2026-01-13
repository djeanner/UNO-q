# detectObjCam

We started this project from the "Video Generic Object Detection" example from Arduino App Lab ver. 0.3.2

Using a very poor webcam the analysis of a street seen from above identified most persons walking on the sidewalk but misses about half the cars passing through. Note the camera was not adapting to sun/dark.

Still, not bad for 50 EUR and 800 mA at 5 V.

Mostly, we changed the following lines of main.py to log the detected objects.

```python
print(f"Detected {key}, at {datetime.now(UTC).isoformat()} with confidence: {value.get("confidence")} in {value.get("bounding_box_xyxy")}")
```
the output has this form:
```txt
Detected person, at 2026-01-13T13:53:16.453588+00:00 with confidence: 0.5642414689064026 in (267, 145, 279, 180)
```
where the four last integers are [x_min, y_min, x_max, y_max] of the detection bounding box.

Extract the logs of the docker with
```bash
docker logs -f detectobjcam-main-1 >> logObj.txt
```
... and copy it out of the board with ...
```bash
scp arduino@Danuno.local://home/arduino/logObj.txt .
```

# Tuning detector

Tuning parameters of the UNO-Q object detector is difficult because the YOLOX model is embedded inside a precompiled Node runner. The model’s inference logic, including NMS IoU, input resolution, max detections, and class list, is baked into the container at build time. Python only communicates via WebSocket, so it can override confidence thresholds, but cannot modify internal YOLOX behavior. Edge Impulse packages the model as a binary blob, with thresholds applied internally. The container is immutable, optimized for stability, and App Lab does not expose the internal configuration. Only post-processing in Python or a custom Edge Impulse deployment allows parameter changes.

# Dockers

Just for easy copy/paste, find here some useful commands in the context of development and follow updates in libraries, *etc.*

```zsh
docker ps
```

## Docker : detectobjcam-main-1

Python libraries in docker detectobjcam-main-1

```zsh
docker exec -it detectobjcam-main-1 pip list
```
or on two steps
```zsh
docker exec -it detectobjcam-main-1 bash
pip list
```

[`pip list` ouput](detectobjcam-main-1/pip_list.txt)

## Docker : detectobjcam-ei-video-obj-detection-runner-1 

Not a python docker. This is the main YOLOX docker for object detection.

## File tree 

[file tree](tree.txt)
