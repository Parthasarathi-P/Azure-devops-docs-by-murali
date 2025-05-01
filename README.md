# Azure-devops-docs-by-murali
documents shared by murali all docs
# one drive link
https://drive.google.com/drive/folders/1ffTm_fX9FHz5Q5N3eOZgfZom4fHhyZcn

#azure parallelism request rise portal
https://forms.office.com/pages/responsepage.aspx?id=v4j5cvGGr0GRqy180BHbR5zsR558741CrNi6q8iTpANURUhKMVA3WE4wMFhHRExTVlpET1BEMlZSTCQlQCN0PWcu&route=shorturl

# Parallal job request portal.
https://forms.office.com/pages/responsepage.aspx?id=v4j5cvGGr0GRqy180BHbR5zsR558741CrNi6q8iTpANURUhKMVA3WE4wMFhHRExTVlpET1BEMlZSTCQlQCN0PWcu&route=shorturl

# Request tracking portal
https://forms.office.com/Pages/DesignPageV2.aspx?saveresponseformid=v4j5cvGGr0GRqy180BHbR5zsR558741CrNi6q8iTpANURUhKMVA3WE4wMFhHRExTVlpET1BEMlZSTC4u&saveresponseid=123676&rcrequirelogin=true&lrpring=MSFT&lrpsession=1db70731-427a-4a53-8079-f58606f43060&d1obforrc=1&prevsubpage=rcfre&rcsidebar=0

# Devops organization creation steps - by microsoft
1. Login to the portal and search for Azure Devops Organization.
2. You will see the below options.
3. Click on Get started using Azure DevOps and click on Open Azure Devops.
4. You can check your Organizations in https://aex.dev.azure.com/me?mkt=en-US

# In order to push the Images to ACR or to deploy on Webapp by using Azure Devops Pipeline, we must assign the Devops user as owner role for azure resources.

# to deploy lms on webapp by dynamic cofiguration using ACR, Redis, flexi server and environment variable ravi sir code does not workd that is node 16.
for this we are using murlai's repo code that is forked to "hiparthapanda" github name of repo is lms-app

# Deploy lms to static webapp before deploy pipeline runs in azure devops or github from where and which branch web app is pulling code go there and in .env update backend url 
ex- VITE_API_URL=https://webapp-lms-be-hkbjamgke7akfwc6.eastus-01.azurewebsites.net/api

================================================================
create postgres use container instance instance of AKS
use environment variables for AKS
host frontend on webapp
================================= 
done---- not functionating as expected request goes to backend but backend api to db fetch did not work 
this was due to an issue
--Mixed content: load all resources via HTTPS to improve the security of your site
Even though the initial HTML page is loaded over a secure HTTPS connection, some resources like images, stylesheets or scripts are being accessed over an insecure HTTP connection. Usage of insecure resources is restricted to strengthen the security of your entire site.

Reason of the issue-
this issue triggers if we are deploying site backend by using container instance that is on http not on https
but the site running on static webapp comes from https. so, frontend header reading data from non secure http creates an issue.

Resolutio-
static always runs on https we can't change it to http, here we must look for a solution where container instance will be on https.

how i resolved
deployed the frontend on webapp by creating frontend image
on web app configuration setting modified
FTP state - all allowed
HTTPS Only - off

then browse frontend site and on browser in place of https:// keep http://
it will open as not secure and the site will be accessable
=================================================================================

lms backend deployment on AKS and stories 9 all deployment yamls and entire repo forked from mubeen is stored on hiparthapanda github.
repo name -lms-public-yamls


==================================================
Don't follow mubeen's document on attaching acr to aks fail.
if' it's success it does not give a clear message it shows same null ony.

verify by cmd-
role assignment list \
  --scope $(az acr show --name lmsimages --query id --output tsv) \
  --query "[?roleDefinitionName=='AcrPull']" \
  --output table
==================================================

If you disabled local account on the cluster and went for microsoft entra ID authentication with RBACK
1. create group add members to the group.
2. assign role on cluster for the group.
3. if you delete that group before that you must enable individual role on the group else it won't work
4. if deleted the group by miss then create a new group and add the group to the cluster.
5. here the group will have acess in inside cluster resources.
     az aks update \
        --resource-group self-hosted-cluster-RG \
        --name SNP-AKS \
        --aad-admin-group-object-ids 508de1e3-31f1-4d9f-916d-07251dbf7e77

   executable on bash.

   ======================================================

   

