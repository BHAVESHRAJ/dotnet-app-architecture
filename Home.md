# eShopModernized (MVC, Web Forms apps and N-Tier app (WCF service) deployed as Windows Containers into Azure)

## Documentation
Check the multiple posts at the Wiki on the right side in order to know how to containerized the base apps or how to deploy to Azure (Windows 1026 VM, Kubernetes-ACS or Service Fabric) the already containerized version of the apps.

## Current version features

- ASP.NET MVC app containerized with Windows Containers
- ASP.NET WebForms app containerized with Windows Containers
- Winforms accessing WCF containerized with Windows Containers
- Deployment metadata and detailed procedures to deploy to the following environments:
    . Regular Windows Server 2016 VM (Virtual MAchine)
    . ACS-Kubernetes orchestrator cluster
    . Service Fabric orchestrators cluster

## Future Roadmap
- Include procedures on how to create CI/CD pipelines in VSTS (Visual Studio Team Services) with releases deploying to VM (Windows Server Containers Docker Host), ACS-Kubernetes and Service Fabric
- User of Azure Active Directory for authentication and authorization
- Uploading the Product Catalog images to Azure Storage Blobs
- Further Hybrid-cloud, networking and security considerations

## FEEDBACK
Feel free to submit your issues plus suggest possible features to be added to the sample applications at the ISSUES section of this current GitHub repo.
