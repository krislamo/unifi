# UniFi Network Server Deployment

This project provides a simple setup for self-hosting a UniFi Network Server
inside a container to manage Ubiquiti networking gear. It leverages the
community-managed linuxserver.io container to save time and engineering effort.

## Requirements
- Docker / Docker Compose
- `pwgen` (optional, for password generation)

## Compatibility
Starting with version 8.1 of UniFi Network Application, MongoDB versions 3.6
through 7.0 are supported.

## Quick Start
Follow these steps to get your UniFi Network Server up and running.

1. Clone this repository and navigate to the project directory

2. Copy the example MongoDB initialization script
    ```txt
    cp example-init-mongo.js init-mongo.js
    ```

3. Change the default password to a random string
    ```txt
    sed -i "s/changeme/$(pwgen -s 32 1)/g" init-mongo.js
    ```
  Note: This command requires `pwgen`. If you don't have it installed, you can
  manually edit the file and replace "changeme" with a strong password of your
  choice.

4. Set the following environment variables in the `.env` file
  - `UNIFI_VERSION`: The desired UniFi Network Application version
  - `MONGO_VERSION`: The desired MongoDB version
  - `MONGO_PASS`: The password you set in step 3

5. Start the containers using Docker Compose:
    ```txt
    docker-compose up -d
    ```

## Version Selection

### UniFi Network Application
It's recommended to install the
[latest UniFi version](https://github.com/linuxserver/docker-unifi-network-application/releases),
preferably by specifying the version number. You can omit the `-lsXX` suffix if desired.

### MongoDB
It's highly recommended to use a specific version tag for
[MongoDB](https://www.mongodb.com/try/download/community) since there are no
automatic upgrades between major versions.

**Note:** Modern MongoDB relies on AVX support. You might encounter issues with
pre-Tiger Lake Celeron and Pentium CPUs on versions after 4.4. For non-AVX
systems, you can use version 4.4.

## Additional Information
For more details and configuration options, please refer to the
[linuxserver/docker-unifi-network-application](https://docs.linuxserver.io/images/docker-unifi-network-application/)
documentation.

## License
This project is free software under the [Zero-Clause BSD](LICENSE).
