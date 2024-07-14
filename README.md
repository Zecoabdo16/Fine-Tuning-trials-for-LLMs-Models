# Use a pipeline as a high-level helper
!pip install av
from transformers import VideoMAEImageProcessor, VideoMAEForVideoClassification
import numpy as np
import torch
from transformers import pipeline

processor = VideoMAEImageProcessor.from_pretrained("MCG-NJU/videomae-huge-finetuned-kinetics")


pipe = pipeline("video-classification", model="MCG-NJU/videomae-huge-finetuned-kinetics" , device = 0, image_processor = processor )



import os
fight_true = 0
all_counts = 0
for i in os.listdir('/kaggle/input/fight-det/fight-detection/fight-detection/fights'):
    all_counts += 1
    result = pipe(f'/kaggle/input/fight-det/fight-detection/fight-detection/fights/{i}')[0]
    if result['label'] in ['arm wrestling','bench pressing','headbutting','punching bag','punching person (boxing)','sword fighting','wrestling','side kick','high kick','headbanging','digging','faceplanting','hammer throw','slapping','tai chi','throwing axe','throwing ball','playing cricket','passing American football (in game)','passing American football (not in game)','drop kicking']:
        fight_true += 1
    else:
        print(result['label'])
print(f'{(fight_true /all_counts ) * 100}%' )



classes for climbing 
"climbing a rope": 66
"66": "climbing a rope",
"67": "climbing ladder",
"68": "climbing tree",
ice climbing: 162
rock climbing: 278
ice climbing : 162



running
Jogging 
running on treadmill": 281
jogging  : 168
hurdling: 160,
skipping rope": 311
hurling : 161
