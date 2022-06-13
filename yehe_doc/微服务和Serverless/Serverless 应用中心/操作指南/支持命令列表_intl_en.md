Serverless Application Center (SLS) is deployed based on Serverless Framework and supports the following CLI commands:

- **`serverless registry`**: Lists available components.

- **`serverless registry publish`**: Publishes components to the SLS component registry.

   `--dev`: Publishes components of the `@dev` version for development or testing.

- **`serverless init xxx`**: Downloads a specified template from the component registry by entering the name of the template to download after `init`, such as "$ serverless init fullstack".
  
    `sls init xxx --name my-app`: Customizes the project directory name.
	
	 `--debug`: Lists log information during template download.

- **`serverless deploy`**: Deploys a component instance in the cloud.

    `--debug`: Lists log information such as the deployment operations and the status output by `console.log()` during component deployment.

    `---inputs publish=true`: Publishes a new version during function deployment.

    `---inputs traffic=0.1`: Switches 10% of the traffic to the `$latest` function version during deployment and switches the rest of the traffic to the last published function version.
>?The legacy command format `sls deploy --inputs.key=value` has been changed to `sls deploy --inputs key=value` since Serverless CLI v3.2.3. Legacy commands cannot be used in new versions of Serverless CLI. If you have upgraded Serverless CLI, please use the new commands.

- **`serverless remove`**: Removes a component instance from the cloud.

    `--debug`: Lists log information such as the removal operations and the status output by `console.log()` during component removal.

- **`serverless info`**: Gets and displays the information about a component instance.

   `--debug`: Lists more `state` values.

- **`serverless dev`**: Enables the development mode ("DEV Mode") and automatically deploys changed information when component status changes are detected. In development mode, information such as execution logs, invocation information, and errors can be displayed on the CLI in real time. The development mode also supports in-cloud debugging for Node.js applications.


