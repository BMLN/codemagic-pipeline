# codemagic-pipeline
#### react-native iOS build/deployment CI/CD Template

needed project structure:

      |
      |___/src/
      |___/ios/
      |___/android/

## prerequisites 
1. App Store Connect API Key, including:
   - APP_STORE_CONNECT_API_KEY
   - APP_STORE_CONNECT_API_KEY_KEY_ID
   - APP_STORE_CONNECT_API_KEY_ISSUER_ID
2. Codemagic integration with your repository, including:
    - Codemagic User API Key
    - Codemagic AppID
3. the rest of the App information:
    - BUNDLE_ID
    - XCODE_SCHEME
4. <b>*ANY*</b> RSA 2048 bit private key, you can use:
   - ssh-keygen -t rsa -b 2048 -m PEM -f ./new_key -q -N ""
#####


## CI/CD

### functionality
1. send an api call to codemagic to start the build with git CI/CD
2. use codemagics' app-store-connect fetch-signing-files to get the signing profiles on to the build machine
3. run fastlane build
4. run fastlane pilot

### gitlab/github - CI/CD
Everytime we push to master branch of the repository it will call the codemagic-API
and pass the protected variables of the repository to enable building there.
Codemagic offers a service that makes it possible to run our iOS- build and deployment on a macOS-machine (which is demanded for iOS applications)

### codemagic - CI/CD

codemagic will now use the environment variables we passed in our API-call to build and deploy 
our application with the help of fastlane - <b>*on macOS*</b>.
Before our assigned machine can do that we need to:
1. fetch the right certificates from apple or generate a matching one through the APP-STORE-CONNECT-API 
2. install the project dependencies 
3. install fastlane

Now, finally we are ready to go!


## fastlane

fastlane is a tool to simplify iOS/Android deployment. We use it here to build and deploy our application.
So our deployment machine later has to have fastlane with its packages installed. 

fastlane will run its commands with the configuration defined through the *Fastfile* and
the *environment variables* we set. For further information on that, look into the *Fastfile* provided here.


