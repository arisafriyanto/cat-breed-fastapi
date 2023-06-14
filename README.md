<h1 align="center">Cat Breed API Documentation</h1>

## How to setup and run locally

1. Clone repository following this command
   <pre>git clone https://github.com/arisafriyanto/cat-breed-fastapi.git</pre>
2. Install python3 (>3.9 or latest)
3. Install pip (>18.1 or latest)
4. Install requirements.txt
   <pre>pip install -r requirements.txt</pre>
5. Change path directory in main.py
   - Load a TensorFlow model that has been saved in the models folder
   - Define the path model   
   <pre>
    model_path = "/path/models"
   </pre>
6. Run app
   <pre>uvicorn main:app --host localhost --port 8080</pre>
7. Test the API using Postman with POST Method, route http://localhost:8080/predict and request body form-data
   - Change key type to `file`
   - select an image from your computer
   <pre>
     key: image_file
     value: Select Files
   </pre>


## How to setup with Google Cloud Platform using Cloud Run
### What you need
1. Cloud Environment: Google Cloud Platform (Cloud Run)
2. Programming Language: Python
3. Web Server: FastAPI (Rest Api)
4. Serverless: Cloud Run

### Next steps
1. Open cloud shell and set the project id
   <pre>gcloud config set project PROJECT_ID</pre>
2. Clone repository following this command
   <pre>git clone https://github.com/arisafriyanto/cat-breed-fastapi.git</pre>
3. Open the app folder
   <pre>cd cat-breed-fastapi/</pre>
4. Change path directory in main.py
   <pre>model_path = "/app/models"</pre>
5. Change host from `localhost` to `0.0.0.0` in main.py
   <pre>
    if __name__ == "__main__":
    uvicorn.run(app, host="0.0.0.0", port=8080)
   </pre>
5. Build docker image manual
   <pre>docker buildx build --platform linux/amd64 -t fastapi-ml-model:v1 .</pre>
6. View the results of a successfully created docker image
   <pre>docker image ls</pre>
7. Tag a Docker image with a specific label
   <pre>docker tag {id} gcr.io/{PROJECT_ID}/fastapi-ml-model:v1</pre>
8. Push the docker image to the container registry
   <pre>docker push gcr.io/{PROJECT_ID}/fastapi-ml-model:v1</pre>
9. Create a service in the Cloud Run, select the previously deployed docker image in the container registry, set port to 8080, adjust other configurations and deploy.