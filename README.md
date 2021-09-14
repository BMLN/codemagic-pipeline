# codemagic-pipeline


## prerequisites 

- appledeveloper account
- $APP_STORE_CONNECT_API_KEY
- $APP_STORE_CONNECT_API_KEY_ISSUER_ID
- $APP_STORE_CONNECT_API_KEY_KEY_ID
#####
- a new private key (generate with ...)
- codemagic api key
- git api key (for versioning)




## CI/CD

### functionality
1. git(lab)-ci sends api call to codemagic to start the build
2. use codemagics' app-store-connect fetch-signing-files to get the signing profiles on to the build machine
3. run fastlane build
4. run fastlane pilot

### git(lab) - CI/CD
We can execute commands everytime we push to the repository where we develop. Here, it will call the codemagic-API
and pass the protected variables of the repository:
- CODEMAGIC_API_KEY
- APPLE_API_KEY
- APPLESTUFFBLABLA

everytime we make changes on the master branch. Codemagic offers a service that makes it possible to run our iOS - build and deployment on a macOS-machine (which is demanded for iOS applications)

### codemagic - CI/CD

codemagic will now use the environment variables we passed in our API-call to build and deploy 
our application with the help of fastlane - on macOS.
Before our assigned machine can do that we need to fetch the right certificates from apple or generate a matching one through the APP-STORE-API and install fastlane.


### fastlane

fastlane is a tool to simplify iOS/Android deployment. We use it here to build and deploy our application.
So our deployment machine later has to have fastlane with its packages installed. 

fastlane will run with our environment variables:
- APP_STORE_CONNECT_API_KEY_KEY
- APP_STORE_CONNECT_API_KEY_KEY_ID
- APP_STORE_CONNECT_API_KEY_ISSUER_ID
- [will need the rest of the app details]

to

1. build the package and sign it with the defined certificate information
2. upload the package to testflight with the help of the api key


