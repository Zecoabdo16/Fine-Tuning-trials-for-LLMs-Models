cap = cv2.VideoCapture(video_path)

# Get video properties
frame_width = int(cap.get(cv2.CAP_PROP_FRAME_WIDTH))
frame_height = int(cap.get(cv2.CAP_PROP_FRAME_HEIGHT))
fps = int(cap.get(cv2.CAP_PROP_FPS))

# Define codec and create VideoWriter objects
# fourcc = cv2.VideoWriter_fourcc(*'XVID')  # For AVI format
# out_avi = cv2.VideoWriter('output_grayscale.avi', fourcc, fps, (frame_width, frame_height), isColor=False)

fourcc_mp4 = cv2.VideoWriter_fourcc(*'mp4v')  # For MP4 format
out_mp4 = cv2.VideoWriter('output_grayscale.mp4', fourcc_mp4, fps, (frame_width, frame_height), isColor=False)
cnt = 0

if video:

  while cap.isOpened():
      ret, frame = cap.read()
      if not ret:
          break
      # Convert frame to grayscale
      img = yolo_pred(frame)

  
      out_mp4.write(img)

      # cv2_imshow( gray_frame)
      if cv2.waitKey(1) & 0xFF == ord('q'):
          break
  # Release resources
      cap.release()
      out_avi.release()
      out_mp4.release()
      cv2.destroyAllWindows()

elif image:
  img = yolo_pred(img)
  cv2.imwrite('./img.png' , img)








from ultralytics import YOLO
import cv2
from ultralytics.utils.plotting import Annotator  # ultralytics.yolo.utils.plotting is deprecated


model = YOLO(model_path)


def yolo_pred(img)


  results = model.predict(img)

  for r in results:

      annotator = Annotator(img)

      boxes = r.boxes
      for box in boxes:

          b = box.xyxy[0]  # get box coordinates in (left, top, right, bottom) format
          c = box.cls
          annotator.box_label(b, model.names[int(c)])

  img = annotator.result()
return img
