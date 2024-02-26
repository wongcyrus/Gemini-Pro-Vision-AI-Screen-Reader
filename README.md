# Gemini Pro Vision AI Screen Reader
Experience the magic of Gemini Pro Vision AI Screen Reader in this thrilling video. We've turbocharged the traditional Google ChromeVox Screen Reader with the mighty power of Google Gemini Pro Vision. Our mission? To tackle the challenge of web image information access for those with visual impairments.

The problem being addressed is the inability of visually impaired individuals to access image information due to the lack of adherence to W3C web accessibility initiatives by websites. Currently, over 80% of websites lack meaningful alternate text for their images. Moreover, it is unfeasible to retroactively add descriptive text to all existing websites manually.

[![Gemini Pro Vision AI Screen Reader for visually impaired - GDSC Solution Challenge 2024](https://img.youtube.com/vi/SUkg_76mF6M/0.jpg)](https://www.youtube.com/watch?v=SUkg_76mF6M)

## Architecture 

Frontend: This project enhances the open-source screen reader, Google ChromeVox Classic, which serves as an extension to the Google Chrome browser. The extension module employs Javascript.

Backend: The backend incorporates the Google Gemini Pro Vision API via the Google cloud function. This API generates descriptive text for images received in either URL or base64 format. The default language for this text is English, although this can be altered by supplying the 'lang' parameter. The text generated by the Gemini API is then sent to the Google Translation API for translation into the selected language, and then returned to the frontend. The cloud functions are developed by Python.

The utilization of ChromeVox Classic screen reader, Cloud Function, and Google Gemini Pro Vision is prevalent. ChromeVox Classic is favored due to its comprehensive functionality and widespread acclaim. Cloud Function is employed owing to its adaptability, ready-to-use environment, superior scalability, and cost-effectiveness. Lastly, Gemini Pro Vision is chosen due to its prowess as the most potent AI model capable of describing an image in a split second, API-based, and its low usage cost.

## Setup procedure

### Frontend:
1. Follow [original instruction](https://source.chromium.org/chromium/chromium/src/+/main:docs/windows_build_instructions.md) to checkout and build ChromeVox Classic
2. Copy and replace all sources under [chromevoxclassic/](chromevoxclassic) to the chromium source under the path ui/accessibility/extensions/chromevoxclassic/
3. After building the ChromeVox Classic browser extension, install the extension under Chrome browser with developer mode turned on
4. Install with "Load unpacked"; the language of generated image description can be configured from the manifest.json by setting the lang code to the attribute "tts_locale", please refer [here](https://cloud.google.com/translate/docs/languages) for supported language codes
5. The cloud function URL can be configured via the attribute "gemini_api" from the manifest.json
6. Reinstall the browser extension after modifying the manifest.json

### Backend: 
#### Manual
This is quick R&D without authenication and rate limit. 
1. Create a new Google Cloud Function, with settings: 2nd gen, memory >= 512 MB, and allow all traffic
2. Copy and replace all sources under [google_cloudfunction/](google_cloudfunction) to your Cloud Function 

#### Production Deplolyment
It includes API Gateway and implements rate limit for each API Key. Fork this repo and create a Codespace.

##### Login your GCP account
```
gcloud auth application-default login
```

##### Create GCP resources
```
./deploy.sh 
```
Record down the output api-url, project-id, and service-name.

##### Enable the API
Set project
```
gcloud auth login
gcloud config set project <project-id>
gcloud auth application-default set-quota-project <project-id>
gcloud services enable <service-name>
```

#### Admin Tools
A set of Python scripts for API key management. 
1. Rename Namelist_template.xlsx to Namelist.xlsx, add user to the excel.
2. Update admin_tools/config.py.


###### Before using admin tools
```
gcloud auth login
gcloud config set project <project-id>
gcloud auth application-default set-quota-project <project-id>
```


# Google Developer Student Clubs Solution Challenge 2024 Submission by [GDCS-HKIIT (Formerly GDSC-IVE)](https://gdsc.community.dev/hong-kong-institute-of-vocational-education/).
