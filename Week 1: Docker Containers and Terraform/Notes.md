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
  -e POSTGRES_USER="root" \
  -e POSTGRES_PASSWORD="root" \
  -e POSTGRES_DB="ny_taxi" \
  -v $(pwd)/ny_taxi_postgres_data: /var/lib/postgressqp/data \
  -p 5432:5432 \
postgres:13
```


Connecting to postgres database and sending to postgres database:

sqlalchemy, import create engine, create an engine that links to database in format:  


```
from sqlalchemy import create_engine

engine = create_engine('<database server>://<username>:<password>@<localhost>:<port>/<database name>')
```

while this established connection, no feedback if it works, in order to check connection run:

```
engine.connect()
```

In pandas, connection can be established using:

```
pd.io.sql.get_schema(<dataframe>, name='<name of database>', con=<engine)
```

Converting columns to timestamps specifically the tpep_pickup_datetime and tpep_droppoff_datetime:

```
df.tpep_pickup_datetime = pd.to_datetime(df.tpep_pickup_datetime)
df.tpep_dropoff_datetime = pd.to_datetime(df.tpep_dropoff_datetime)
```



Iterator:

```
df_iter = pd.read_csv('yellow_tripdata_2021-01.csv', iterator=True, chunksize=1000000)

df = next(df_iter)

#creating table in postgres

df.head(n=0).to_sql(name='yellow_taxi_data', con=engine, if_exists = 'replace')
INSERTS header for table with table name

df.to_sql(name='yellow_taxi_data', con = engine, if_exists='append'
```



Now in order to load the whole 1.03 million row data set, run while loop:  
Various print statements also help with error handling and figuring out timing etc.

```
while True:
  t_start = time()
  df = next(df_iter)
  df.tpep_pickup_datetime = pd.to_datetime(pd.tpep_pikckup_datetime)
  df.tpep_dropoff_datetime = pd.to_datetime(pd.tpep_dropoff_datetime)

  df.to_sql(name='yellow_taxi_data', con=engine, if_exists='append')

  t_end = time()

  print(insert another cunk, took %.3f second' % (t_end - t_start)
```


Convert this ingestion notebook script into python script:

```
jupyter nbconvert --to=script <name of script to be converted>.py
jupyter nbconvert --to=script ingestion_script.ipynb
```

subsequently converts it to .py file


docker compose:  

docker-compose.yaml:  

```
services:
  pgdatabase:
    image: postgres13
    environment:
      -POSTGRES_USER=root
      -POSTGRES_PASSWORD=root
      -POSTGES_DB=ny_taxi
    volumes:
      - "./ny_taxi_postgres_data:/var/lib/postgresql/data:rw"
    ports:
    - "5432:5432"
  pgadmin:
    image: dpage/pgadmin4
    environtment:
      -PGADMIN_DEFAULT_EMAIL = admin@admin.com
      -PGADMIN_DEFAULT_PASSWORD = root
    ports:
      - "8080:80"
```

Now, run docker compose up to bring up the container with the network,
then run docker compose down to shut dodwn the container and network.







