
# ML Pipeline
An end to end machine learning classification model trained using Random Forest.

## Debugging.  
* When developing, you can override the parameter ``main.execute_steps`` to only execute one or
  more steps of the pipeline, instead of the entire pipeline. 
  For example, this only executes the ``random_forest`` step:
  ```bash
  mlflow run . -P hydra_options="main.execute_steps='random_forest'"
  ```
  and this executes ``download`` and ``preprocess``:
  ```bash
  mlflow run . -P hydra_options="main.execute_steps='download,preprocess'"
  ```

## Run Production version
upload results to wandb
`mlflow run . -P hydra_options="main.project_name=genre_classification_prod"`
then change artifact release alias to prod.

## Pipeline Graphical Overview
![graph](./images/graphical_view.JPG)

## Sample Output
**Feature Importance**

![features](./images/feature_importance_0_f1fd3194.png)

## Run the release

`mlflow run https://github.com/1ayham1/genre_classification.git -v 1.0.0 -P hydra_options="main.project_name=remote_execution" `

## Deployment
`wandb artifact get genre_classification_prod/model_export:prod --root model`

### Offline inference
` wandb artifact get genre_classification_prod/data_test.csv:latest `

then
```
mlflow models predict \
                -t csv \
                -i ./artifacts/data_test.csv:v0/data_test.csv \
                -m model
```

