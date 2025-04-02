# Generate a QR Code using RPA and Camunda
This project demonstrates how to integrate a Camunda 8 BPMN Process with a Robot Framework RPA bot to generate QR codes.

## What Does This Project Do?

The project starts with a form where you can input a URL (e.g., `https://camunda.com/contact/`). A BPMN process is then triggered, which activates an RPA bot. The bot opens a web browser, navigates to `https://www.qrcode-monkey.com/`, and generates a QR code for the provided URL. The QR code image is sent back to the process, where a user task displays it for review.

![BPMN Process](./img/bpmn-rpa-qr-process.png)


## Components

<video width="420" height="240" controls>
  <source src="./img/RPAElements.mp4" type="video/mp4">
</video>

### Tools to Build and Run
1. **Camunda Desktop Modeler**: Used to build the RPA script. [Download the Camunda Modeler](https://camunda.com/download/modeler/).
2. **RPA Worker**: Used to run and test the RPA script. [Download and install the RPA Worker](https://github.com/camunda/rpa-worker/releases).
3. **Camunda 8 SaaS**: Used to build and execute the BPMN model. [Create a Camunda 8 SaaS account](https://modeler.camunda.io/) and set up a cluster.

### Artifacts in This Repository
1. `getData.rpa`: The RPA script with instructions for generating the QR code.
2. `Enter URL.form` & `Display QR Code.form`: Web forms for user input and displaying the QR code.
3. `Generate QR Code.bpmn`: The BPMN process that orchestrates the workflow and manages variables and states.

## Setup and Prerequisites

You'll need to get the RPA Worker up and running, gor detailed instructions, refer to the [Camunda RPA Getting Started Guide](https://docs.camunda.io/docs/8.7/components/rpa/getting-started/).

## Creating and Adding Credentials

This project requires two API keys from your Camunda SaaS account. Follow the [instructions here](https://docs.camunda.io/docs/8.7/components/console/manage-clusters/manage-api-clients/) to create API keys.

1. **API Key for Worker**:  
   Used by the workers to fetch and complete tasks. It requires access to **Zeebe**. Details on setting up credentials in your modeler can be found [here](https://docs.camunda.io/docs/components/modeler/desktop-modeler/connect-to-camunda-8/).

2. **API Key for Modeler**:  
   Used by the Desktop Modeler to deploy scripts to your SaaS cluster. It requires access to **Zeebe** and **Secrets**. Instructions for adding the key to the worker are available [here](https://github.com/camunda/rpa-worker/releases).

## Running the Project

### The Process
1. Open the Camunda Web Modeler, create a new project, and upload the `Generate QR Code.bpmn` file.
2. Upload the `Enter URL.form` and `Display QR Code.form` files to the same directory.
3. Deploy the process to your Camunda cluster.

### The RPA Bot
1. Open the RPA Worker properties file and enable Zeebe access by setting:
   ```properties
   camunda.client.zeebe.enabled=true
   ```
2. Go to the Camunda Desktop Modeler and open the `getData.rpa` file. You should see "✅ RPA worker Connected" at the bottom of the modeler.
3. Deploy the `getData.rpa`.

### Run the Process
1. Go to Camunda 8 SaaS tasklist and in the process section find the `Generate QR Code` process and click "Start Process".
2. Enter a URL into the frontend.
3. Wait for the worker to complete its work.
4. See in Tasklist a Usertask will appear showing the QR code.
