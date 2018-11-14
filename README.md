Reid sub-system

# install
```bash
pip install -r requirements.txt
```

# simple use
```python
import reid
import cv2
video = reid.get_data('/path/to/your/file')
pictures = reid.get_picture(video)
for picture in pictures:
	cv2.imshow('pic', picture)
	k = cv2.waitKey(30) & 0xff
	if k == 29:
		break
cv2.destroyAllWindows()
```
#faster rcnn for reid usage
'''
faster rcnn for reid 剪切行人图片功能运行

1：demo.py in line407 设置write json路径
2：import /lib/data/save_json.py cut_image函数，读取存储目标坐标框的json信息文件，裁剪目标图片
‘’‘
