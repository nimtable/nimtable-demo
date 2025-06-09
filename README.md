<!--
 Licensed to the Apache Software Foundation (ASF) under one
 or more contributor license agreements.  See the NOTICE file
 distributed with this work for additional information
 regarding copyright ownership.  The ASF licenses this file
 to you under the Apache License, Version 2.0 (the
 "License"); you may not use this file except in compliance
 with the License.  You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

 Unless required by applicable law or agreed to in writing,
 software distributed under the License is distributed on an
 "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
 KIND, either express or implied.  See the License for the
 specific language governing permissions and limitations
 under the License.
-->

# Nimtable Quickstart Image

Nimtable helps you easily manage and explore Apache Iceberg catalogs. With a web-based platform designed for clarity and simplicity, Nimtable makes it easy to browse tables, run queries, analyze file distributions, and optimize storage layouts.

This is a docker compose environment to quickly get up and running with a Spark environment and a local REST
catalog, MinIO as a storage backend, and Nimtable for Iceberg lakehouse management.

**note**: If you don't have docker installed, you can head over to the [Get Docker](https://docs.docker.com/get-docker/)
page for installation instructions.

## Usage

```bash
docker-compose up
```

Wait for all services to start.

The services available are:
- **Jupyter Notebooks**: http://localhost:8888 (create and manage data)
- **Nimtable Web Interface**: http://localhost:3000 (explore and analyze data)
- **MinIO Console**: http://localhost:9001 (view storage)


The environment comes with a collection of pre-built Jupyter notebooks that demonstrate various Iceberg features and capabilities. **Use these notebooks to learn Iceberg concepts hands-on, while using Nimtable to visualize and monitor the tables you create**.

### How to Use the Notebooks
1. **Open both interfaces**: Access Jupyter at http://localhost:8888 and Nimtable at http://localhost:3000
2. **Start learning**: Browse the available notebooks in Jupyter and choose one to start with.
3. **Run and observe**: Execute notebook cells (Shift+Enter) and immediately check Nimtable to see table changes
4. **Compare states**: After each major operation in the notebook, refresh Nimtable to observe:
   - New tables being created
   - Schema evolution
   - Snapshot history
   - File organization
5. **Experiment**: Modify notebook code and see the real-time impact in Nimtable

**💡 Pro Tip**: Keep both Jupyter and Nimtable open in separate browser tabs for the best learning experience. As you create, modify, and optimize tables in the notebooks, you can immediately see the results in Nimtable's intuitive interface.

## Alternative Access Methods

While the notebook server is running, you can also use these command-line tools:

```bash
docker exec -it spark-iceberg spark-shell
```
```
docker exec -it spark-iceberg spark-sql
```
```
docker exec -it spark-iceberg pyspark
```

To stop everything, just run `docker-compose down`.

## Troubleshooting & Maintenance

### Refreshing Docker Image

The prebuilt spark image is uploaded to Dockerhub. Out of convenience, the image tag defaults to `latest`.

If you have an older version of the image, you might need to remove it to upgrade.
```bash
docker image rm tabulario/spark-iceberg && docker-compose pull
```

### Building the Docker Image locally

If you want to make changes to the local files, and test them out, you can build the image locally and use that instead:

```bash
docker image rm tabulario/spark-iceberg && docker-compose build
```

### Use `Dockerfile` In This Repo

To directly use the Dockerfile in this repo (as opposed to pulling the pre-build `tabulario/spark-iceberg` image), you can use `docker-compose build`.

### Deploying Changes

To deploy changes to the hosted docker image `tabulario/spark-iceberg`, run the following. (Requires access to the tabulario docker hub account)

```sh
cd spark
docker buildx build -t tabulario/spark-iceberg --platform=linux/amd64,linux/arm64 . --push
```

---

For more information on getting started with using Iceberg, checkout
the [Quickstart](https://iceberg.apache.org/spark-quickstart/) guide in the official docs.

The repository for the docker image is [located on dockerhub](https://hub.docker.com/r/tabulario/spark-iceberg).
