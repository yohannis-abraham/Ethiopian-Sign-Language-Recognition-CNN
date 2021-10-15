# Ethiopian-Sign-Language-Recognition-CNN
The goal of this project was to develop a real-time ESL recognition system in which ESL sign gestures are recognized by a CNN model. The model provides text/voice output for correctly recognized signs. To accomplish this goal, the following approaches were utilized.

## Dataset
A data-set in machine learning is a collection of data pieces that can be used to train machine learning model for prediction or regression purposes. For this study, the ESL dataset was collected from \url{https://data.mendeley.com/datasets/5d3nkyhsrf/1}. It contains 1172 RGB images of the size of 1280x720. The dataset contains gesture images of only 7 ESL alphabets, i.e. 'che,'gne','ke','le','me','ne' and ’qe’. Data-processing techniques were applied and managed to extract the palm area of the signer as a 64x64px gray scaled image. Furthermore, a csv dataset was generated from pre-processed images, composing label (1 column) and image pixel (4096 columns) values of each image as a row. Finally, the csv dataset was used to build our CNN model. Two approaches were implemented in this project. The first one uses ESL dataset (image data) to build and train our model. Whereas, the second approach uses Google's Mediapipe to extract 21 landmarks (x and y coordinates) from the static image data. The extracted hand landmarks were used to train our CNN model.

## Approach one (Using ESL image dataset):
In this approach we used a dataset of 64x64px pre-processed hand sign gesture images to train and evaluate the CNN model. To accomplish this task, we first extract image pixel values from all training images, normalize them and dump them in to csv file containing label and all 4596 pixels as a column. We iterate through all images in the dataset and generate a csv file containing pixel values of all the images in the dataset. We cleaned out empty rows and load it for training. The basic steps used in this approach was as follows.
1.  Load ESL dataset (generated CSV) and split them for train-test (80:20% ratio)
2.	Extract class labels from the training set and encode them (LabelBinarizer was used)
3.	Normalize the image pixel values (divide by 255)
4.	Flatten the input image dimensions to 1D (width pixels x height pixels)
5.	Build a model architecture (Sequential) with Dense layers
6.	Train the model and evaluate it and save the model for later use
7.	Load the trained model and make prediction from signs extracted from live camera feed (Here Open CV was used to extract ROI region from webcam feed and fed it to our model to recognize it)

## Approach two (Using MediaPipe and ESL dataset):
The second implementation approach uses MediaPipe alongside ESL image dataset. MediaPipe offers cross-platform, customizable ML solutions for live and streaming media. A sub section of MediaPipe called MediaPipe Hands was used in this project.  MediaPipe Hands is a high-fidelity hand and finger tracking solution. It employs machine learning (ML) to infer 21 3D landmarks of a hand from just a single frame. For two-dimensional data such as images, only 3D landmarks (X & Y values) are required. Here we used MediaPipe to extract hand landmarks from a given image and used those landmarks to train and test the CNN model. The basic steps used in this approach was as follows.
1.	Develop a dataset (CSV) consists of 21 landmarks and the class label using MediaPipe to extract landmarks from images (ESL gestures).
2.	Normalize values between 0 and 1.
3.	Encode labels (One Hot Encoding)
4.	Build a model architecture (sequential) with dense layers. The model architecture was the same as that of approach one. But here Conv1D and MaxPooling1D were used since the dataset was composed of one-dimensional data when defining the model.
5.	Train the model (using our landmarks dataset) and evaluate it and save the model for later use
6.	Load the trained model and make prediction from signs extracted from live camera feed (Here Open CV was used to extract ROI region from webcam feed and fed it to our model to recognize it)

