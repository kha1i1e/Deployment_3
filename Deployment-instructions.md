<p align="center">
<img src="https://github.com/kura-labs-org/kuralabs_deployment_1/blob/main/Kuralogo.png">
</p>

## Deployment Instructions:
1. Create your own Jenkins Server and install the following on the server:
    - Install "python3.10-venv", "python-pip", "unzip"
2. Create a multibranch pipeline and run the build for the application
    - You'll see an option called branch sources. Choose GitHub and enter your GitHub link and credentials. 
4. Follow the install [AWS EB CLI](https://scribehow.com/shared/How_to_install_AWS_EB_CLI__J6eBRB9FQl2fGenfUVemlA) instructions
5. Then, add this stage to your Jenkins file and rerun your build: `stage ('Deploy') {
steps {
sh '/var/lib/jenkins/.local/bin/eb deploy'
}
}
`
6. **IF** your application redeployed successfully, what did you notice?
7. Configure a [Webhook](https://scribehow.com/shared/Setting_up_a_GitHub_webhook_for_Jenkins_deployment__OCRQGNvARfWF4clyeFcsGQ)
8. **BONUS:** Once you've configured your webhook, change the background or some text in the application. **HINT** Look into the HTML or CSS file and ask chatGPT for help
9. Did the application redeploy? 
