### Udacity Data Engineer Nanodegree project
A music streaming startup, Sparkify, has grown their user base and song database and want to move their processes and data onto the cloud. Their data resides in S3, in a directory of JSON logs on user activity on the app, as well as a directory with JSON metadata on the songs in their app.

As their data engineer, you are tasked with building an ETL pipeline that extracts their data from S3, stages them in Redshift, and transforms data into a set of dimensional tables for their analytics team to continue finding insights in what songs their users are listening to. 

### Requirements for running
- Python3 
- AWS account
- Configured aws credentials file (https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-configure.html)


### Instructions for running locally

Clone repository to local machine
```
git clone https://github.com/brfulu/redshift-data-modeling.git
```

Change directory to local repository
```
cd redshift-data-modeling
```

Create python virtual environment
```
python3 -m venv venv             # create virtualenv
source venv/bin/activate         # activate virtualenv
pip install -r requirements.txt  # install requirements
```

Go to source directory
```
cd src/
```

Create Redshift cluster
```
python -m scripts.create_cluster # take note of Endpoint, Role_ARN and Security_Group output
```

Edit dwh.cfg file
```
HOST=<ENTER REDSHIFT ENDPOINT>   # paste Endpoint output from script above
ARN='<ENTER REDSHIFT ROLE ARN>'  # paste Role_ARN from script above (leave quotes)
SG_ID=<ENTER SECURITY GROUP ID>  # paste sg_id from output above
```

Create schema
```
python -m scripts.create_tables
```

Execute ETL
```
python -m scripts.etl # load data into staging tables, transform and load into fact and dim tables
```

Check results

```
jupyter notebook  # launch jupyter notebook app

# The notebook interface will appear in a new browser window or tab.
# Navigate to src/notebooks/test.ipynb and run sql queries against Redshift
```

Delete cluster
```
python -m scripts.delete_cluster
```
