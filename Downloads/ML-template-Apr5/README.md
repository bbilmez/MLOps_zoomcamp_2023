## Machine Learning Infrastructure Template

This template provides a machine learning infrastructure for hosting a Kedro project on a Prefect server. It allows you to schedule your Kedro pipelines to run on different Kubernetes configurations as well as allocating the GPU power of the workstation and scheduling training sessions.

## Usage


### Environment Variables

To use this template, create your own kedro pipelines in the src/kedro_mlflow_bentoml folder. Pipeline.py should register your kedro pipelines.

Then add the following environment variables to your gitlab or github variables/secrets. In Gitlab everything is a CI/CD variable. In GITHUB there is a difference for the variables and secrets.
GITHUB variables:
- IMAGE_REGISTRY: the name of the Docker registry where your image will be stored. If this is a private repository see ## private docker repo
- IMAGE_NAME: the name of your Docker image you want to create
- IMAGE_TAG: the tag for your Docker image
SECRETS:
- PROJECT_NAME: the name you want to give your project in the Prefect dashboard
- FLOW_NAME: The name you want to give the kedro pipelines in the prefect dashboard.
- PREFECT_API_KEY: The API key for the Prefect cloud
- DOCKERHUB_USERNAME: the username to login to the dockerhub
- DOCKERHUB_TOKEN: The token to logn to the dockerhub

To deploy this project to the prefect cloud and workstation: commit to gitlab or github with the env variables in the repo secrets.

## private docker repo
If you use a private docker repository follow [this](https://https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/) guide to add dockerconfig credentials to the kubernetes pod. Then add the `image_pull_secrets =[<your-secret-name>]` in the get_run_config() function in iris_example.py


## Allocating GPU power
You can change the kubernetes agent that will execute the flow by changing the value for labels in get_run_config(). A kubernetes agent corresponding to that label will execute the pipelines on the workstation.


### Contributing

If you'd like to contribute to this template, please follow these guidelines:
1. Fork the repository.
2. Create a new branch for your changes.
3. Make your changes and test them locally.
4. Push your changes to your forked repository.
5. Submit a pull request to the main repository.

### License

This template is licensed under: .....
