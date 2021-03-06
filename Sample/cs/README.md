## Product Recommendations Sample

The sample under the [Recommendations.Sample](./Recommendations.Sample) folder is a C# sample that shows how to use an API endpoint provisioned by
the Recommendations preconfigured solution. You can find more details about the Recommendations preconfigured solution here: https://aka.ms/recotemplate. 
The sample uses an API client autogenerated using [AutoRest](https://www.nuget.org/packages/autorest/) using the Recommendations service swagger file availble under https://<service_name>.azurewebsites.net/swagger/docs/v1 .
 
The sample demonstrates how to:
 
 1. Train a product recommendations predictive models based on historical transaction data and information on the product catalog
 2. Get Item-to-Item Recommendations from a trained model
 3. Get Personalized Recommendations from a trained model
 4. Set a model to be the default model, and request recommendations from the default model
  
## Pre-Requirements
The steps below are explained in more detail in the [Getting Started Guide](../../getting-started.md)
 
1. Before you can run the application you need to deploy the Recommendations Template. See [Deployment Instructions](../../doc/deployment-instructions.md) for more detail
 
2. You will get an API Key as part of the deployment process and the url of your solution. 
Set the *apiAdminKey* and *recommendationsEndPointUri* variables in *Recommendations.Sample/Program.cs* file based on those values

3. You will need to upload your catalog and usage events data for training to some container in the service's blob storage account

>Note that training a recommendation model is performed using a single catalog file (optional) and at least one (but potentially multiple) usage events files. 

Any usage events files need to be **uploaded to a folder** under the blob container. 
The path of that folder will have to be specified as the '*usageRelativePath*' parameter in the [train new model API request](../../doc/api-reference.md#train-a-new-model). It is also possible to set '*usageRelativePath*' to a single specific usage file. 
 
Similarly, any usage events file(s) used for evaluation, should be uploaded to a **separate folder** under the blob container. 
The path of that folder will have to be specified as the '*evaluationUsageRelativePath*' parameter in the [train new model API request](../../doc/api-reference.md#train-a-new-model). It is also possible to set '*evaluationUsageRelativePath*' to a single specific usage file. 

The **catalog file** can be uploaded directly under the container **or** nested under some subfolder(s). 
The path to the catalog file (including its name) will have to be specified as the '*catalogFileRelativePath*' parameter in the [train new model API](../../doc/api-reference.md#train-a-new-model).

As a summary, the following parameters are used to specify the locations of the various data inputs to model training process:
* blobContainerName
* trainUsageRelativePath  
* trainCatalogFileRelativePath (**optional*)
* evaluationUsageRelativePath (**optional*)
   
Learn more about [model training parameters here.](../../doc/api-reference.md#model-training-parameters-schema).
 

