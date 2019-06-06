# icub-face-detection
Software to detect the iCub's face from Images and Videos

## Instructions on how to label data, prepare data, and run data

1. Use VoTT (Microsoft)
2. change export data to Pascal VOC (to get .xml files)
3. don't forget to specify that you only want the labelled data
4. get a video/image in mp4 MPEG format
5. build bounding boxes of the icub face in the relevant frames
6. save the project (remember that I won't save the labelled assets)
7. always confirm that the project is counting the labelled assets (otherwise you won't have bouding boxes of the icub face in the .xml files)
8. get the dataset and use xml_to_csv.py file to convert to a csv file
9. From tensorflow/models/research/
``` bash
export PYTHONPATH=$PYTHONPATH:`pwd`:`pwd`/slim - to run the object_detection API to convert to TFRecords
```
10. use the generateTFrecords.py file to genereate the tfrecords from the csv file
11. add the train.records, test.records, and 2 more to the data folder of the object_detection API
12. add the model (ssd_model for now) + the .pbdx file to the training folder
13. add the images of the dataset to a folder (icub_face) inside the object_detection API (still don't know what for)

## Instructions on how to test the trained model

After you have trained your model you want to test it. This is what you need to do:
1. export the graph of your train model
``` bash
python3 object_detection/export_inference_graph.py     --input_type image_tensor     --pipeline_config_path object_detection/training/ssd_mobilenet_v1_pets.config     --trained_checkpoint_prefix object_detection/training/model.ckpt-200000 --output_directory object_detection/icub_graph/
```
2. add the frozen model to your program - frozen_inference_graph.pb
3. add the labels of your model - icub_detection.pbtxt




