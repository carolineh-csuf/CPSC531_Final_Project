# Distributed Image Classification with Hadoop and Spark
# CPSC531_Final_Project

This project implements distributed image classification on a Hadoop cluster, leveraging HDFS for storage and Apache Spark for data processing. The MNIST dataset is used to train a three-layer CNN model built with PyTorch. The training process uses PyTorch Distributed Data Parallel (DDP) for parallel processing across multiple CPUs, showcasing the integration of Hadoop, Spark, and deep learning techniques in distributed environments.

## Features
- **Distributed Data Storage:** Utilizes HDFS to store and distribute the MNIST dataset and model dependencies.
- **Parallel Processing:** Employs Apache Spark for managing parallel execution across multiple nodes.
- **Deep Learning with PyTorch:** Implements a three-layer CNN trained using PyTorch DDP.
- **Efficient Model Training:** Achieves accurate classification of MNIST images with distributed resources.

## Prerequisites
- Hadoop installed and configured
- Apache Spark installed and configured
- PyTorch installed with support for Distributed Data Parallel
- MNIST dataset uploaded to the Hadoop directory `/user/MNIST`

## Directory Setup
- MNIST dataset: `/user/MNIST`
- Python script: `/user/hadoop/MNIST_SPARK_DDP_Demo.py`
- Dependencies (zipped): `/user/hadoop/libs.zip`

## Job Submission (Standalone Mode)
Use the following command to submit the Spark job:

```bash
spark-submit --verbose \
  --master spark://localhost:7077 \
  --deploy-mode client \
  --num-executors 6 \
  --executor-memory 4G \
  --conf spark.executorEnv.MASTER_ADDR=localhost \
  --conf spark.executorEnv.MASTER_PORT=12345 \
  --conf spark.executorEnv.WORLD_SIZE=6 \
  --py-files hdfs://localhost:9000/user/hadoop/libs.zip \
  hdfs://localhost:9000/user/hadoop/MNIST_SPARK_DDP_Demo.py
