# avkans-ndi-utils
A class for getting NDI frames out of Avkans NDI cameras in cv2 compatible formats.

## Background
AVKans makes an inexpensive line of cameras that now support NewTek NDI protocol.   This module is intended to make it easy to connect and get cv2 images from these cameras, and likely other NDI sources.   It was originally created as part of an AI face tracker.

This package is not distributed by or endorsed by AVKans or NewTek.

## License
This is licensed under the MIT License.

## Dependencies
This is a simple wrapper for the NDI Library, and requires it to work.   It also uses numpy, and it's recommended to install cv2 if you wish to manipulate the images.
```
pip install ndi-python
pip install numpy
pip install opencv-python
```

## Color notes
Newtek images come in the standard RGB format, but cv2 normally uses BGR format.   You can trivially change between them using cv2 as follows.   If your images come out looking like the color channels are mixed, try this.
```
img=cam.get_cv2_frame()
img=cv2.cvtColor(img,cv2.COLOR_BGR2RGB,img)
```

## Example usage

```
from avkans-ndi-utils import AvkansCamera
import numpy as np
import cv2


cam1 = AvkansCamera()

# Search for sources (optional - you can directly connect by IP if you don't need discovery)
search_results = cam1.get_sources_as_dict()
print("Search results: ",search_results)

# Connect by IP
result = cam1.connect_by_ip("192.168.35.37")
print(result)

for i in range(30):
    t=time.time()
    frame = cam1.get_cv2_frame()
    print(f"Got frame {i} in ",time.time()-t, " seconds.")

t=time.time()
frame = cam1.get_cv2_frame()
print("Got frame in ",time.time()-t, " seconds.")
print("Frame shape:  ",frame.shape)





```

