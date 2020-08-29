# Deploy_classification_model

Here I trained a model using TF Hub. The model is pre trained on 7B data. The dataset is on a sentiment classification of food, where `-1` means negative review, `0` means nutral and `+1` means positive review. The pre trained model will take care of our model.    
After downloading the data you can run the whole notebook. The model will be created in `model_checkpoint` folder, where the best model will be saved along with the weights. The model will be exported in the `amazon_review` folder, there will be a folder based on the time frame you are running the notebook. You can find it from there.     

Beside docker tensorflow serving supports     
+ Remote Procedure Protocal (gRPC)
+ Representational State Transfer (REST)     

Default ports    
+ RPC: 8500
+ REST: 8501

### Data
The dataset can be found *[here](https://www.kaggle.com/snap/amazon-fine-food-reviews/data)*

### Deploy
open a cmd and cd over to the `Deploy_classification_model`     
Run this in  cmd    
1. Docker     
    1. `docker pull tensorflow/serving`      
    2. `docker run -p 8500:8500 -p 8501:8501 --mount type=bind,source=/path/amazon_review/,target=/models/amazon_review -e MODEL_NAME=amazon_review -t tensorflow/serving`     
2. Rest    
`python3 tf_serving_rest_client.py`   
it will run the model and let us type the comment manually.    
Default port `http://{HOST}:{PORT}/v1/models/{MODEL_NAME}`     
Specified port `http://{HOST}:{PORT}/v1/models/{MODEL_NAME}[/versions/{MODEL_VERSION}]:predict`    
3. gRPC    
`python3 tf_serving_grpc_client.py`    
it will run the model and let us type the comment manually.    


