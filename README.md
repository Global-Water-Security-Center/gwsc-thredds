# THREDDS Configuration for GWSC Services

This repository contains example configuration files for a THREDDS server. It uses the Docker image for THREDDS and can be created easily with the docker-compose command.

To use:
1. Create a new `thredds` user on your system and add yourself to the corresponding group:

    ```bash
    useradd -m thredds
    usermod -aG thredds ${USER}
    ```

2. Restart to make the changes take effect. Very that you now belong to the `thredds` group with the following command:

    ```bash
    groups
    ```
   
3. Review the docker-compose recipe and environment in the `docker-compose.yml` and `compose.env` files.
   
    a. Tweak the volume paths to your desired locations.
    b. Set the `TOMCAT_USER_ID` and `TOMCAT_GROUP_ID` environment variables to the id of the `thredds` user and group you created in step 1. Run the following command to see the ids of the groups you belong to:
   
    ```bash
    id
    ```

4. Copy the the `tomcat-users.xml` file from https://github.com/Unidata/thredds-docker/tree/master/files into the top level directory of this repo (same level as this README). DO NOT COMMIT THIS FILE.

5. Run the following command to create and start the docker container:

    ```bash
    docker-compose up
    ```

6. Press `ctrl-C` to stop the container. 
   
7. After starting the first time the following directories will be added to the data directory: `public`, `cache`, and `logs`. Add the write group permission to any files and directories in the data directory that are owned by the `thredds` user:

    ```bash
    chmod g+w <files>
    ```

8. Place data in the `data\public` directory and change owner and group to be `thredds` user. Be sure both owner and group permissions have read and write access.

   **Note:** Refer to the `README` in the [gwsc-ingest respository](https://github.com/Global-Water-Security-Center/gwsc-ingest) for instructions on how to produce the datasets referred to in the `era5Catalog.xml`.

10. Modify the `*.xml` files in the data directory to add new datasets to the THREDDS server. The root THREDDS catalog file is `catalog.xml`

11. Start/stop the THREDDS container using the docker-compose commands:

    ```bash
    docker-compose start
    docker-compose stop
    ```
