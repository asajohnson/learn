Run a local MongoDB server to develop your data application. This process isn't required to use an Azure Cosmos DB database or deploy to Azure App Service.

## Install and run MongoDB

Select a method to install and run a local MongoDB database. The MongoDB needs to be running and able to respond to requests on the default local address and port: `mongodb://127.0.0.1:27017`.

### [Install and run MongoDB locally](#tab/install-local)

If your MongoDB installed, you can skip this section. 

1. Download [MongoDB Community](https://www.mongodb.com/docs/manual/installation/) edition.
1. Install MongoDB community edition.
1. Start your local MongoDB Server.

### [Install and run MongoDB container](#tab/install-container)


1. In Visual Studio Code, select <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>P</kbd> to open the command palette.
1. Search for **Remote-Containers: Reopen in Container**. 

    This sample uses the Node.js + MongoDB dev container.

1. Wait until the web and database containers are started and the integrated terminal shows the container's prompt of `node ➜ /workspace $ `

    When you need to use the terminal for either your web app or database, make sure you are in this container-connected terminal.

---

## Review connection properties

The web app is configured to use the local database.

1. In Visual Studio Code, open the `.env` file. It has the MongoDB connection string, database name and collection name. 

    ```
    PORT=8080
    NODE_DEBUG=app
    MONGODB_URI_CONNECTION_STRING=mongodb://127.0.0.1:27017
    MONGODB_URI_DATABASE_NAME=js-rentals
    MONGODB_URI_COLLECTION_NAME=rentals
    ```

1. The sample application uses this file to connect to the local MongoDB database.  
1. This file isn't deployed to Azure App Service, as defined by the `./.vscode/settings.json` file to ignore it.

    ```
    //./.vscode/settings.json
     {
        "appService.zipIgnorePattern": [
            "node_modules{,/**}", 
            ".env"
        ],
        "appService.deploySubpath": "."
    }
    ```

## Configure MongoDB extension

Configure Visual Studio Code's MongoDB extension to find and use the running local MongoDB database on port 27017.

1. In Visual Studio Code, select <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>P</kbd> to open the command palette.
1. Search for **MongoDB: Connect with connection string**. 
1. Enter the local connection string: `mongodb://127.0.0.1:27017`

## Upload sample data to local database

Use the MongoDB extension's playground feature to upload data into the local MongoDB database. The sample comes with 6 rental properties of information. Import this data into the local database.

1. In Visual Studio Code, select <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>P</kbd> to open the command palette.
1. Search for **MongoDB: Refresh Playgrounds list**. 
1. Select `insert.mongodb` to open the playground.
1. Enter <kbd>Ctrl</kbd> + <kbd>Alt</kbd> + <kbd>R</kbd> to run the entire playground, inserting the data into your local MongoDB database.

## Run local web app

### [Run app with MongoDB locally](#tab/run-local)

1. In the Visual Studio Code integrated terminal, start the local web app to verify it connects to the database:

    ```bash
    npm start
    ```

1. Open a web browser with the following URL to view the sample application:

    ```
    http://localhost:8080
    ```

1. The rental property cards display with data.

### [Run app with MongoDB container](#tab/run-container)

1. In the integrated terminal for the dev container, start the local web app to verify it connects to the database:

    ```bash
    npm start
    ```

1. On your local host computer, open a web browser with the following URL to view the sample application:

    ```
    http://localhost:8080
    ```

1. The rental property cards display with data.

---

## Check your work

* The local MongoDB is running.
* The local web app is running in the browser with data displayed.

