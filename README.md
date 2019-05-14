# keda-azure-function

This [Helm](https://helm.sh) chart parameterizes a deployment of an [Azure Function](https://docs.microsoft.com/en-us/azure/azure-functions/) on [KEDA](https://github.com/kedacore/keda) such that it can be operationalized with a [CI/CD pipeline](https://azure.microsoft.com/en-us/services/devops/) or [GitOps workflow](https://github.com/microsoft/bedrock).

## Usage

This chart is intended to be used in conjunction with a upstream CI/CD pipeline that builds a Docker container for your Azure Function. 

Adjust all of the values of the included `values.yaml` file to match the needs of the Azure Function you'd like to deploy:

```yaml
image: docker.io/myaccount/mycontainer:mytag
functions:
- myfunction 
secrets:
  AzureWebJobsStorage: "DefaultEndpointsProtocol=https;EndpointSuffix=core.windows.net;AccountName=mystorageaccount;AccountKey=dWR7tgY...Aq0w=="
  FUNCTIONS_WORKER_RUNTIME: node
triggers:
- metadata:
    connection: AzureWebJobsStorage
    direction: in
    name: myitem 
    queueName: myqueue 
    type: queueTrigger
  type: azure-queue
```

An Azure Queue trigger is used here as an example but any trigger type that is supported by KEDA is supported.  
