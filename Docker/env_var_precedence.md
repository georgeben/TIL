### List of ways to set environmental variables in your docker container with decreasing order of precedence.  

1. Setting environemt variables from the application running in the container. Your app can explicitly set environment variables e.g `process.env.ENV_VAR_NAME=value`
2. Adding the environment varaible to the current shell session e.g export NAME=VAR before running the container
3. Setting environment varaibles using the CLI. Example: `docker run -e ENV_VAR_NAME=VALUE`
4. Setting environment variables via an .env file. An env file can be specified using the --env-file command line argument. When using docker-compose, values starting with $ are automatically replaced with values from an .env file in that directory.
5. Setting environment varaibles in the Dockerfile using the ENV command.
