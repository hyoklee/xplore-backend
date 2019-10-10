# Refer https://github.com/sairahul/classify for latest version

# Usage Instructions

## Running without the docker image.  

Install the dependencies in backend.dockerfile file and run the following command from
backend/app directory 

```
SQLITE_DB="sqlite:////Users/pulikunt/myfiles/xplore/classify/backend/db.sqlite" uvicorn app.main:app --reload 
```

## Database Migrations

Generates migrations

```
alembic revision --autogenerate -m "Added a new table"
```

Running first time (tables not created) or After any addition/deletion/modification of tables

```
alembic upgrade head
```

## Adding a new dataset

```
python scripts/add_dataset.py --name pneumothorax --base-dir /Users/pulikunt/myfiles/xplore/datasets/siim-acr-pneumothorax-segmentation/original --thumbnail-dir /Users/pulikunt/myfiles/xplore/datasets/siim-acr-pneumothorax-segmentation/thumbnails
```


## Docs

```
http://localhost:8000/docs#/datasets/
```

## Docker building
```
docker build --tag=xplore-backend -f backend.dockerfile .
docker run -e "SQLITE_DB=sqlite:////data/db.sqlite" -e "FIRST_SUPERUSER=" -e "FIRST_SUPERUSER_PASSWORD=" -e "WORKERS_PER_CORE=0.125" -p 8000:8000 -v /data/xplore_data:/data xplore-backend
```

Use env file to run
```
docker run  --env-file=backend.env -p 8000:80 -v /data/xplore_data:/data xplore-backend
```

