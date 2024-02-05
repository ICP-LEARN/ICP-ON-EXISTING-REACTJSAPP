
# Deploying an Existing ReactJS Application on the Internet Computer

## Overview

This guide provides step-by-step instructions on how to deploy an existing ReactJS application as a frontend canister on the Internet Computer.

## Prerequisites

1. An existing ReactJS application.
2. [DFX](https://sdk.dfinity.org/docs/download.html) installed and configured on your machine.

## Step 1: Build Your ReactJS Application

1. Open a terminal and navigate to the root directory of your ReactJS project.

    ```bash
    cd /path/to/your/reactjs/project
    ```

2. Build your ReactJS application using the appropriate command:

    ```bash
    npm run build
    ```

    If you are using Yarn:

    ```bash
    yarn build
    ```

    Ensure the build process completes successfully, and the static assets are generated in a `build` folder.

## Step 2: Update dfx.json

1. In the root directory of your project, create a `dfx.json` file if not already present.

2. Open `dfx.json` and add the following configuration:

    ```json
    {
      "canisters": {
        "app": {
          "frontend": {
            "entrypoint": "build/index.html"
          },
          "source": ["build"],
          "type": "assets"
        }
      },
      "output_env_file": ".env"
    }
    ```

    Ensure that `"entrypoint"` and `"source"` point to the correct file and folder, respectively.

## Step 3: Generate Candid Definitions

1. Run the following command to generate Candid definitions:

    ```bash
    dfx generate
    ```

## Step 4: Deploy the Project

1. Deploy the ReactJS application locally:

    ```bash
    dfx deploy
    ```

2. Deploy the ReactJS application on the Internet Computer mainnet:

    ```bash
    dfx deploy --network ic
    ```

    After running this command, you will see a generated link where you can navigate to your ReactJS application.

## Step 5: View the Frontend Canister

1. Replace `<canister-id>` in the following URL with the actual canister ID provided during deployment:

    ```bash
    http://127.0.0.1:8000/?canisterId=<canister-id>
    ```

    This URL will allow you to access and view your ReactJS application on the Internet Computer.

## Conclusion

Congratulations! You have successfully deployed your existing ReactJS application as a frontend canister on the Internet Computer. Feel free to share your application with others or explore further capabilities provided by the Internet Computer ecosystem.

