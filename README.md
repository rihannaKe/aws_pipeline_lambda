
# TASK 2: BACKEND APPLICATION IMPLEMENTATION

This repo contains the the deliverable for a backend solution exposing the requested metrics. It serves the output of the following computations:
- the average monthly value from 1st of June 2022 to 1st of July 2023 metrics for each ADM1 areas of Colombia and Burkina Faso (metric A)
- The daily national estimate for the FCS prevalence from 1st of June 2022 to 1st of July 2023
(metric B) and its variance

## Used tech stack
I used an AWS lambda function for the backend implementation. The choice of using a sererless approch, instead of using a server and backend python API development using  e.g Flask API, relies on choosing to leverage the Servless computation as it is cost saving, easily scalabile.
The backend service is avaible at the following endpoint: https://byyp3wv7otj6cmoxmksgwz5bze0pocum.lambda-url.eu-central-1.on.aws/
The endpoint return a json object of the requested metrics as follows:
---
{
    "COL": {
    "metric_a": [
        "average": {
            "2022-6": {"people": 790956.53,"prevalence": 0.12},
            ...
        }],
    }
    "metric_b": {
        "2022-06-01": {"people": 5712364,"prevalence": 0.11,"variance": 0.01}
        ...
    },
    "BFA": {
        "metric_a": [...],
        "metric_b": {...}
    }
}
---

### Deployment
The deployment of the code is automized and the used CI/CD approch is shown in the above figure
![CI/CD](./static_assets/ci_cd_diagram.png)

I used the AWS codeBuild service. Whenever we push the code to github, an automatic build and deploy will follow.
For more complete CI/CD with staging and testing, it can be extended to use AWS Code pipeline service.

### Code
Here is a list of the main files and their usage 
- **lambda_function.py** contains all the necessery code used to compute and deliver the output of the requested metrics
- **iam-policy.json** contains policy to add foir the CodeBuild service
- **buildspec.yml** file will first install the dependencies for the Lambda function code. Then, it will zip up the Lambda function code and deploy it to AWS Lambda.

