<!-- 8/8/24 Removed from transparency note because not released due to a bug. -->

## Scene, shot, and keyframe detection notes

- The detector works best on media files that have shots and scenes within them.  
- If the video is filmed with one camera that never moves, the shot segmentation works poorly, and the keyframes might not be representative. 
- Keyframes are selected by taking into account the blurriness level of the frames. If most of the shot is blurry, for example with motion, the keyframe might also be blurry. 
- Videos with poor visual quality produce poor results. 
- The time of each shot/scene/keyframe might shift (less than a second).

## Scene, shot, and keyframe components

No components defined.