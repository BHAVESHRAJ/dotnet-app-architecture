# eShopModernizedMVC

## How to: dockerize the app
1. Add Docker files to the project:
   * In Visual Studio right click on the project -> Add-> Docker support
   * The docker-compose files are created plus the dcproj.
2. Add the environment variables to the docker-compose.override and create a .env file. Containers will use docker-compose, not the web.config, so the settings that need to be set must be there. This environment variables must be caught in the application and used instead of the application settings. In our apps this is done in the CatalogConfiguration class.

## How to: run application in Windows Server 2016 with Containers
1. Create the docker image:
   * Build the solution in Release to build the eshopmodernizedmvc image.
   * When the build is done, open a Powershell prompt and execute ```docker images``` and in the list of images must appear eshopmodernizedmvc with tag _latest_
2. Publish the image in the Container Registry, in this case ACR:
   * Create one ACR on Azure. Take note of the address (e.g. myprivateacr.azurecr.io) and the user and password of the registry.
   * Login to the container registry. From a Powershell execute ```docker login -u dockerUser -p dockerPassword myprivateacr.azurecr.io``` using the values of your ACR
   * Add to the image our ACR address as a prefix to indicate where it must be published. Execute ```docker tag eshopmodernizedmvc myprivateacr.azurecr.io/eshopmodernizedmvc``` to mark it for publishing in the ACR. After this if you execute ```docker images``` this new _myprivateacr.azurecr.io/eshop/modernizedmvc must appear in the list of images.
   * Publish the tagged image executing ```docker push myprivateacr.azurecr.io/eshopmodernizedmvc```
   * Note: to publish in Docker hub instead of ACR, the login step is the same (with Docker Hub credentials), and skip the tag step because by default docker will publish to Docker Hub.
3. Run the image in the VM:
   * Create one VM in Azure. Select Windows Server 2016 Datacenter with containers. This way Docker is already installed and configured.
   * Copy the files _docker-compose.nobuild.yml_, _docker-compose.override.yml_ and _.env_ to the VM in a folder.
   * Edit the .env to put the IP of the VM in the variable.
   * Edit the _docker-compose.nobuild_ file to add the prefix of your ACR eshop/modernizedmvc:

          > image:myprivateacr.azurecr.io/eshop/modernizedmvc
 
   * If your image is in a private registry, login first. For ACR would be to execute in the VM ```docker login -u dockerUser -p dockerPassword myprivateacr.azurecr.io```.
   * Run ```docker-compose -f .\docker-compose.nobuild.yml -f .\docker-compose.override.yml up```. The first time the images will be downloaded from the registry, so this step can take some minutes the initial execution.
   * After this open the browser and write http://{ip of the VM}:5114 and the app should open.
 

