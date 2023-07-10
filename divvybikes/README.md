repository to stream the divvy bikes data and setup the pipeline for inferencing. 

- Create schema.yaml for the project
- run the create_schema.ipynb notebook to load the schema to minio
- run the feature-extractor.ipynb to start the feature extractor, without this, training and inferencing might not work
- run steps in import.ipynb notebook, this will start the ingesting of dataset to pipeline.
    - If a model exist, you will already start seeing the prediction in the integration pod, otherwise proceed with train.ipynb
- run the steps in train.ipynb notebook to train the model and save it on minio. Once model is saved new data streamed will have predictions logged in the integration pod automatically.
- These predictions can also be seen in the grafana dashboard.


