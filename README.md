# Generate a QR Code using RPA and Camunda
This is an example project that integarate a Camunda 8 BPMN Process with a Robot Framework RPA bot. 

## What Does this project do

This project is started with a form that asks you to add a URL `https://camunda.com/contact/`. From there a BPMN process is kicked off. The first task then activates an RPA bot that opens a web browser, goes to `https://www.qrcode-monkey.com/` and generates a QR Code for the URL in question. It then sends an image of hte QR Code back to the process where a user task displays the QR Code for all to enjoy. 

![img](./img/bpmn-rpa-qr-process.png)


## What are the components

### Tools To Build and Run
1. Camunda Desktop Modeler
    1. Building the RPA Script
1. RPA Worker
    1. Running & Testing the RPA Script
1. Camunda 8 SaaS 
    1. Building and Excuting the BPMN Model

### Artifacts in this repo
1. `getData.rpa` - This is the script given to the worker with the instructions on how to get the QR Code
1. `Enter URL.form` & `Display QR Code.form` - These are just web forms which get data from the user for the bot to use and also show the restuls of the rpa bot's adventure in cyberspace!
1. `Generate QR Code.bpmn` - This is the BPMN Process that holds the variables and the state as well as orchestrating the other components

## How to install and Run

Create a C8 SaaS account
download the modeler
download and install the rpa worker

## Create Creds

1. API Key for Worker.
1. API Key for Modeler. 
