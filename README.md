Reid sub-system

# Requirement
```
gcc-5
cuda9.0
```

# install
```bash
git clone https://github.com/cutrain/reid
cd reid
pip install -r requirements.txt
cd frcnn/lib
./make.sh
```

# prepare
You should put the pretrained model at ./frcnn/model/faster_rcnn.pth

# *use* (one step)
```python
import sys
sys.path.append('/path/to/the/reid_module')
import reid
import skimage

person_paths = ['a.jpg', 'b.jpg']
video_paths = ['a.mp4', 'b.mp4']
imgs = reid.person_reid(person_paths, video_paths, k=10)
for i in range(len(person_paths)):
	for person in imgs[i]:
		skimage.io.imshow(person)
```
**NOTE** : image is RGB format, remember to change channel if you use cv2 (which is BGR)

# *use* (step by step)
```python
import sys
sys.path.append('/path/to/the/reid_module')
import reid
import skimage

# read video
video = reid.get_data('/path/to/your/file')
# generate pictures
pictures = list(reid.get_picture(video))
# person detection
bboxes = list(map(reid.detect, pictures))
img = reid.draw_box(pictures[0], bboxes[0])
# cut images
for i in range(len(bboxes)):
	data_images = reid.cut_image(pictures[i], bboxes[i])
# feature extraction
features = reid.get_feature(data_images)
# retrieval
index = reid.retrieval(features[0], features, k=10) # you can change features[0] into any other feature you got

```

