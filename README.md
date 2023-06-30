# Monument Distinguisher

This project is capable of differentiating between different famous monuments (wonders of the world).

![Stonehenge example before model](https://github.com/epsilon71/Wonders-of-the-World-Classification/assets/102933624/7a23246e-2a5d-4a06-bf8a-50acc8b3bd28)
![Stonhenge image after classification through the model](https://github.com/epsilon71/Wonders-of-the-World-Classification/assets/102933624/7ff53f6b-e26c-4329-8a9e-cbf22c78805b)

## The Algorithm

This project uses the resnet-18 neural network to train a machine learning model to differentiate between different images and their classes. The training depends on using this neural network, the addition of labels and data (images). The testing requires testing images that were not in the training dataset.

Training the model depends on using this neural network, the addition of labels and data (images). The testing requires testing images that were not in the training dataset.

## Running this project

1. Open _Visual Studio Code_
2. Connect your _Jetson Nano_ through an SSH connection using the IP of the nano
3. Enter its password
4. Download the jetson-inference file from this link: [jetson-inference](https://github.com/dusty-nv/jetson-inference)
5. Download the dataset from this link: [dataset](https://www.kaggle.com/datasets/balabaskar/wonders-of-the-world-image-classification/download?datasetVersionNumber=2)
6. Make 3 new folders in the _Wonders of Word_ folder: **test** **train** and **val**
7. In each of those folders add a folder by the name of each of the classes you want to use (statue_of_liberty, burj_khalifa, etc...)
8. Add around 80% of the photos from each class to their respective folders in **train**, and the other 20% in their respective folder in **train**. Add around 10 images (any) in their respective folder.
9. Connect _filezilla_ to your jetson nano and rename the folder **wonders_of_the_world**.
10. Move the jetson-inference file into the nano through filezilla and then move the dataset 'wonders_of_the_world' into the directory **jetson-inference/python/training/classification/data**
11. Add a file called **labels.txt** in the **wonders_of_the_world** folder and have each line of the txt file have the classes you want to use in the order that they are in the files, e.g.

burj_khalifa

chichen_itza

christ_the_redeemer

13. Create a folder under models named **wonders_of_the_world**
15. Change directories to **jetson-inference/** in the VS Code terminal
16. Enter the docker by entering: `./docker/run.sh`
17. Enter this command to begin to train the model. Add ` --epochs=#` after the command, where # is the number of epochs you want the model to train itself with (preferably 35). Command: `python3 train.py --model-dir=models/wonders_of_the_world data/wonders_of_the_world` The model will train now and may take longer depending on the epoch amount entered.
18. Change directories to **jetson-inference/python/training/classification** in the docker.
19. Enter this command to run the onnx export script: `python3 onnx_export.py --model-dir=models/wonders_of_the_world`
20. Exit the docker by pressing _Ctrl + D_
21. Change to this directory: **jetson-inference/python/training/classification**
22. Set the NET and DATASET variables by entering these two consecutive commands: `NET=models/wonders_of_the_world` `DATASET=data/wonders_of_the_world`
23. Test the model by running this command: `imagenet.py --model=$NET/resnet18.onnx --input_blob=input_0 --output_blob=output_0 --labels=$DATASET/labels.txt $DATASET/test/burj_khalifa/ccae0e0415.jpg result.jpg` The bolded parts can be edited to any image desired, including images you can import from elsewhere. It is important to only take the images from the test folder.
24. Open the _result.jpg_ file that will be created and see the image with an added label of what monument it is on the top right and its confidence percentage.


[View a video explanation here](https://youtu.be/YxDQeJB-jog)
