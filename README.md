# Quora-Question-Pair
## Solution Approach
	
We partition the Quora question pairs into a 90/10 train/test split. We run training for 25 epochs with a further 90/10 train/validation split, saving the weights from the model checkpoint with the maximum validation accuracy. Training takes approximately 140 secs/epoch, using Tensorflow as a backend for Keras on an Amazon Web Services EC2 p2-xlarge GPU compute instance. We finally evaluate the best checkpointed model to obtain a test set accuracy of 0.8291. 

There are two files included in the repository. Those are described as follows: -

### Data_Prepration.ipynb

This notebook is used to prepare data for the model. The comments have been provided within the notebook to understand the working of each section of the notebook.
* This notebook starts with importing the necessary data.
* The Global Variables are declared like the URL of Quora Question Pair and that of the Word Embeddings. 
* Downloading and extracting the Question Pairs from the URL
* Running Tokenizer to add index to each word within the sentence
* Downloading and extracting Glove Word Embeddings from the URL and processing the downloaded data by counting the downloaded words within the dataset.
* Truncating the Word Embeddings that lie between 200D to 300D as we are going to use 200D matrix which is most accurate as mentioned in assumption.
* Preparing the Tensors for the Qustions and Labels for training purpose.
* Saving Tensors to file for future use in Model Training in Model_Train.ipynb

### Model_Train.ipynb

This notebook is used to prepare train the model. The comments have been provided within the notebook to understand the working of each section of the notebook.
* This notebook starts with importing the necessary data.
* The Global Variables are declared like name of the files in which the Tensors are defined.
* Data is loaded into the server memory for execution and training of model. The word count are stored into the Json file
* Partitioning the Dataset into Training and Testing sets for getting the information about the accuracy and loss that the model is going through.
* Model is defined as per the image shown in Technical Architecture
* Summary of the Model depicting the Tensors are shown within the notebook
* The best accuracy is recorded and the values corresponding the best accuracy is stored onto the tensors files.
* The result with best accuracy and the corresponding loss is shown within the notebook.

## Implementation Framework
###	General Implementation Approach: -

•	The Jupyter notebooks provided on the Github repository are needed to be uploaded on the Jupyter Server and then has to be executed in the order shown below: -

* Data_Prepration.ipynb – This file has to be executed first as this file will see prepare all the data required to train and evaluate the model.
* Model_Train.ipynb – This contains the neural layers which are going to be trained to find if the two question pairs are duplicate or not. 

###	Hardware and Software Details: -

•	We will require an AWS P2.xlarge instance of Deep Learning AMI (Ubuntu). We will run our model on GPU of this instance for faster processing. Advantage of using GPU can be seen as time taken per EPOCH as shown below:-

* CPU 	: ~942 seconds per EPOCH
* GPU	: ~141 seconds per EPOCH

•	We will require to create a separate Anaconda Environment with Keras-GPU installed in it. This will download all the dependencies including the Tensorflow-GPU as its backend. To install Keras-GPU in you environment perform the following steps: -

* conda create -n <env_name> python=3.6 anaconda
* source <env_name> activate
* conda install Keras-GPU

•	Now we can execute the model thorugh the Jupyter Notebook. You need to confi-gure the Jupyter notebook prior to execute it on server. The link to configure the Jupyter the notebook has been provided in the reference. You can launch the jupy-ter notebook using the following command

* jupyter notebook
