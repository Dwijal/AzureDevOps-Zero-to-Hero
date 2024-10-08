# Day 7 - Azure Artifacts 👨‍💻

## Check out the video below for Day7 👇
(https://youtu.be/krK4HTmaCJc)

## Setup your Azure repos with the same application code

You can import the below repo to clone the Nike landing page sample website code to your Azure Repos:

https://github.com/piyushsachdeva/nike_landing_page.git

**Note:** You must set the app settings as below to disable all file caching:

*  WEBSITE_DYNAMIC_CACHE=0
*  WEBSITE_LOCAL_CACHE_OPTION=Never
  

## Architectural diagram used in the video

![image](https://github.com/piyushsachdeva/AzureDevOps-Zero-to-Hero/assets/40286378/f7facb49-af0d-4f6a-8e14-ae8444423c91)


We have 3 views in the Azure Artifacts and the artifact is published into these view we can set the rule in Azure app servie to trigger the Deploy Pipeline.

To perform actions on this artifact the Feed should have 2 permission i.e. on organization level and project level. It should have Contributor role.

1)Project Collection Build Service 
2)Projcect_name Build Service

## Build Pipeline YAML code:

``` YAML
trigger: 
- main

stages:
- stage: Build
  jobs:
  - job: Build
    pool:
      vmImage: 'ubuntu-latest'
    steps:
    - task: Npm@1
      inputs:
        command: 'custom'
        customCommand: 'install -D tailwindcss postcss autoprefixer'
    - task: Npm@1
      inputs:
        command: 'custom'
        customCommand: 'run build'

    - task: Npm@1
      inputs:
        command: 'publish'
        workingDir: './dist'
        publishRegistry: 'useFeed'
        publishFeed: '$FEED_DETAILS'
```



### Post-deployment inline script in the Release pipeline

```
cp -rf /home/site/wwwroot/package/* /home/site/wwwroot/
```


