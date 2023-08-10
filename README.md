# FFMpeg
Contains all the code and description of video file conversions of different format

Convert Image Sequence to H264 using ffmpeg:
=====================================================================================
ffmpeg -framerate 30 -i DSC_%04d.JPG -c:v libx264 -crf 23 -pix_fmt yuv420p output.mp4

[Alternatively, you can use the following to convert a set of Images into Video:

import numpy as np
import glob
 
img_array = []
for filename in glob.glob('C:/New folder/Images/*.jpg'):
    img = cv2.imread(filename)
    height, width, layers = img.shape
    size = (width,height)
    img_array.append(img) 
 
out = cv2.VideoWriter('project.avi',cv2.VideoWriter_fourcc(*'DIVX'), 15, size)
 
for i in range(len(img_array)):
    out.write(img_array[i])
out.release()]

FFMPEG extracts intra-frames I, P,B frames: (in example we have B frames
===========================================================================
ffmpeg -i <inputfile> -vf '[in]select=eq(pict_type\,B)[out]' b.frames.mp4

On a related note, we can use colors to show each macroblock:
============================================================================
ffmpeg -debug vis_mb_type -i input.mp4 output.mp4

This will also show you the motion vectors:
ffplay -debug vis_mb_type -vismv 7 input.mp4

