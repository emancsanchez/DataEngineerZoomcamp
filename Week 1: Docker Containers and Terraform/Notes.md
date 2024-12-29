# Week 1:
## Docker Containers

### Docker Containers
Installs appplications in packages called Containers

CSV Files >>> Data pipeline (Python Script >>> Table in Postgres  
(source) >>>       (processing)           >>> Destination


Containers run on a computer with separate entities or volumes

Producability = Docker image can be run on another computer or cloud computing  

Why to care about docker?
Reproduction  
Local Experimentation  
Integration Tests(CI/CD)  
Running Pipelines in thte cloud (AWS Batch, Kubernetes)  
Spark  
Serverless(AWS Lambda, Google Functions)  

##Working in the Terminal  

VSCode

```
VSCode ..
```

>docker run -it ubuntu bash

```
docker run <tags> <image> <comment or parameter>
```


tags  
-it (interactive mode)

```
docker run -it python:3.9
<image>:<version>
```

```
docker run -it --entrypoint=bash python:3.9
ENTERS docker from bash instead of from python module in order to run pip install pandas
```

Adding pandas to container image to run with pandas or any packages or dependency  

Dockerfile
```
FROM python:3.9

RUN pip install pandas

ENTRYPOINT [ "bash" ]

```

Now run:

```
docker build -t test
docker build <image name > : <image>
```

then  

```
docker run -it test:pandas
```

Create pipepline.py file:  
```
import pandas as pd

#code will be generated throughout course here

print('Job finished successfully')
```


UPDATE DOCKERFILE:

```
FROM python:3.9

RUN pip install pandas

WORKDIR /the/location/path
COPY pipeline.py pipeline.py
#COPY <source file> <copy to workdir named file>
ENTRYPOINT ['Python' , 'pipeline.py']
```


# <ins>END OF INTRO TO DOCKER</ins>

# <ins> Ingesting NY Taxi Data to Postgres </ins>

This is the docker comment to run in terminal:

```
docker run -it \
  -e POSTGRES=USER="root" \
  -e POSTGRES_PASSWORD="root" \
  -e POSTGRES_DB="ny_taxi" \
  -v $(pwd)/ny_taxi_postgres_data: /var/lib/postgressqp/data \
  -p 5432:5432 \
postgres:13
```








