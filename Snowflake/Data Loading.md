# Table create
 create or replace schema.table_name
 (
 field_1 integer, 
 field_2 varchar(10),
 field_3 boolean
 ) ;

# Snowflake batch load using snowsql

snowsql -a account_name -u user_name -d database_name -w warehouse_name -D variable_name=variable_value -f file_name_with_path -o options

password can be set in environment using SNOWSQL_PWD

# Copy into snowflake Stage table

copy into stage_schema.stage_table
from @external_stage_location
FILE_FORMAT=(type=csv field_delimiter = ',' ) ON_ERROR=ABORT_STATEMENT TRUNCATECOLUMNS=TRUE;

# Insert into Main table

insert into main_schema.main_table
(
field_1,
field_2,
field_3
)
select
field_1,
field_2,
field_3
from stage_schema.stage_table
