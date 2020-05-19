# Task01 Understand Competition
This is a competition about street view house number recognition. The task is that giving an image, outputs n bounding box and n numbers showing the position and value of the house numbers. To simplify the task, the function becomes giving an image, outputs N numbers (fixed length, -1 means none) indicating the house numbers.  
## Learning Object
- familiar with the background and data of competition
- get start with PyTorch
## Images and Labels
- 30k Training, 10k Validation and 80K Testing
- Each image has uncertain numbers 
- Some numbers are not horizontal
- Labels: all image has a json file showing that each number has a bounding box (x, y, height, width) and its value.
- Metrics: Accuracy
  