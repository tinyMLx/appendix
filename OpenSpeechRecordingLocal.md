## Using the Open-Speech-Recording Application Locally to Develop Your Own Dataset

If you would like to run the open-speech-application locally please follow the instructions below. In order for this to work you need to have [```Python``` installed](https://www.python.org/downloads/) on your local machine as well as the [python package manager ```pip```](https://packaging.python.org/tutorials/installing-packages/).

We have [forked a version](https://github.com/tinyMLx/open-speech-recording/) of Pete's Open-Speech-Recording application to use only local memory which you can use to record your own datafiles. If you'd like a more robust version that you want to share with others to aid in your data collection (and therefore use a google storage buckets which may cost some money) please see [Pete's original project](https://github.com/petewarden/open-speech-recording). You can setup and use our version of the app as follows.

1. Clone the repository and install the only requirement, flask:
  ```
  git clone https://github.com/tinyMLx/open-speech-recording.git
  pip install flask
  ```

2. You can then run the server locally (from within the open-speech-recording folder) by running:
  ```
  cd open-speech-recording
  export FLASK_APP=main.py
  python -m flask run
  ```

3. Then open the link provided in the terminal in a web browser to run the application. Make sure to **run the application in a private or incognito window** which avoids any cacheing issues. Also we've found that the app works best when **using Chrome** so if you are having issues with another browser please try it in Chrome.

4. The application can then be run as specified in the [edX course instructions](https://github.com/tinyMLx/courseware/raw/master/edX/readings/4-6-6.pdf). Once you are done recording, click to download the audio files. You will find that instead of downloading the files indivudally or via a zip, you now have a large collection of ```.ogg``` files in your open-speech-recording directory.

5. You can now safely kill the flask app from the command line by running ```cntrl+c``` (or ```cmd+c```) and can now proceed to formatting your audio files and then training your model in Colab.