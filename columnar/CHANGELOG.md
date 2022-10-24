### citus v11.0.1_beta (April 11, 2022) ###

* Adds propagation of `DOMAIN` objects

* Adds support for `TABLESAMPLE`

* Allows adding a unique constraint with an index

* Fixes a bug that could cause `EXPLAIN ANALYZE` to fail for prepared statements
  with custom type

* Fixes a bug that could cause Citus not to create function in transaction block
  properly

* Fixes a bug that could cause returning invalid JSON when running
  `EXPLAIN ANALYZE` with subplans

* Fixes a bug that prevents non-client backends from accessing shards

### citus v11.0.0_beta (March 22, 2022) ###

* Drops support for PostgreSQL 12

* Turns metadata syncing on by default

* Adds `citus_finalize_upgrade_to_citus11()` which is necessary to upgrade to
  Citus 11+ from earlier versions

* Adds `citus.max_client_connections` GUC to limit non-Citus connections

* Allows locally creating objects having a dependency that cannot be distributed

* Distributes aggregates with `CREATE AGGREGATE` command

* Distributes functions with `CREATE FUNCTION` command

* Adds `citus.create_object_propagation` GUC to control DDL creation behaviour
  in transactions

* Hides shards based on `application_name` prefix

* Prevents specifying `application_name` via `citus.node_conninfo`

* Starts identifying rebalancer backends by `application_name=citus_rebalancer`

* Starts identifying internal backends by `application_name=citus_internal`

* Adds `citus.enable_unsafe_triggers` flag to enable unsafe triggers on
  distributed tables

* Adds `fix_partition_shard_index_names` UDF to fix currently broken names

* Adds propagation for foreign server commands

* Adds propagation of `TEXT SEARCH CONFIGURATION` objects

* Adds propagation of `TEXT SEARCH DICTIONARY` objects

* Adds support for `ALTER FUNCTION ... SUPPORT ...` commands

* Adds support for `CREATE SCHEMA AUTHORIZATION` statements without schema name

* Adds support for `TRUNCATE` for foreign tables

* Adds support for adding local tables to metadata using
  `citus_add_local_table_to_metadata()` UDF

* Adds support for adding partitioned local tables to Citus metadata

* Adds support for automatic binary encoding in re-partition joins when possible

* Adds support for foreign tables in MX

* Adds support for operator class parameters in indexes

* Adds support for re-partition joins in transaction blocks

* Adds support for re-partition joins on followers

* Adds support for shard replication > 1 hash distributed tables on Citus MX

* Improves handling of `IN`, `OUT` and `INOUT` parameters for functions

* Introduces `citus_backend_gpid()` UDF to get global pid of the current backend

* Introduces `citus_check_cluster_node_health` UDF to check cluster connectivity

* Introduces `citus_check_connection_to_node` UDF to check node connectivity

* Introduces `citus_coordinator_nodeid` UDF to find the node id of the
  coordinator node

* Introduces `citus_stat_activity` view and drops `citus_worker_stat_activity`
  UDF

* Introduces `citus.use_citus_managed_tables` GUC to add local tables to Citus
  metadata automatically

* Introduces a new flag `force_delegation` in `create_distributed_function()`

* Allows `create_distributed_function()` on a function owned by an extension

* Allows creating distributed tables in sequential mode

* Allows disabling nodes when multiple failures happen

* Adds support for pushing procedures with `OUT` arguments down to the worker
  nodes

* Overrides `pg_cancel_backend()` and `pg_terminate_backend()` to run with
  global pid

* Delegates function calls of the form `SELECT .. FROM func()`

* Adds propagation of `CREATE SCHEMA .. GRANT ON SCHEMA ..` commands

* Propagates `pg_dist_object` to worker nodes

* Adds propagation of `SCHEMA` operations

* Adds missing version-mismatch checks for columnar tables

* Adds missing version-mismatch checks for internal functions

* `citus_shard_indexes_on_worker` shows all local shard indexes regardless of
  `search_path`

* `citus_shards_on_worker` shows all local shards regardless of `search_path`

* Deprecates inactive shard state, never marks any placement inactive

* Disables distributed & reference foreign tables

* Prevents propagating objects having a circular dependency

* Prevents propagating objects having a dependency to an object with unsupported
  type

* Deprecates `master_get_table_metadata` UDF

* Disallows remote execution from queries on shards

* Drops `citus.enable_cte_inlining` GUC

* Drops `citus.single_shard_commit_protocol` GUC, defaults to 2PC

* Drops support for `citus.multi_shard_commit_protocol`, always use 2PC

* Avoids unnecessary errors for `ALTER STATISTICS IF EXISTS` when the statistics
  does not exist

* Fixes a bug that causes columnar storage pages to have zero LSN

* Fixes a bug that causes issues while create dependencies from multiple
  sessions

* Fixes a bug that causes reading columnar metapage as all-zeros when
  writing to a columnar table

* Fixes a bug that could break `DROP SCHEMA/EXTENSON` commands when there is a
  columnar table

* Fixes a bug that could break pg upgrades due to missing `pg_depend` records
  for columnar table access method

* Fixes a bug that could cause `CREATE INDEX` to fail for expressions when using
  custom `search_path`

* Fixes a bug that could cause `worker_save_query_explain_analyze` to fail on
  custom types

* Fixes a bug that could cause failed re-partition joins to leak result tables

* Fixes a bug that could cause prerequisite columnar table access method
  objects being not created during pg upgrades

* Fixes a bug that could cause re-partition joins involving local shards to fail

* Fixes a bug that limits usage of sequences in non-int columns

* Fixes a bug that prevents `DROP SCHEMA CASCADE`

* Fixes a build error that happens when `lz4` is not installed

* Fixes a clog lookup failure that could occur when writing to a columnar table

* Fixes a crash that occurs when the aggregate that cannot be pushed-down
  returns empty result from a worker

* Fixes a missing `FROM` clause entry error

* Fixes a possible segfault that could happen when reporting distributed
  deadlock

* Fixes an issue that could cause unexpected errors when there is an in-progress
  write to a columnar table

* Fixes an unexpected error that occurs due to aborted writes to a columnar
  table with an index

* Fixes an unexpected error that occurs when writing to a columnar table created
  in older version

* Fixes issue when compiling Citus from source with some compilers

* Fixes issues on `ATTACH PARTITION` logic

* Fixes naming issues of newly created partitioned indexes

* Improves self-deadlock prevention for `CREATE INDEX / REINDEX CONCURRENTLY`
  commands for builds using PG14 or higher

* Moves `pg_dist_object` to `pg_catalog` schema

* Partitions shards to be co-located with the parent shards

* Prevents Citus table functions from being called on shards

* Prevents creating distributed functions when there are out of sync nodes

* Provides notice message for idempotent `create_distributed_function` calls

* Reinstates optimisation for uniform shard interval ranges

* Relaxes table ownership check to privileges check while acquiring lock

* Drops support for `citus.shard_placement_policy` GUC

* Drops `master_append_table_to_shard` UDF

* Drops `master_apply_delete_command` UDF

* Removes copy into new shard logic for append-distributed tables

* Drops support for distributed `cstore_fdw` tables in favor of Citus
  columnar table access method

* Removes support for dropping distributed and local indexes in the same
  statement

* Replaces `citus.enable_object_propagation` GUC with
  `citus.enable_metadata_sync`

* Requires superuser for `citus_add_node()` and `citus_activate_node()` UDFs

* Revokes read access to `columnar.chunk` from unprivileged user

* Disallows unsupported lateral subqueries on distributed tables

* Stops updating shard range in `citus_update_shard_statistics` for append
  tables

### citus v10.2.5 (March 15, 2022) ###

* Fixes a bug that could cause `worker_save_query_explain_analyze` to fail on
  custom types

* Fixes a bug that limits usage of sequences in non-integer columns

* Fixes a crash that occurs when the aggregate that cannot be pushed-down
  returns empty result from a worker

* Improves concurrent metadata syncing and metadata changing DDL operations

### citus v10.2.4 (February 1, 2022) ###

* Adds support for operator class parameters in indexes

* Fixes a bug with distributed functions that have `OUT` parameters or
  return `TABLE`

* Fixes a build error that happens when `lz4` is not installed

* Improves self-deadlock prevention for `CREATE INDEX` &
  `REINDEX CONCURRENTLY` commands for builds using PG14 or higher

* Fixes a bug that causes commands to fail when `application_name` is set

### citus v10.1.4 (February 1, 2022) ###

* Adds missing version checks for columnar tables

* Fixes a bug that could break `DROP SCHEMA/EXTENSION` commands when there is
  a columnar table

* Fixes a build error that happens when `lz4` is not installed

* Fixes a missing `FROM` clause entry error

* Reinstates optimisation for uniform shard interval ranges

* Fixes a bug that causes commands to fail when `application_name` is set

### citus v10.2.3 (November 29, 2021) ###

* Adds `fix_partition_shard_index_names` udf to fix currently broken
  partition index names

* Fixes a bug that could break `DROP SCHEMA/EXTENSION` commands when there is
  a columnar table

* Fixes a bug that could break pg upgrades due to missing `pg_depend` records
  for columnar table access method

* Fixes a missing `FROM` clause entry error

* Fixes an unexpected error that occurs when writing to a columnar table
  created in older versions

* Fixes issue when compiling Citus from source with some compilers

* Reinstates optimisation for uniform shard interval ranges

* Relaxes table ownership check to privileges check while acquiring lock

### citus v10.0.6 (November 12, 2021) ###

* Adds missing version checks for columnar tables

* Fixes a bug that caused `worker_append_table_to_shard` to write as superuser

* Fixes a bug with local cached plans on tables with dropped columns

* Fixes a missing `FROM` clause entry error

* Fixes a use after free issue that could happen when altering a distributed
  table

* Reinstates optimisation for uniform shard interval ranges

### citus v9.5.10 (November 8, 2021) ###

* Fixes a release problem in 9.5.9

### citus v9.5.9 (November 8, 2021) ###

* Fixes a bug preventing `INSERT SELECT .. ON CONFLICT` with a constraint name
  on local shards

* Fixes a bug with local cached plans on tables with dropped columns

* Fixes a crash in queries with a modifying `CTE` and a `SELECT`
  without `FROM`

* Fixes a missing `FROM` clause entry error

* Fixes a missing intermediate result when coordinator is in metadata

* Reinstates optimisation for uniform shard interval ranges

### citus v9.2.8 (November 4, 2021) ###

* Adds a configure flag to enforce security

### citus v9.2.7 (November 3, 2021) ###

* Fixes `ALTER TABLE IF EXISTS SET SCHEMA` with non-existing table bug

* Fixes `CREATE INDEX CONCURRENTLY` with no index name on a postgres table bug

* Fixes a bug that could cause crashes with certain compile flags

* Fixes a crash because of overflow in partition id with certain compile flags

* Fixes a memory leak in subtransaction memory handling

* Fixes deparsing for queries with anonymous column references

### citus v10.2.2 (October 14, 2021) ###

* Fixes a bug that causes reading columnar metapage as all-zeros when
  writing to a columnar table

* Fixes a bug that could cause prerequisite columnar table access method
  objects being not created during pg upgrades

* Fixes a bug that could cause `CREATE INDEX` to fail for expressions when
  using custom `search_path`

* Fixes an unexpected error that occurs due to aborted writes to a columnar
  table with an index

### citus v10.2.1 (September 24, 2021) ###

* Adds missing version-mismatch checks for columnar tables

* Adds missing version-mismatch checks for internal functions

* Fixes a bug that could cause partition shards being not co-located with
  parent shards

* Fixes a bug that prevents pushing down boolean expressions when using
  columnar custom scan

* Fixes a clog lookup failure that could occur when writing to a columnar table

* Fixes an issue that could cause unexpected errors when there is an
  in-progress write to a columnar table

* Revokes read access to `columnar.chunk` from unprivileged user

### citus v10.1.3 (September 17, 2021) ###

* Fixes a bug that caused `worker_append_table_to_shard` to write as superuser

* Fixes a crash in shard rebalancer when no distributed tables exist

* Fixes a use after free issue that could happen when altering a distributed
  table

### citus v9.5.8 (September 15, 2021) ###

* Fixes a bug that caused `worker_append_table_to_shard` to write as superuser

* Fixes a use after free issue that could happen when altering a distributed
  table

### citus v10.2.0 (September 14, 2021) ###

* Adds PostgreSQL 14 support

* Adds hash & btree index support for columnar tables

* Adds helper UDFs for easy time partition management:
  `get_missing_time_partition_ranges`, `create_time_partitions`, and
  `drop_old_time_partitions`

* Adds propagation of ALTER SEQUENCE

* Adds support for ALTER INDEX ATTACH PARTITION

* Adds support for CREATE INDEX ON ONLY

* Allows more graceful failovers when replication factor > 1

* Enables chunk group filtering to work with Params for columnar tables

* Enables qual push down for joins including columnar tables

* Enables transferring of data using binary encoding by default on PG14

* Improves `master_update_table_statistics` and provides distributed deadlock
  detection

* Includes `data_type` and `cache` in sequence definition on worker

* Makes start/stop_metadata_sync_to_node() transactional

* Makes sure that table exists before updating table statistics

* Prevents errors with concurrent `citus_update_table_statistics` and DROP table

* Reduces memory usage of columnar table scans by freeing the memory used for
  last stripe read

* Shows projected columns for columnar tables in EXPLAIN output

* Speeds up dropping partitioned tables

* Synchronizes hasmetadata flag on mx workers

* Uses current user while syncing metadata

* Adds a parameter to cleanup metadata when metadata syncing is stopped

* Fixes a bug about int and smallint sequences on MX

* Fixes a bug that cause partitions to have wrong distribution key after
  DROP COLUMN

* Fixes a bug that caused `worker_append_table_to_shard` to write as superuser

* Fixes a bug that caused `worker_create_or_alter_role` to crash with NULL input

* Fixes a bug that causes pruning incorrect shard of a range distributed table

* Fixes a bug that may cause crash while aborting transaction

* Fixes a bug that prevents attaching partitions when colocated foreign key
  exists

* Fixes a bug with `nextval('seq_name'::text)`

* Fixes a crash in shard rebalancer when no distributed tables exist

* Fixes a segfault caused by use after free in when using a cached connection

* Fixes a UNION pushdown issue

* Fixes a use after free issue that could happen when altering a distributed
  table

* Fixes showing target shard size in the rebalance progress monitor

### citus v10.1.2 (August 16, 2021) ###

* Allows more graceful failovers when replication factor > 1

* Fixes a bug that causes partitions to have wrong distribution key after
  `DROP COLUMN`

### citus v10.0.5 (August 16, 2021) ###

* Allows more graceful failovers when replication factor > 1

* Fixes a bug that causes partitions to have wrong distribution key after
  `DROP COLUMN`

* Improves citus_update_table_statistics and provides distributed deadlock
  detection

### citus v9.5.7 (August 16, 2021) ###

* Allows more graceful failovers when replication factor > 1

* Fixes a bug that causes partitions to have wrong distribution key after
  `DROP COLUMN`

* Improves master_update_table_statistics and provides distributed deadlock
  detection

### citus v9.4.6 (August 8, 2021) ###

* Allows more graceful failovers when replication factor > 1

* Improves master_update_table_statistics and provides distributed deadlock
  detection

### citus v10.1.1 (August 5, 2021) ###

* Improves citus_update_table_statistics and provides distributed deadlock
  detection

* Fixes showing target shard size in the rebalance progress monitor

### citus v10.1.0 (July 14, 2021) ###

* Drops support for PostgreSQL 11

* Adds `shard_count` parameter to `create_distributed_table` function

* Adds support for `ALTER DATABASE OWNER`

* Adds support for temporary columnar tables

* Adds support for using sequences as column default values when syncing
  metadata

* `alter_columnar_table_set` enforces columnar table option constraints

* Continues to remove shards after failure in `DropMarkedShards`

* Deprecates the `citus.replication_model` GUC

* Enables `citus.defer_drop_after_shard_move` by default

* Ensures free disk space before moving a shard

* Fetches shard size on the fly for the rebalance monitor

* Ignores old placements when disabling or removing a node

* Implements `improvement_threshold` at shard rebalancer moves

* Improves orphaned shard cleanup logic

* Improves performance of `citus_shards`

* Introduces `citus.local_hostname` GUC for connections to the current node

* Makes sure connection is closed after each shard move

* Makes sure that target node in shard moves is eligible for shard move

* Optimizes partitioned disk size calculation for shard rebalancer

* Prevents connection errors by properly terminating connections

* Prevents inheriting a distributed table

* Prevents users from dropping & truncating known shards

* Pushes down `VALUES` clause as long as not in outer part of a `JOIN`

* Reduces memory usage for multi-row inserts

* Reduces memory usage while rebalancing shards

* Removes length limits around partition names

* Removes dependencies on the existence of public schema

* Executor avoids opening extra connections

* Excludes orphaned shards while finding shard placements

* Preserves access method of materialized views when undistributing
  or altering distributed tables

* Fixes a bug that allowed moving of shards belonging to a reference table

* Fixes a bug that can cause a crash when DEBUG4 logging is enabled

* Fixes a bug that causes pruning incorrect shard of a range distributed table

* Fixes a bug that causes worker_create_or_alter_role to crash with NULL input

* Fixes a bug where foreign key to reference table was disallowed

* Fixes a bug with local cached plans on tables with dropped columns

* Fixes data race in `get_rebalance_progress`

* Fixes `FROM ONLY` queries on partitioned tables

* Fixes an issue that could cause citus_finish_pg_upgrade to fail

* Fixes error message for local table joins

* Fixes issues caused by omitting public schema in queries

* Fixes nested `SELECT` query with `UNION` bug

* Fixes null relationName bug at parallel execution

* Fixes possible segfaults when using Citus in the middle of an upgrade

* Fixes problems with concurrent calls of `DropMarkedShards`

* Fixes shared dependencies that are not resident in a database

* Fixes stale hostnames bug in prepared statements after `master_update_node`

* Fixes the relation size bug during rebalancing

* Fixes two race conditions in the get_rebalance_progress

* Fixes using 2PC when it might be necessary

### citus v10.0.4 (July 14, 2021) ###

* Introduces `citus.local_hostname` GUC for connections to the current node

* Removes dependencies on the existence of public schema

* Removes limits around long partition names

* Fixes a bug that can cause a crash when DEBUG4 logging is enabled

* Fixes a bug that causes pruning incorrect shard of a range distributed table

* Fixes an issue that could cause citus_finish_pg_upgrade to fail

* Fixes FROM ONLY queries on partitioned tables

* Fixes issues caused by public schema being omitted in queries

* Fixes problems with concurrent calls of DropMarkedShards

* Fixes relname null bug when using parallel execution

* Fixes two race conditions in the get_rebalance_progress

### citus v9.5.6 (July 8, 2021) ###

* Fixes minor bug in `citus_prepare_pg_upgrade` that caused it to lose its
  idempotency

### citus v9.5.5 (July 7, 2021) ###

* Adds a configure flag to enforce security

* Fixes a bug that causes pruning incorrect shard of a range distributed table

* Fixes an issue that could cause citus_finish_pg_upgrade to fail

### citus v9.4.5 (July 7, 2021) ###

* Adds a configure flag to enforce security

* Avoids re-using connections for intermediate results

* Fixes a bug that causes pruning incorrect shard of a range distributed table

* Fixes a bug that might cause self-deadlocks when COPY used in TX block

* Fixes an issue that could cause citus_finish_pg_upgrade to fail

### citus v8.3.3 (March 23, 2021) ###

* Fixes a bug that leads to various issues when a connection is lost

* Fixes a bug where one could create a foreign key between non-colocated tables

* Fixes a deadlock during transaction recovery

* Fixes a memory leak in adaptive executor when query returns many columns

### citus v10.0.3 (March 16, 2021) ###

* Prevents infinite recursion for queries that involve `UNION ALL`
  below `JOIN`

* Fixes a crash in queries with a modifying `CTE` and a `SELECT`
  without `FROM`

* Fixes upgrade and downgrade paths for `citus_update_table_statistics`

* Fixes a bug that causes `SELECT` queries to use 2PC unnecessarily

* Fixes a bug that might cause self-deadlocks with
  `CREATE INDEX` / `REINDEX CONCURRENTLY` commands

* Adds `citus.max_cached_connection_lifetime` GUC to set maximum connection
  lifetime

* Adds `citus.remote_copy_flush_threshold` GUC that controls
  per-shard memory usages by `COPY`

* Adds `citus_get_active_worker_nodes` UDF to deprecate
  `master_get_active_worker_nodes`

* Skips 2PC for readonly connections in a transaction

* Makes sure that local execution starts coordinated transaction

* Removes open temporary file warning when cancelling a query with
  an open tuple store

* Relaxes the locks when adding an existing node

### citus v10.0.2 (March 3, 2021) ###

* Adds a configure flag to enforce security

* Fixes a bug due to cross join without target list

* Fixes a bug with `UNION ALL` on PG 13

* Fixes a compatibility issue with pg_audit in utility calls

* Fixes insert query with CTEs/sublinks/subqueries etc

* Grants `SELECT` permission on `citus_tables` view to `public`

* Grants `SELECT` permission on columnar metadata tables to `public`

* Improves `citus_update_table_statistics` and provides distributed deadlock
  detection

* Preserves colocation with procedures in `alter_distributed_table`

* Prevents using `alter_columnar_table_set` and `alter_columnar_table_reset`
  on a columnar table not owned by the user

* Removes limits around long table names

### citus v9.5.4 (February 19, 2021) ###

* Fixes a compatibility issue with pg_audit in utility calls

### citus v10.0.1 (February 19, 2021) ###

* Fixes an issue in creation of `pg_catalog.time_partitions` view

### citus v9.5.3 (February 16, 2021) ###

* Avoids re-using connections for intermediate results

* Fixes a bug that might cause self-deadlocks when `COPY` used in xact block

* Fixes a crash that occurs when distributing table after dropping foreign key

### citus v10.0.0 (February 16, 2021) ###

* Adds support for per-table option for columnar storage

* Adds `rebalance_table_shards` to rebalance the shards across the nodes

* Adds `citus_drain_node` to move all shards away from any node

* Enables single-node Citus for production workloads

* Adds support for local table and distributed table/subquery joins

* Enables foreign keys between reference tables and local tables
  (`citus.enable_local_reference_table_foreign_keys`)

* Adds support for co-located/recurring correlated subqueries

* Adds support for co-located/recurring sublinks in the target list

* Adds `alter_distributed_table` and `alter_table_set_access_method` UDFs

* Adds `alter_old_partitions_set_access_method` UDF to compress old partitions

* Adds cascade option to `undistribute_table` UDF for foreign key connected
  relations

* Allows distributed table creation immediately after CREATE EXTENSION citus

* Automatically adds coordinator to the metadata before the first distributed
  table created

* Introduces adaptive connection management for local nodes

* Adds support for local execution in `INSERT..SELECT` commands that perform
  re-partitioning

* Adds `public.citus_tables` view

* Adds `pg_catalog.citus_shards`, `pg_catalog.citus_shards_on_worker` and
  `pg_catalog.citus_shard_indexes_on_worker` views

* Adds `pg_catalog.time_partitions` view for simple (time) partitions and their
  access methods

* Adds `remove_local_tables_from_metadata` UDF for local tables automatically
  added to metadata when defining foreign keys with reference tables

* Adds support for `CREATE INDEX` commands without index name on citus tables

* Adds support for `CREATE TABLE ... USING table_access_method` statements

* Propagates `ALTER TABLE .. SET LOGGED/UNLOGGED` statements

* Propagates `ALTER INDEX .. SET STATISTICS` statements

* Propagates `ALTER SCHEMA RENAME` statements

* Propagates `CREATE STATISTICS` statements across workers.

* Propagates `DROP STATISTICS` statements across the workers

* Propagates all types of `ALTER STATISTICS` statements.

* Avoids establishing new connections until the previous ones are finalized

* Avoids re-using connections for intermediate results

* Improves performance in some subquery pushdown cases

* Removes unused `citus.binary_master_copy_format` GUC

* Removes unused `citus.expire_cached_shards` GUC

* Removes unused `citus.large_table_shard_count` GUC

* Removes unused `citus.max_assign_task_batch_size` GUC

* Removes unused `citus.max_running_tasks_per_node` GUC

* Removes unused `citus.max_task_string_size` GUC

* Removes unused `citus.max_tracked_tasks_per_node` GUC

* Removes unused `citus.sslmode` GUC

* Removes unused `citus.task_tracker_delay` GUC

* Removes the word 'master' from Citus UDFs

* Removes unused UDF `mark_tables_colocated`

* Removes `upgrade_to_reference_table` UDF

* Renames 'master' to 'distributed' for columns of `citus_dist_stat_activity`

* Renames 'master' to 'distributed' for columns of `citus_worker_stat_activity`

* Chooses the default co-location group deterministically

* Deletes distributed transaction entries when removing a node

* Drops support for `create_citus_local_table` in favor of
  `citus_add_local_table_to_metadata`

* Fixes `EXPLAIN ANALYZE` error when query returns no columns

* Fixes a bug preventing `INSERT SELECT .. ON CONFLICT` with a constraint name
  on local shards

* Fixes a bug related to correctness of multiple joins

* Fixes a bug that might cause self-deadlocks when `COPY` used in xact block

* Fixes a bug with partitioned tables that block new partition creation due to
  wrong constraint names on workers

* Fixes a crash that occurs when distributing table after dropping foreign key

* Fixes a crash when adding/dropping foreign keys from reference to local
  tables added to metadata

* Fixes an unexpected error when executing `CREATE TABLE IF NOT EXISTS
  PARTITION OF` commands

* Fixes deadlock issue for `CREATE INDEX` in single node

* Fixes distributed deadlock detection being blocked by metadata sync

* Fixes handling indexes when adding local table to metadata

* Fixes `undistribute_table` when table has column with `GENERATED ALWAYS AS
  STORED` expressions

* Improves concurrent index creation failure message

* Prevents empty placement creation in the coordinator when executing
  `master_create_empty_shard()`

### citus v9.5.2 (January 26, 2021) ###

* Fixes distributed deadlock detection being blocked by metadata sync

* Prevents segfaults when SAVEPOINT handling cannot recover from connection
  failures

* Fixes possible issues that might occur with single shard distributed tables

### citus v9.4.4 (December 28, 2020) ###

* Fixes a bug that could cause router queries with local tables to be pushed
  down

* Fixes a segfault in connection management due to invalid connection hash
  entries

* Fixes possible issues that might occur with single shard distributed tables

### citus v9.5.1 (December 1, 2020) ###

* Enables PostgreSQL's parallel queries on EXPLAIN ANALYZE

* Fixes a bug that could cause excessive memory consumption when a partition is
  created

* Fixes a bug that triggers subplan executions unnecessarily with cursors

* Fixes a segfault in connection management due to invalid connection hash
  entries

### citus v9.4.3 (November 24, 2020) ###

* Enables PostgreSQL's parallel queries on EXPLAIN ANALYZE

* Fixes a bug that triggers subplan executions unnecessarily with cursors

### citus v9.5.0 (November 10, 2020) ###

* Adds support for PostgreSQL 13

* Removes the task-tracker executor

* Introduces citus local tables

* Introduces `undistribute_table` UDF to convert tables back to postgres tables

* Adds support for `EXPLAIN (ANALYZE) EXECUTE` and `EXPLAIN EXECUTE`

* Adds support for `EXPLAIN (ANALYZE, WAL)` for PG13

* Sorts the output of `EXPLAIN (ANALYZE)` by execution duration.

* Adds support for CREATE TABLE ... USING table_access_method

* Adds support for `WITH TIES` option in SELECT and INSERT SELECT queries

* Avoids taking multi-shard locks on workers

* Enforces `citus.max_shared_pool_size` config in COPY queries

* Enables custom aggregates with multiple parameters to be executed on workers

* Enforces `citus.max_intermediate_result_size` in local execution

* Improves cost estimation of INSERT SELECT plans

* Introduces delegation of procedures that read from reference tables

* Prevents pull-push execution for simple pushdownable subqueries

* Improves error message when creating a foreign key to a local table

* Makes `citus_prepare_pg_upgrade` idempotent by dropping transition tables

* Disallows `ON TRUE` outer joins with reference & distributed tables when
  reference table is outer relation to avoid incorrect results

* Disallows field indirection in INSERT/UPDATE queries to avoid incorrect
  results

* Disallows volatile functions in UPDATE subqueries to avoid incorrect results

* Fixes CREATE INDEX CONCURRENTLY crash with local execution

* Fixes `citus_finish_pg_upgrade` to drop all backup tables

* Fixes a bug that cause failures when `RECURSIVE VIEW` joined reference table

* Fixes DROP SEQUENCE failures when metadata syncing is enabled

* Fixes a bug that caused CREATE TABLE with CHECK constraint to fail

* Fixes a bug that could cause VACUUM to deadlock

* Fixes master_update_node failure when no background worker slots are available

* Fixes a bug that caused replica identity to not be propagated on shard repair

* Fixes a bug that could cause crashes after connection timeouts

* Fixes a bug that could cause crashes with certain compile flags

* Fixes a bug that could cause deadlocks on CREATE INDEX

* Fixes a bug with genetic query optimization in outer joins

* Fixes a crash when aggregating empty tables

* Fixes a crash with inserting domain constrained composite types

* Fixes a crash with multi-row & router INSERT's in local execution

* Fixes a possibility of doing temporary file cleanup more than once

* Fixes incorrect setting of join related fields

* Fixes memory issues around deparsing index commands

* Fixes reference table access tracking for sequential execution

* Fixes removal of a single node with only reference tables

* Fixes sending commands to coordinator when it is added as a worker

* Fixes write queries with const expressions and COLLATE in various places

* Fixes wrong cancellation message about distributed deadlock

### citus v9.4.2 (October 21, 2020) ###

* Fixes a bug that could lead to multiple maintenance daemons

* Fixes an issue preventing views in reference table modifications

### citus v9.4.1 (September 30, 2020) ###

* Fixes EXPLAIN ANALYZE output truncation

* Fixes a deadlock during transaction recovery

### citus v9.4.0 (July 28, 2020) ###

* Improves COPY by honoring max_adaptive_executor_pool_size config

* Adds support for insert into local table select from distributed table

* Adds support to partially push down tdigest aggregates

* Adds support for receiving binary encoded results from workers using
  citus.enable_binary_protocol

* Enables joins between local tables and CTEs

* Adds showing query text in EXPLAIN output when explain verbose is true

* Adds support for showing CTE statistics in EXPLAIN ANALYZE

* Adds support for showing amount of data received in EXPLAIN ANALYZE

* Introduces downgrade paths in migration scripts

* Avoids returning incorrect results when changing roles in a transaction

* Fixes `ALTER TABLE IF EXISTS SET SCHEMA` with non-existing table bug

* Fixes `CREATE INDEX CONCURRENTLY` with no index name on a postgres table bug

* Fixes a bug that could cause crashes with certain compile flags

* Fixes a bug with lists of configuration values in ALTER ROLE SET statements

* Fixes a bug that occurs when coordinator is added as a worker node

* Fixes a crash because of overflow in partition id with certain compile flags

* Fixes a crash that may happen if no worker nodes are added

* Fixes a crash that occurs when inserting implicitly coerced constants

* Fixes a crash when aggregating empty tables

* Fixes a memory leak in subtransaction memory handling

* Fixes crash when using rollback to savepoint after cancellation of DML

* Fixes deparsing for queries with anonymous column references

* Fixes distribution of composite types failing to include typemods

* Fixes explain analyze on adaptive executor repartitions

* Fixes possible error throwing in abort handle

* Fixes segfault when evaluating func calls with default params on coordinator

* Fixes several EXPLAIN ANALYZE issues

* Fixes write queries with const expressions and COLLATE in various places

* Fixes wrong cancellation message about distributed deadlocks

* Reports correct INSERT/SELECT method in EXPLAIN

* Disallows triggers on citus tables

### citus v9.3.5 (July 24, 2020) ###

* Fixes `ALTER TABLE IF EXISTS SET SCHEMA` with non-existing table bug

* Fixes `CREATE INDEX CONCURRENTLY` with no index name on a postgres table bug

* Fixes a crash because of overflow in partition id with certain compile flags

### citus v9.3.4 (July 21, 2020) ###

* Fixes a bug that could cause crashes with certain compile flags

* Fixes a bug with lists of configuration values in ALTER ROLE SET statements

* Fixes deparsing for queries with anonymous column references

### citus v9.3.3 (July 10, 2020) ###

* Fixes a memory leak in subtransaction memory handling

### citus v9.3.2 (Jun 22, 2020) ###

* Fixes a version bump issue in 9.3.1

### citus v9.2.6 (Jun 22, 2020) ###

* Fixes a version bump issue in 9.2.5

### citus v9.3.1 (Jun 17, 2020) ###

* Adds support to partially push down tdigest aggregates

* Fixes a crash that occurs when inserting implicitly coerced constants

### citus v9.2.5 (Jun 17, 2020) ###

* Adds support to partially push down tdigest aggregates

* Fixes an issue with distributing tables having generated cols not at the end

### citus v9.3.0 (May 6, 2020) ###

* Adds `max_shared_pool_size` to control number of connections across sessions

* Adds support for window functions on coordinator

* Improves shard pruning logic to understand OR-conditions

* Prevents using an extra connection for intermediate result multi-casts

* Adds propagation of `ALTER ROLE .. SET` statements

* Adds `update_distributed_table_colocation` UDF to update colocation of tables

* Introduces a UDF to truncate local data after distributing a table

* Adds support for creating temp schemas in parallel

* Adds support for evaluation of `nextval` in the target list on coordinator

* Adds support for local execution of `COPY/TRUNCATE/DROP/DDL` commands

* Adds support for local execution of shard creation

* Uses local execution in a transaction block

* Adds support for querying distributed table sizes concurrently

* Allows `master_copy_shard_placement` to replicate placements to new nodes

* Allows table type to be used in target list

* Avoids having multiple maintenance daemons active for a single database

* Defers reference table replication to shard creation time

* Enables joins between local tables and reference tables in transaction blocks

* Ignores pruned target list entries in coordinator plan

* Improves `SIGTERM` handling of maintenance daemon

* Increases the default of `citus.node_connection_timeout` to 30 seconds

* Fixes a bug that occurs when creating remote tasks in local execution

* Fixes a bug that causes some DML queries containing aggregates to fail

* Fixes a bug that could cause failures in queries with subqueries or CTEs

* Fixes a bug that may cause some connection failures to throw errors

* Fixes a bug which caused queries with SRFs and function evalution to fail

* Fixes a bug with generated columns when executing `COPY dist_table TO file`

* Fixes a crash when using non-constant limit clauses

* Fixes a failure when composite types used in prepared statements

* Fixes a possible segfault when dropping dist. table in a transaction block

* Fixes a possible segfault when non-pushdownable aggs are solely used in HAVING

* Fixes a segfault when executing queries using `GROUPING`

* Fixes an error when using `LEFT JOIN with GROUP BY` on primary key

* Fixes an issue with distributing tables having generated cols not at the end

* Fixes automatic SSL permission issue when using "initdb --allow-group-access"

* Fixes errors which could occur when subqueries are parameters to aggregates

* Fixes possible issues by invalidating the plan cache in `master_update_node`

* Fixes timing issues which could be caused by changing system clock

### citus v9.2.4 (March 30, 2020) ###

* Fixes a release problem in 9.2.3

### citus v9.2.3 (March 25, 2020) ###

* Do not use C functions that have been banned by Microsoft

* Fixes a bug that causes wrong results with complex outer joins

* Fixes issues found using static analysis

* Fixes left join shard pruning in pushdown planner

* Fixes possibility for segmentation fault in internal aggregate functions

* Fixes possible segfault when non pushdownable aggregates are used in `HAVING`

* Improves correctness of planning subqueries in `HAVING`

* Prevents using old connections for security if `citus.node_conninfo` changed

* Uses Microsoft approved cipher string for default TLS setup

### citus v9.0.2 (March 6, 2020) ###

* Fixes build errors on EL/OL 6 based distros

* Fixes a bug that caused maintenance daemon to fail on standby nodes

* Disallows distributed function creation when replication_model is `statement`

### citus v9.2.2 (March 5, 2020) ###

* Fixes a bug that caused some prepared stmts with function calls to fail

* Fixes a bug that caused some prepared stmts with composite types to fail

* Fixes a bug that caused missing subplan results in workers

* Improves performance of re-partition joins

### citus v9.2.1 (February 14, 2020) ###

* Fixes a bug that could cause crashes if distribution key is NULL

### citus v9.2.0 (February 10, 2020) ###

* Adds support for `INSERT...SELECT` queries with re-partitioning

* Adds `citus.coordinator_aggregation_strategy` to support more aggregates

* Adds caching of local plans on shards for Citus MX

* Adds compatibility support for dist. object infrastructure from old versions

* Adds defering shard-pruning for fast-path router queries to execution

* Adds propagation of `GRANT ... ON SCHEMA` queries

* Adds support for CTE pushdown via CTE inlining in distributed planning

* Adds support for `ALTER TABLE ... SET SCHEMA` propagation.

* Adds support for `DROP ROUTINE` & `ALTER ROUTINE` commands

* Adds support for any inner join on a reference table

* Changes `citus.log_remote_commands` level to `NOTICE`

* Disallows marking ref. table shards unhealthy in the presence of savepoints

* Disallows placing new shards with shards in TO_DELETE state

* Enables local execution of queries that do not need any data access

* Fixes Makefile trying to cleanup PG directory during install

* Fixes a bug causing errors when planning a query with multiple subqueries

* Fixes a possible deadlock that could happen during shard moves

* Fixes a problem when adding a new node due to tables referenced in func body

* Fixes an issue that could cause joins with reference tables to be slow

* Fixes cached metadata for shard is inconsistent issue

* Fixes inserting multiple composite types as partition key in VALUES

* Fixes unnecessary repartition on joins with more than 4 tables

* Prevents wrong results for replicated partitioned tables after failure

* Restricts LIMIT approximation for non-commutative aggregates

### citus v9.1.2 (December 30, 2019) ###

* Fixes a bug that prevents installation from source

### citus v9.1.1 (December 18, 2019) ###

* Fixes a bug causing SQL-executing UDFs to crash when passing in DDL

* Fixes a bug that caused column_to_column_name to crash for invalid input

* Fixes a bug that caused inserts into local tables w/ dist. subqueries to crash

* Fixes a bug that caused some noop DML statements to fail

* Fixes a bug that prevents dropping reference table columns

* Fixes a crash in IN (.., NULL) queries

* Fixes a crash when calling a distributed function from PL/pgSQL

* Fixes an issue that caused CTEs to sometimes leak connections

* Fixes strange errors in DML with unreachable sublinks

* Prevents statements in SQL functions to run outside of a transaction

### citus v9.1.0 (November 21, 2019) ###

* Adds extensions to distributed object propagation infrastructure

* Adds support for ALTER ROLE propagation

* Adds support for aggregates in create_distributed_function

* Adds support for expressions in reference joins

* Adds support for returning RECORD in multi-shard queries

* Adds support for simple IN subqueries on unique cols in repartition joins

* Adds support for subqueries in HAVING clauses

* Automatically distributes unary aggs w/ combinefunc and non-internal stype

* Disallows distributed func creation when replication_model is 'statement'

* Drops support for deprecated real-time and router executors

* Fixes a bug in local execution that could cause missing rows in RETURNING

* Fixes a bug that caused maintenance daemon to fail on standby nodes

* Fixes a bug that caused other CREATE EXTENSION commands to take longer

* Fixes a bug that prevented REFRESH MATERIALIZED VIEW

* Fixes a bug when view is used in modify statements

* Fixes a memory leak in adaptive executor when query returns many columns

* Fixes underflow init of default values in worker extended op node creation

* Fixes potential segfault in standard_planner inlining functions

* Fixes an issue that caused failures in RHEL 6 builds

* Fixes queries with repartition joins and group by unique column

* Improves CTE/Subquery performance by pruning intermediate rslt broadcasting

* Removes `citus.worker_list_file` GUC

* Revokes usage from the citus schema from public

### citus v9.0.1 (October 25, 2019) ###

* Fixes a memory leak in the executor

* Revokes usage from the citus schema from public

### citus v9.0.0 (October 7, 2019) ###

* Adds support for PostgreSQL 12

* Adds UDFs to help with PostgreSQL upgrades

* Distributes types to worker nodes

* Introduces `create_distributed_function` UDF

* Introduces local query execution for Citus MX

* Implements infrastructure for routing `CALL` to MX workers

* Implements infrastructure for routing `SELECT function()` to MX workers

* Adds support for foreign key constraints between reference tables

* Adds a feature flag to turn off `CREATE TYPE` propagation

* Adds option `citus.single_shard_commit_protocol`

* Adds support for `EXPLAIN SUMMARY`

* Adds support for `GENERATE ALWAYS AS STORED`

* Adds support for `serial` and `smallserial` in MX mode

* Adds support for anon composite types on the target list in router queries

* Avoids race condition between `create_reference_table` & `master_add_node`

* Fixes a bug in schemas of distributed sequence definitions

* Fixes a bug that caused `run_command_on_colocated_placements` to fail

* Fixes a bug that leads to various issues when a connection is lost

* Fixes a schema leak on `CREATE INDEX` statement

* Fixes assert failure in bare `SELECT FROM reference table FOR UPDATE` in MX

* Makes `master_update_node` MX compatible

* Prevents `pg_dist_colocation` from multiple records for reference tables

* Prevents segfault in `worker_partition_protocol` edgecase

* Propagates `ALTER FUNCTION` statements for distributed functions

* Propagates `CREATE OR REPLACE FUNCTION` for distributed functions

* Propagates `REINDEX` on tables & indexes

* Provides a GUC to turn of the new dependency propagation functionality

* Uses 2PC in adaptive executor when dealing with replication factors above 1

### citus v8.3.2 (August 09, 2019) ###

* Fixes performance issues by skipping unnecessary relation access recordings

### citus v8.3.1 (July 29, 2019) ###

* Improves Adaptive Executor performance

### citus v8.3.0 (July 10, 2019) ###

* Adds a new distributed executor: Adaptive Executor

* citus.enable_statistics_collection defaults to off (opt-in)

* Adds support for CTEs in router planner for modification queries

* Adds support for propagating SET LOCAL at xact start

* Adds option to force master_update_node during failover

* Deprecates master_modify_multiple_shards

* Improves round robin logic on router queries

* Creates all distributed schemas as superuser on a separate connection

* Makes COPY adapt to connection use behaviour of previous commands

* Replaces SESSION_LIFESPAN with configurable number of connections at xact end

* Propagates ALTER FOREIGN TABLE commands to workers

* Don't schedule tasks on inactive nodes

* Makes DROP/VALIDATE CONSTRAINT tolerant of ambiguous shard extension

* Fixes an issue with subquery map merge jobs as non-root

* Fixes null pointers caused by partial initialization of ConnParamsHashEntry

* Fixes errors caused by joins with shadowed aliases

* Fixes a regression in outer joining subqueries introduced in 8.2.0

* Fixes a crash that can occur under high memory load

* Fixes a bug that selects wrong worker when using round-robin assignment

* Fixes savepoint rollback after multi-shard modify/copy failure

* Fixes bad foreign constraint name search

* Fixes a bug that prevents stack size to be adjusted

### citus v8.2.2 (June 11, 2019) ###

* Fixes a bug in outer joins wrapped in subqueries

### citus v8.2.1 (April 03, 2019) ###

* Fixes a bug that prevents stack size to be adjusted

### citus v8.1.2 (April 03, 2019) ###

* Don't do redundant ALTER TABLE consistency checks at coordinator

* Fixes a bug that prevents stack size to be adjusted

* Fix an issue with some DECLARE .. CURSOR WITH HOLD commands

### citus v8.2.0 (March 28, 2019) ###

* Removes support and code for PostgreSQL 9.6

* Enable more outer joins with reference tables

* Execute CREATE INDEX CONCURRENTLY in parallel

* Treat functions as transaction blocks

* Add support for column aliases on join clauses

* Skip standard_planner() for trivial queries

* Added support for function calls in joins

* Round-robin task assignment policy relies on local transaction id

* Relax subquery union pushdown restrictions for reference tables

* Speed-up run_command_on_shards()

* Address some memory issues in connection config

* Restrict visibility of get_*_active_transactions functions to pg_monitor

* Don't do redundant ALTER TABLE consistency checks at coordinator

* Queries with only intermediate results do not rely on task assignment policy

* Finish connection establishment in parallel for multiple connections

* Fixes a bug related to pruning shards using a coerced value

* Fix an issue with some DECLARE .. CURSOR WITH HOLD commands

* Fixes a bug that could lead to infinite recursion during recursive planning

* Fixes a bug that could prevent planning full outer joins with using clause

* Fixes a bug that could lead to memory leak on `citus_relation_size`

* Fixes a problem that could cause segmentation fault with recursive planning

* Switch CI solution to CircleCI

### citus v8.0.3 (January 9, 2019) ###

* Fixes maintenance daemon panic due to unreleased spinlock

* Fixes an issue with having clause when used with complex joins

### citus v8.1.1 (January 7, 2019) ###

* Fixes maintenance daemon panic due to unreleased spinlock

* Fixes an issue with having clause when used with complex joins

### citus v8.1.0 (December 17, 2018) ###

* Turns on ssl by default for new installations of citus

* Restricts SSL Ciphers to TLS1.2 and above

* Adds support for INSERT INTO SELECT..ON CONFLICT/RETURNING via coordinator

* Adds support for round-robin task assignment for queries to reference tables

* Adds support for SQL tasks using worker_execute_sql_task UDF with task-tracker

* Adds support for VALIDATE CONSTRAINT queries

* Adds support for disabling hash aggregate with HLL

* Adds user ID suffix to intermediate files generated by task-tracker

* Only allow transmit from pgsql_job_cache directory

* Disallows GROUPING SET clauses in subqueries

* Removes restriction on user-defined group ID in node addition functions

* Relaxes multi-shard modify locks when enable_deadlock_prevention is disabled

* Improves security in task-tracker protocol

* Improves permission checks in internal DROP TABLE functions

* Improves permission checks in cluster management functions

* Cleans up UDFs and fixes permission checks

* Fixes crashes caused by stack size increase under high memory load

* Fixes a bug that could cause maintenance daemon panic

### citus v8.0.2 (December 13, 2018) ###

* Fixes a bug that could cause maintenance daemon panic

* Fixes crashes caused by stack size increase under high memory load

### citus v7.5.4 (December 11, 2018) ###

* Fixes a bug that could cause maintenance daemon panic

### citus v8.0.1 (November 27, 2018) ###

* Execute SQL tasks using worker_execute_sql_task UDF when using task-tracker

### citus v7.5.3 (November 27, 2018) ###

* Execute SQL tasks using worker_execute_sql_task UDF when using task-tracker

### citus v7.5.2 (November 14, 2018) ###

* Fixes inconsistent metadata error when shard metadata caching get interrupted

* Fixes a bug that could cause memory leak

* Fixes a bug that prevents recovering wrong transactions in MX

* Fixes a bug to prevent wrong memory accesses on Citus MX under very high load

* Fixes crashes caused by stack size increase under high memory load

### citus v8.0.0 (October 31, 2018) ###

* Adds support for PostgreSQL 11

* Adds support for applying DML operations on reference tables from MX nodes

* Adds distributed locking to truncated MX tables

* Adds support for running TRUNCATE command from MX worker nodes

* Adds views to provide insight about the distributed transactions

* Adds support for TABLESAMPLE in router queries

* Adds support for INCLUDE option in index creation

* Adds option to allow simple DML commands from hot standby

* Adds support for partitioned tables with replication factor > 1

* Prevents a deadlock on concurrent DROP TABLE and SELECT on Citus MX

* Fixes a bug that prevents recovering wrong transactions in MX

* Fixes a bug to prevent wrong memory accesses on Citus MX under very high load

* Fixes a bug in MX mode, calling DROP SCHEMA with existing partitioned table

* Fixes a bug that could cause modifying CTEs to select wrong execution mode

* Fixes a bug preventing rollback in CREATE PROCEDURE

* Fixes a bug on not being able to drop index on a partitioned table

* Fixes a bug on TRUNCATE when there is a foreign key to a reference table

* Fixes a performance issue in prepared INSERT..SELECT

* Fixes a bug which causes errors on DROP DATABASE IF EXISTS

* Fixes a bug to remove intermediate result directory in pull-push execution

* Improves query pushdown planning performance

* Evaluate functions anywhere in query

### citus v7.5.1 (August 28, 2018) ###

* Improves query pushdown planning performance

* Fixes a bug that could cause modifying CTEs to select wrong execution mode

### citus v7.4.2 (July 27, 2018) ###

* Fixes a segfault in real-time executor during online shard move

### citus v7.5.0 (July 25, 2018) ###

* Adds foreign key support from hash distributed to reference tables

* Adds SELECT ... FOR UPDATE support for router plannable queries

* Adds support for non-partition columns in count distinct

* Fixes a segfault in real-time executor during online shard move

* Fixes ALTER TABLE ADD COLUMN constraint check

* Fixes a bug where INSERT ... SELECT was allowed to update distribution column

* Allows DDL commands to be sequentialized via `citus.multi_shard_modify_mode`

* Adds support for topn_union_agg and topn_add_agg across shards

* Adds support for hll_union_agg and hll_add_agg across shards

* Fixes a bug that might cause shards to have a wrong owner

* GUC select_opens_transaction_block defers opening transaction block on workers

* Utils to implement DDLs for policies in future, warn about being unsupported

* Intermediate results use separate connections to avoid interfering with tasks

* Adds a node_conninfo GUC to set outgoing connection settings

### citus v6.2.6 (July 06, 2018) ###

* Adds support for respecting enable_hashagg in the master planner

### citus v7.4.1 (June 20, 2018) ###

* Fixes a bug that could cause transactions to incorrectly proceed after failure

* Fixes a bug on INSERT ... SELECT queries in prepared statements

### citus v7.4.0 (May 15, 2018) ###

* Adds support for non-pushdownable subqueries and CTEs in UPDATE/DELETE queries

* Adds support for pushdownable subqueries and joins in UPDATE/DELETE queries

* Adds faster shard pruning for subqueries

* Adds partitioning support to MX table

* Adds support for (VACUUM | ANALYZE) VERBOSE

* Adds support for multiple ANDs in `HAVING` for pushdown planner

* Adds support for quotation needy schema names

* Improves operator check time in physical planner for custom data types

* Removes broadcast join logic

* Deprecates `large_table_shard_count` and `master_expire_table_cache()`

* Modifies master_update_node to lock write on shards hosted by node over update

* `DROP TABLE` now drops shards as the currrent user instead of the superuser

* Adds specialised error codes for connection failures

* Improves error messages on connection failure

* Fixes issue which prevented multiple `citus_table_size` calls per query

* Tests are updated to use `create_distributed_table`

### citus v7.2.2 (May 4, 2018) ###

* Fixes a bug that could cause SELECTs to crash during a rebalance

### citus v7.3.0 (March 15, 2018) ###

* Adds support for non-colocated joins between subqueries

* Adds support for window functions that can be pushed down to worker

* Adds support for modifying CTEs

* Adds recursive plan for subqueries in WHERE clause with recurring FROM clause

* Adds support for bool_ and bit_ aggregates

* Adds support for Postgres `jsonb` and `json` aggregation functions

* Adds support for respecting enable_hashagg in the master plan

* Adds support for renaming a distributed table

* Adds support for ALTER INDEX (SET|RESET|RENAME TO) commands

* Adds support for setting storage parameters on distributed tables

* Performance improvements to reduce distributed planning time

* Fixes a bug on planner when aggregate is used in ORDER BY

* Fixes a bug on planner when DISTINCT (ON) clause is used with GROUP BY

* Fixes a bug of creating coordinator planner with distinct and aggregate clause

* Fixes a bug that could open a new connection on every table size function call

* Fixes a bug canceling backends that are not involved in distributed deadlocks

* Fixes count distinct bug on column expressions when used with subqueries

* Improves error handling on worker node failures

* Improves error messages for INSERT queries that have subqueries

### citus v7.2.1 (February 6, 2018) ###

* Fixes count distinct bug on column expressions when used with subqueries

* Adds support for respecting enable_hashagg in the master plan

* Fixes a bug canceling backends that are not involved in distributed deadlocks

### citus v7.2.0 (January 16, 2018) ###

* Adds support for CTEs

* Adds support for subqueries that require merge step

* Adds support for set operations (UNION, INTERSECT, ...)

* Adds support for 2PC auto-recovery

* Adds support for querying local tables in CTEs and subqueries

* Adds support for more SQL coverage in subqueries for reference tables

* Adds support for count(distinct) in queries with a subquery

* Adds support for non-equijoins when there is already an equijoin for queries

* Adds support for non-equijoins when there is already an equijoin for subquery

* Adds support for real-time executor to run in transaction blocks

* Adds infrastructure for storing intermediate distributed query results

* Adds a new GUC named `enable_repartition_joins` for auto executor switch

* Adds support for limiting the intermediate result size

* Improves support for queries with unions containing filters

* Improves support for queries with unions containing joins

* Improves support for subqueries in the `WHERE` clause

* Increases `COPY` throughput

* Enables pushing down queries containing only recurring tuples and `GROUP BY`

* Load-balance queries that read from 0 shards

* Improves support for using functions in subqueries

* Fixes a bug that could cause real-time executor to crash during cancellation

* Fixes a bug that could cause real-time executor to get stuck on cancellation

* Fixes a bug that could block modification queries unnecessarily

* Fixes a bug that could cause assigning wrong IDs to transactions

* Fixes a bug that could cause an assert failure with `ANALYZE` statements

* Fixes a bug that could allow pushing down wrong set operations in subqueries

* Fixes a bug that could cause a deadlock in create_distributed_table

* Fixes a bug that could confuse user about `ANALYZE` usage

* Fixes a bug that could lead to false positive distributed deadlock detections

* Relaxes the locking for DDL commands on partitioned tables

* Relaxes the locking on `COPY` with replication

* Logs more remote commands when citus.log_remote_commands is set

### citus v6.2.5 (January 11, 2018) ###

* Fixes a bug that could crash the coordinator while reporting a remote error

### citus v7.1.2 (January 4, 2018) ###

* Fixes a bug that could cause assigning wrong IDs to transactions

* Increases `COPY` throughput

### citus v7.1.1 (December 1, 2017) ###

* Fixes a bug that could prevent pushing down subqueries with reference tables

* Fixes a bug that could create false positive distributed deadlocks

* Fixes a bug that could prevent running concurrent COPY and multi-shard DDL

* Fixes a bug that could mislead users about `ANALYZE` queries

### citus v7.1.0 (November 14, 2017) ###

* Adds support for native queries with multi shard `UPDATE`/`DELETE` queries

* Expands reference table support in subquery pushdown

* Adds window function support for subqueries and `INSERT ... SELECT` queries

* Adds support for `COUNT(DISTINCT) [ON]` queries on non-partition columns

* Adds support for `DISTINCT [ON]` queries on non-partition columns

* Introduces basic usage statistic collector

* Adds support for setting replica identity while creating distributed tables

* Adds support for `ALTER TABLE ... REPLICA IDENTITY` queries

* Adds pushdown support for `LIMIT` and `HAVING` grouped by partition key

* Adds support for `INSERT ... SELECT` queries via worker nodes on MX clusters

* Adds support for adding primary key using already defined index

* Adds parameter to shard copy functions to support distinct replication models

* Changes `shard_name` UDF to omit public schema name

* Adds `master_move_node` UDF to make changes on nodename/nodeport more easy

* Fixes a bug that could cause casting error with `INSERT ... SELECT` queries

* Fixes a bug that could prevent upgrading servers from Citus 6.1

* Fixes a bug that could prevent attaching partitions to a table in schema

* Fixes a bug that could prevent adding a node to cluster with reference table

* Fixes a bug that could cause a crash with `INSERT ... SELECT` queries

* Fixes a bug that could prevent creating a partitoned table on Cloud

* Implements various performance improvements

* Adds internal infrastructures and tests to improve development process

* Addresses various race conditions and deadlocks

* Improves and standardizes error messages

### citus v7.0.3 (October 16, 2017) ###

* Fixes several bugs that could cause crash

* Fixes a bug that could cause deadlock while creating reference tables

* Fixes a bug that could cause false-positives in deadlock detection

* Fixes a bug that could cause  2PC recovery not to work from MX workers

* Fixes a bug that could cause cache incohorency

* Fixes a bug that could cause maintenance daemon to skip cache invalidations

* Improves performance of transaction recovery by using correct index

### citus v7.0.2 (September 28, 2017) ###

* Updates task-tracker to limit file access

### citus v6.2.4 (September 28, 2017) ###

* Updates task-tracker to limit file access

### citus v6.1.3 (September 28, 2017) ###

* Updates task-tracker to limit file access

### citus v7.0.1 (September 12, 2017) ###

* Fixes a bug that could cause memory leaks in `INSERT ... SELECT` queries

* Fixes a bug that could cause incorrect execution of prepared statements

* Fixes a bug that could cause excessive memory usage during COPY

* Incorporates latest changes from core PostgreSQL code

### citus v7.0.0 (August 28, 2017) ###

* Adds support for PostgreSQL 10

* Drops support for PostgreSQL 9.5

* Adds support for multi-row `INSERT`

* Adds support for router `UPDATE` and `DELETE` queries with subqueries

* Adds infrastructure for distributed deadlock detection

* Deprecates `enable_deadlock_prevention` flag

* Adds support for partitioned tables

* Adds support for creating `UNLOGGED` tables

* Adds support for `SAVEPOINT`

* Adds UDF `citus_create_restore_point` for taking distributed snapshots

* Adds support for evaluating non-pushable `INSERT ... SELECT` queries

* Adds support for subquery pushdown on reference tables

* Adds shard pruning support for `IN` and `ANY`

* Adds support for `UPDATE` and `DELETE` commands that prune down to 0 shard

* Enhances transaction support by relaxing some transaction restrictions

* Fixes a bug causing crash if distributed table has no shards

* Fixes a bug causing crash when removing inactive node

* Fixes a bug causing failure during `COPY` on tables with dropped columns

* Fixes a bug causing failure during `DROP EXTENSION`

* Fixes a bug preventing executing `VACUUM` and `INSERT` concurrently

* Fixes a bug in prepared `INSERT` statements containing an implicit cast

* Fixes several issues related to statement cancellations and connections

* Fixes several 2PC related issues

* Removes an unnecessary dependency causing warning messages in pg_dump

* Adds internal infrastructure for follower clusters

* Adds internal infrastructure for progress tracking

* Implements various performance improvements

* Adds internal infrastructures and tests to improve development process

* Addresses various race conditions and deadlocks

* Improves and standardizes error messages

### citus v6.2.3 (July 13, 2017) ###

* Fixes a crash during execution of local CREATE INDEX CONCURRENTLY

* Fixes a bug preventing usage of quoted column names in COPY

* Fixes a bug in prepared INSERTs with implicit cast in partition column

* Relaxes locks in VACUUM to ensure concurrent execution with INSERT

### citus v6.2.2 (May 31, 2017) ###

* Fixes a common cause of deadlocks when repairing tables with foreign keys

### citus v6.2.1 (May 24, 2017) ###

* Relaxes version-check logic to avoid breaking non-distributed commands

### citus v6.2.0 (May 16, 2017) ###

* Increases SQL subquery coverage by pushing down more kinds of queries

* Adds CustomScan API support to allow read-only transactions

* Adds support for `CREATE/DROP INDEX CONCURRENTLY`

* Adds support for `ALTER TABLE ... ADD CONSTRAINT`

* Adds support for `ALTER TABLE ... RENAME COLUMN`

* Adds support for `DISABLE/ENABLE TRIGGER ALL`

* Adds support for expressions in the partition column in INSERTs

* Adds support for query parameters in combination with function evaluation

* Adds support for creating distributed tables from non-empty local tables

* Adds UDFs to get size of distributed tables

* Adds UDFs to add a new node without replicating reference tables

* Adds checks to prevent running Citus binaries with wrong metadata tables

* Improves shard pruning performance for range queries

* Improves planner performance for joins involving co-located tables

* Improves shard copy performance by creating indexes after copy

* Improves task-tracker performance by batching several status checks

* Enables router planner for queries on range partitioned table

* Changes `TRUNCATE` to drop local data only if `enable_ddl_propagation` is off

* Starts to execute DDL on coordinator before workers

* Fixes a bug causing incorrectly reading invalidated cache

* Fixes a bug related to creation of schemas of in workers with incorrect owner

* Fixes a bug related to concurrent run of shard drop functions

* Fixes a bug related to `EXPLAIN ANALYZE` with DML queries

* Fixes a bug related to SQL functions in FROM clause

* Adds a GUC variable to report cross shard queries

* Fixes a bug related to partition columns without native hash function

* Adds internal infrastructures and tests to improve development process

* Addresses various race conditions and deadlocks

* Improves and standardizes error messages

### citus v6.1.2 (May 31, 2017) ###

* Fixes a common cause of deadlocks when repairing tables with foreign keys

### citus v6.1.1 (May 5, 2017) ###

* Fixes a crash caused by router executor use after connection timeouts

* Fixes a crash caused by relation cache invalidation during COPY

* Fixes bug related to DDL use within PL/pgSQL functions

* Fixes a COPY bug related to types lacking binary output functions

* Fixes a bug related to modifications with parameterized partition values

* Fixes improper value interpolation in worker sequence generation

* Guards shard pruning logic against zero-shard tables

* Fixes possible NULL pointer dereference and buffer underflow (via PVS-Studio)

* Fixes a INSERT ... SELECT bug that could push down non-partition column JOINs

### citus v6.1.0 (February 9, 2017) ###

* Implements _reference tables_, transactionally replicated to all nodes

* Adds `upgrade_to_reference_table` UDF to upgrade pre-6.1 reference tables

* Expands prepared statement support to nearly all statements

* Adds support for creating `VIEW`s which reference distributed tables

* Adds targeted `VACUUM`/`ANALYZE` support

* Adds support for the `FILTER` clause in aggregate expressions

* Adds support for function evaluation within `INSERT INTO ... SELECT`

* Adds support for creating foreign key constraints with `ALTER TABLE`

* Adds logic to choose router planner for all queries it supports

* Enhances `create_distributed_table` with parameter for explicit colocation

* Adds generally useful utility UDFs previously available as "Citus Tools"

* Adds user-facing UDFs for locking shard resources and metadata

* Refactors connection and transaction management; giving consistent experience

* Enhances `COPY` with fully transactional semantics

* Improves support for cancellation for a number of queries and commands

* Adds `column_to_column_name` UDF to help users understand `partkey` values

* Adds `master_disable_node` UDF for temporarily disabling nodes

* Adds proper MX ("masterless") metadata propagation logic

* Adds `start_metadata_sync_to_node` UDF to propagate metadata changes to nodes

* Enhances `SERIAL` compatibility with MX tables

* Adds `node_connection_timeout` parameter to control node connection timeouts

* Adds `enable_deadlock_prevention` setting to permit multi-node transactions

* Adds a `replication_model` setting to specify replication of new tables

* Changes the `shard_replication_factor` setting's default value to one

* Adds code to automatically set `max_prepared_transactions` if not configured

* Accelerates lookup of colocated shard placements

* Fixes a bug affecting `INSERT INTO ... SELECT` queries using constant values

* Fixes a bug by ensuring `COPY` does not mark placements inactive

* Fixes a bug affecting reads from `pg_dist_shard_placement` table

* Fixes a crash triggered by creating a foreign key without a column

* Fixes a crash related to accessing catalog tables after aborted transactions

* Fixes a bug affecting JOIN queries requiring repartitions

* Fixes a bug affecting node insertions to `pg_dist_node` table

* Fixes a crash triggered by queries with modifying common table expressions

* Fixes a bug affecting workloads with concurrent shard appends and deletions

* Addresses various race conditions and deadlocks

* Improves and standardizes error messages

### citus v6.0.1 (November 29, 2016) ###

* Fixes a bug causing failures during pg_upgrade

* Fixes a bug preventing DML queries during colocated table creation

* Fixes a bug that caused NULL parameters to be incorrectly passed as text

### citus v6.0.0 (November 7, 2016) ###

* Adds compatibility with PostgreSQL 9.6, now the recommended version

* Removes the `pg_worker_list.conf` file in favor of a `pg_dist_node` table

* Adds `master_add_node` and `master_add_node` UDFs to manage membership

* Removes the `\stage` command and corresponding csql binary in favor of `COPY`

* Removes `copy_to_distributed_table` in favor of first-class `COPY` support

* Adds support for multiple DDL statements within a transaction

* Adds support for certain foreign key constraints

* Adds support for parallel `INSERT INTO ... SELECT` against colocated tables

* Adds support for the `TRUNCATE` command

* Adds support for `HAVING` clauses in `SELECT` queries

* Adds support for `EXCLUDE` constraints which include the partition column

* Adds support for system columns in queries (`tableoid`, `ctid`, etc.)

* Adds support for relation name extension within `INDEX` definitions

* Adds support for no-op `UPDATE`s of the partition column

* Adds several general-purpose utility UDFs to aid in Citus maintenance

* Adds `master_expire_table_cache` UDF to forcibly expire cached shards

* Parallelizes the processing of DDL commands which affect distributed tables

* Adds support for repartition jobs using composite or custom types

* Enhances object name extension to handle long names and large shard counts

* Parallelizes the `master_modify_multiple_shards` UDF

* Changes distributed table creation to error if the target table is not empty

* Changes the `pg_dist_shard.logicalrelid` column from an `oid` to `regclass`

* Adds a `placementid` column to `pg_dist_shard_placement`, replacing Oid use

* Removes the `pg_dist_shard.shardalias` distribution metadata column

* Adds `pg_dist_partition.repmodel` to track tables using streaming replication

* Adds internal infrastructure to take snapshots of distribution metadata

* Addresses the need to invalidate prepared statements on metadata changes

* Adds a `mark_tables_colocated` UDF for denoting pre-6.0 manual colocation

* Fixes a bug affecting prepared statement execution within PL/pgSQL

* Fixes a bug affecting `COPY` commands using composite types

* Fixes a bug that could cause crashes during `EXPLAIN EXECUTE`

* Separates worker and master job temporary folders

* Eliminates race condition between distributed modification and repair

* Relaxes the requirement that shard repairs also repair colocated shards

* Implements internal functions to track which tables' shards are colocated

* Adds `pg_dist_partition.colocationid` to track colocation group membership

* Extends shard copy and move operations to respect colocation settings

* Adds `pg_dist_local_group` to prepare for future MX-related changes

* Adds `create_distributed_table` to easily create shards and infer colocation

### citus v5.2.2 (November 7, 2016) ###

* Adds support for `IF NOT EXISTS` clause of `CREATE INDEX` command

* Adds support for `RETURN QUERY` and `FOR ... IN` PL/pgSQL features

* Extends the router planner to handle more queries

* Changes `COUNT` of zero-row sets to return `0` rather than an empty result

* Reduces the minimum permitted `task_tracker_delay` to a single millisecond

* Fixes a bug that caused crashes during joins with a `WHERE false` clause

* Fixes a bug triggered by unique violation errors raised in long transactions

* Fixes a bug resulting in multiple registration of transaction callbacks

* Fixes a bug which could result in stale reads of distribution metadata

* Fixes a bug preventing distributed modifications in some PL/pgSQL functions

* Fixes some code paths that could hypothetically read uninitialized memory

* Lowers log level of _waiting for activity_ messages

### citus v5.2.1 (September 6, 2016) ###

* Fixes subquery pushdown to properly extract outer join qualifiers

* Addresses possible memory leak during multi-shard transactions

### citus v5.2.0 (August 15, 2016) ###

* Drops support for PostgreSQL 9.4; PostgreSQL 9.5 is required

* Adds schema support for tables, other named objects (types, operators, etc.)

* Evaluates non-immutable functions on master in all modification commands

* Adds support for SERIAL types in non-partition columns

* Adds support for RETURNING clause in INSERT, UPDATE, and DELETE commands

* Adds support for multi-statement transactions involving a fixed set of nodes

* Full SQL support for SELECT queries which can be executed on a single worker

* Adds option to perform DDL changes using prepared transactions (2PC)

* Adds an `enable_ddl_propagation` parameter to control DDL propagation

* Accelerates shard pruning during merges

* Adds `master_modify_multiple_shards` UDF to modify many shards at once

* Adds COPY support for arrays of user-defined types

* Now supports parameterized prepared statements for certain use cases

* Extends LIMIT/OFFSET support to all executor types

* Constraint violations now fail fast rather than hitting all placements

* Makes `master_create_empty_shard` aware of shard placement policy

* Reduces unnecessary sleep during queries processed by real-time executor

* Improves task tracker executor's task cleanup logic

* Relaxes restrictions on cancellation of DDL commands

* Removes ONLY keyword from worker SELECT queries

* Error message improvements and standardization

* Moves `master_update_shard_statistics` function to `pg_catalog` schema

* Fixes a bug where hash-partitioned anti-joins could return incorrect results

* Now sets storage type correctly for foreign table-backed shards

* Fixes `master_update_shard_statistics` issue with hash-partitioned tables

* Fixes an issue related to extending table names that require escaping

* Reduces risk of row counter overflows during modifications

* Fixes a crash related to FILTER clause use in COUNT DISTINCT subqueries

* Fixes crashes related to partition columns with high attribute numbers

* Fixes certain subquery and join crashes

* Detects flex for build even if PostgreSQL was built without it

* Fixes assert-enabled crash when `all_modifications_commutative` is true

### citus v5.2.0-rc.1 (August 1, 2016) ###

* Initial 5.2.0 candidate

### citus v5.1.1 (June 17, 2016) ###

* Adds complex count distinct expression support in repartitioned subqueries

* Improves task tracker job cleanup logic, addressing a memory leak

* Fixes bug that generated incorrect results for LEFT JOIN queries

* Improves compatibility with Debian's reproducible builds project

* Fixes build issues on FreeBSD platforms

### citus v5.1.0 (May 17, 2016) ###

* Adds distributed COPY to rapidly populate distributed tables

* Adds support for using EXPLAIN on distributed queries

* Recognizes and fast-paths single-shard SELECT statements automatically

* Increases INSERT throughput via shard pruning optimizations

* Improves planner performance for joins involving tables with many shards

* Adds ability to pass columns as arguments to function calls in UPDATEs

* Introduces transaction manager for use by multi-shard commands

* Adds COUNT(DISTINCT ...) pushdown optimization for hash-partitioned tables

* Adds support for certain UNIQUE indexes on hash- or range-partitioned tables

* Deprecates \stage in favor of using COPY for append-partition tables

* Deprecates `copy_to_distributed_table` in favor of first-class COPY support

* Fixes build problems when using non-packaged PostgreSQL installs

* Fixes bug that sometimes skipped pruning when partitioned by a VARCHAR column

* Fixes bug impeding use of user-defined functions in repartitioned subqueries

* Fixes bug involving queries with equality comparisons of boolean types

* Fixes crash that prevented use alongside `pg_stat_statements`

* Fixes crash arising from SELECT queries that lack a target list

* Improves warning and error messages

### citus v5.1.0-rc.2 (May 10, 2016) ###

* Fixes test failures

* Fixes EXPLAIN output when FORMAT JSON in use

### citus v5.1.0-rc.1 (May 4, 2016) ###

* Initial 5.1.0 candidate

### citus v5.0.1 (April 15, 2016) ###

* Fixes issues on 32-bit systems

### citus v5.0.0 (March 24, 2016) ###

* Public release under AGPLv3

* PostgreSQL extension compatible with PostgreSQL 9.5 and 9.4