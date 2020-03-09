# Great Expectations Pipeline 
End-to-end project with dbt, GE, airflow for the purpose of demonstrating how to implement Great Expectations alongside dbt and airflow.
## Setup

some basic setup steps.

### Database setup
 we need a  relational database available that can be accessed using a SQLAlchemy connection URL. We developed the tutorial using a postgres database. 

### Install and configure tools
* airflow - run `airflow initdb`, set up `$AIRFLOW_HOME` and point the dags_folder in airflow.cfg to the project path
* dbt - set up your database connection in the dbt_profile.yml (see the example_dbt_profile.yml in this project)
* great_expectations - no further setup needed

### Environment variables

The pipeline's configuration variables are passed using environment variables. Set the following variables:
* `export GE_TUTORIAL_DB_URL=postgresql://your_user:your_password@your_dh_host:5432/your_db_name`
* `export GE_TUTORIAL_PROJECT_PATH=your_project_path`


## Pipeline overview
Follows the ELT Pattern. It loads data from files into a database and then transforms it. 
The pipeline simply takes two data input files and processes them in a WAP (write - audit - publish) type pattern:
1. Use GE to validate the input CSV files. Stop if they do not meet our expectations 
2. Load the source files to a postgres database using SQLAlchemy
3. Use GE to validate that the data was loaded into the database successfully
4. Use GE to validate the analytical result.
5. If the analytical result is valid, publish (promote) the analytical table to a "prod" table by renaming it

The entire pipelin is orchestrated with the following airflow DAG:

## Running the pipeline

TBD
