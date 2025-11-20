# mlfs-book
O'Reilly book - Building Machine Learning Systems with a feature store: batch, real-time, and LLMs


## ML System Examples


[Dashboards for Example ML Systems]([https://featurestorebook.github.io/mlfs-book/](https://kkkkkkatherine01.github.io/air-quality-prediction/air-quality/))

    
# Create a conda or virtual environment for your project before you install the requirements
    pip install -r requirements.txt


##  Run pipelines with make commands

    make aq-backfill
    make aq-features
    make aq-train
    make aq-inference
    make aq-clean

or 
    make aq-all



## Feldera


mkdir -p /tmp/c.app.hopsworks.ai
ln -s  /tmp/c.app.hopsworks.ai ~/hopsworks
docker run -p 8080:8080 \
  -v ~/hopsworks:/tmp/c.app.hopsworks.ai \
  --tty --rm -it ghcr.io/feldera/pipeline-manager:latest


## Introduction to ML
I wrote a brief introduction to machine learning [here](./introduction_to_supervised_ml.pdf)
