# ELM integration

In the thesis project I added a new computation type using the ELM API. This new computation allows you to train a Machine Learning model using previously tagged data

## Quick start

To use this computation, the ELM server must be active, and a POST call must be made, indicating the following parameters in the body: 

* <b>_id:</b> unique name chosen for the new computation,
* <b>code:</b> "model",
* <b>feature:</b> the feature you want to use,
* <b>filter:</b> the filter must always indicate the feature specified above and any other restrictions,
* <b>items:</b> the items of the feature that you want to use,
* <b>tags:</b> you have to specify the two tags for binary classification,
* <b>metadata:</b> metadata are the configuration parameters of ELM (see the ELM project).

Below is an example of computation done on a feature that has three items (temp_est, temp_int and hum_int), requesting that a LinearSVC model be trained

```
POST {{url}}/v1/computations
body
{
    "_id": "Model-1",
    "code": "model",
    "filter": "{\"feature\":\"smartHomeFeature\"}",
    "feature": "smartHomeFeature",
    "items": ["temp_int","hum_int","temp_est"],
    "tags": ["empty","detection"],
    "metadata": {
        "est": "{\"estimator\": \"LinearSVC\",\"C_exp_lowerlimit\":-3,\"C_exp_upperlimit\":2,\"C_exp_step\":2}"
    }
}
```