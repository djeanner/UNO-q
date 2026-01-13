# detectObjCam

We started this project from the "Video Generic Object Detection" example from Arduino App Lab ver. 0.3.2

Using a very poor webcam the analysis of a street seen from above identified most persons walking on the sidewalk but misses about half the cars passing through. Note the camera was not adapting to sun/dark.

Mostly, we changed the following lines of main.py to log the detected objects.

```python
print(f"Detected {key}, at {datetime.now(UTC).isoformat()} with confidence: {value.get("confidence")} in {value.get("bounding_box_xyxy")}")
```
the output has this form:
```txt
Detected person, at 2026-01-13T13:53:16.453588+00:00 with confidence: 0.5642414689064026 in (267, 145, 279, 180)
```
where the four last integers are [x_min, y_min, x_max, y_max] of the detection bounding box.

# Dockers


```zsh
docker ps
```

## Docker : detectobjcam-main-1

Python libraries in docker detectobjcam-main-1

```zsh
docker exec -it detectobjcam-main-1 pip list
```

[`pip list` ouput](detectobjcam-main-1/pip_list.txt)

## Docker : detectobjcam-ei-video-obj-detection-runner-1 

Not a python docker

## File tree 

[file tree](tree.txt)
