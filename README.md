# Predicting Miles Per Gallon

Machine Learning Deployment Using Docker and Kubernetes.

### Setup & Installation

- Download Google Cloud SDK
- Create Kubernetes Cluster
- After cluster is created, connect the cluster to the local terminal.

### Making a Sample Project
- Training a Random Forest Model

Import the packages and classes from the core folder. Then substantiate the classes, such that we can call all functions from the classes later on. Next step is loading dataset  into dataframe, which we provided a function for in the LoadData class.  When we call the function, we use Pandas to read a data table, and then we specify the column names from  the class. The CleanData class has a function for this, where we specify the dataframe to only contain the rows where horsepower does not contain a question mark – in other      words, it removes the rows where horsepower has a question mark instead of a number. The next and last step before training our model is specifying which feature we want to predict. Naturally, for this dataset at least, we want to predict the mpg feature, which is miles per gallon for a car.

Split the dataset into training and testing (Y- feature trying to predict and X is the features we are using to predict Y). Random Forest with default parameters, and then Scikit-learn to train a random forest model with the training data. After that is done,predict on the testing data, and we can also score how well the predictions went. The absolute last step is "dumping" the model, which means exporting it to a file, that we can load into Python at another point in time. For this, we use joblib.

### Making Models accessible through a service

- To expose as a service, created a flask app. After we run this code, doesnt expose it to the world yet. So we need a cloud provider, this is the entrypoint to the application. This is packaged and shipped to the GCP.

### Deployment with Docker & Kubernetes

- Created a dockerfile and built the image 

### Building and pushing an image to the cloud

- Just change the project ID on the bash script(build_push_image.sh) annd run this script

### Deploying with Kubernetes

- The image is now built and pushed to the cloud. To be able to run, created deployment and service YAML files
- When we apply this deployment, specified for kubernetes to create 3 replicas(Pods). So the application is running in the cloud, but it's not exposed yet.
- Service YAML file is created to expose the application, specified the type - Load Balancer. The port is set to 80, because that defaults to just the external-ip address, while the targetPort is set to 5000, since that is what we specified in the deployment file and Flask application.

### How do I access my application?
- Access the application through external-ip from the service. Machine Learning model is ready to serve predictions at an endpoint.

### Making a request to the application
- External IP from earlier, which we are going to resue. The following JSON request can be sent as HTTP POST Method and recieve expected response.
  
  In just 0.29 seconds, we received the prediction of this car, and our machine learning model predicted 16.383.
  

An example of input to Flask service in main.py:

```json
{
    "cylinders": 8,
    "displacement": 307.0,
    "horsepower": 130.0,
    "weight": 3504,
    "acceleration": 12.0,
    "model_year": 70,
    "origin": 1,
    "car_name": "chevrolet chevelle malibu"
}
```



