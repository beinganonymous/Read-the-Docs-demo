# Application for GSoC 2020 : Multiple File Uploads
----------

# About Me
## Personal Information

**Name** : Chetan D Patil
**Country** : India
**Email** : [chetanpatilonmail@gmail.com](https://mail.google.com/mail/u/0/?view=cm&fs=1&tf=1&source=mailto&to=chetanpatilonmail@gmail.com)
**GitHub** : [beinganonymous](https://github.com/beinganonymous)
**Major** :  Bachelors of Technology in Information Technology Engineering
**College** : [Vishwakarma Institute of Information Technology, Pune, India](https://viit.ac.in/)
**Time Zone**: Indian Standard Time (UTC + 5:30)


# Interest in App Inventor
----------

I first learnt about MIT App Inventor in 2017. I was looking for tools to develop Android Application and then i came to know about two tools MIT App Inventor and Android Studio. System requirements of Android studio was too high hence i choose to go with MIT App Inventor, since then i love to use MIT App Inventor for developing mobile apps.  It is such a great platform for developing computational thinking, and I am very eager to contribute to the effort.


# Interest in introductory programming 
----------

I have been learning introductory programming since 2016. I have good understanding of various programming languages such as C, C++, Java, Python.

**C/C++**: I was introduced to computer programming through the language C during the first year of my college, I have been coding in C and C++ since then for the implementation of Data Structures and Algorithms for courses in my college as well as for Competitive Coding. I have also used C for coding basic computer networks.

**Java**: I gained experience of coding in Java through the Object Oriented programming course during the second year of my college.

**Python**: I have done various projects in Python involving various applications of Machine Learning and Deep Learning like Data analysis, Audio processing, Image segmentation and am very fluent in coding in Python.

I have also taken Hands on Session for Android with Kotlin for 3 days where i have covered introductory programming with Kotlin and developed some Android apps with Kotlin. Here is Session plan that i have used ([Session](https://github.com/beinganonymous)). Also i have taken Seminar on Git Workflow at my University.  

# Proposed summer project
----------
## Why me ?

I am pursuing my bachelors in Information at Vishwakarma Institute of Information Technology. I have won few competition such as Smart India Hackathon which is National Level Hackathon in India and developed a road safety app for same, I have developed some real-time application such as secure chatting which provides external data security by encrypting messages and decrypt  same when needed. I have contributed in open source for DevFest App for Google Developer Group Pune. I have cleared the third level of Google's Foo Bar challenge. 
I have contributed on two issues in MIT App Inventor [#2071](https://github.com/mit-cml/appinventor-sources/issues/2071) and [#2107](https://github.com/mit-cml/appinventor-sources/issues/2107). Through this Google Summer of Code project, I hope to contribute good quality code to the MIT App Inventor project.


## Title

Designer Projects : Multiple File Uploads


## Abstract

**MIT App Inventor** is a web application integrated development environment. It allows newcomers to computer programming to create application software(apps). This project focuses on improving the capacity of current designer to allow multiple file uploads.
The current designer only allows uploading one asset at a time. If you need to upload 10 images, you need to do the process 10 times. It would be a much better experience to be able to upload a number of assets in one go.

Most of my work has been centred around fixing bugs during the user on-boarding process. Further, [#2071](https://github.com/mit-cml/appinventor-sources/issues/2071) which helped me familiarize with different parts of the code-base to a good extent.


## Deliverables:

The deliverables of the project would be as follows:

1. **An improvement in the currently existing file chooser**: 

   Current file chooser only support to upload one file at a time, so this deliverable will add support to current file          chooser to allow multiple file upload in one go.
    
2. **Test cases for Multiple File Uploads**: File upload is an important part of any web application. We can test file upload either using manual testing or using automation testing. Following elements should be tested while uploading files.

    - Test the phrase upload is correctly aligned with the upload button.
    - Verify, a window is opened once this upload button is clicked.
    - Make sure, cancel button works during the upload process.
    - Test, only the particular file types can be uploaded. For example doc or pdf, or image files like jpeg, bmp, png etc.
    - Verify uploaded file cannot exceed a certain size. For example, uploaded file cannot exceed 2 MB size.
    - Make sure, multiple file upload is working properly if the application under test (AUT) demands such scenario.
    - Test timeout function is working properly. For Ex: upload should be canceled automatically after, say 5 minutes.
    - Verify, the progress of upload function is working properly.
    - Make sure file upload process can resume, in case of network connectivity problem. (Once the problem is rectified).
    - Test empty upload is not working.
    - Verify multiple uploads of the same file is not allowed.
    - Make sure a new copy of the uploaded file is created to avoid overwriting.
    - Test drag and drop file options to upload is working properly besides the traditional way of uploading.
    - Once the file is uploaded or error in uploading, proper redirection happens to a web page or part of an application.
         
3. **Project Documentation**: 
    
    Write a proper documentation for project with proper test cases.

4. **Some general issues** **:** 
    
    - Delete key does not prompt deletion in designer -(issues [#2040](https://github.com/mit-cml/appinventor-sources/issues/2040))
    - Add property to File to use app external data dir rather than whole storage partition -(issues #[1833](https://github.com/mit-cml/appinventor-sources/issues/1833))
    - Drag and Drop Support to upload files -(issue [#2122](https://github.com/mit-cml/appinventor-sources/issues/2122))
    
    
## Approach
----------

### An improvement in the currently existing file chooser

The current designer only allows uploading one asset at a time. If you need to upload 10 images, you need to do the process 10 times. It would be a much better experience to be able to upload a number of assets in one go.
****

- **Allow File Chooser to select multiple files** : 
    
    Improve current file chooser allow to select multiple files at a time. After opening computer window it should allow to       select multiple files at a time. A pseudo-code to implement this :
    
        JFileChooser chooser = new JFileChooser();
        chooser.setMultiSelectionEnabled(true);
        chooser.showOpenDialog(frame);
        File[] files = chooser.getSelectedFiles();


- **Implement POST multipart request operation to understand that more than one file :** 

   Add File inputs in browsers to support multiple file selection and implement POST operation to understand that more than    one file might come in a request and to handle it accordingly. 

   Multipart utility class uses ``java.net.HttpURLConnection`` class and follows the [*RFC 1867*](http://www.ietf.org/rfc/rfc1867.txt) *(Form-based File Upload in HTML)* to make an HTTP POST request with ``multipart/form-    data`` content type in order to upload files to a given URL. It has one constructor and three methods:

    - ``**MultipartUtility**(String requestURL, String charset)``: creates a new instance of this class for a given request URL and charset.
    - void ``**addFormField**(String name, String value)``: adds a regular text field to the request.
    - void ``**addHeaderField**(String name, String value)``: adds an HTTP header field to the request.
    - void ``**addFilePart**(String fieldName, File uploadFile)``: attach a file to be uploaded to the request.
    - ``List<String> **finish**()``: this method must be invoked lastly to complete the request and receive response from server as a list of String.
        
   Client side pseudo code to implement multipart request.     
   ```public class MultipartFileUploader { 
        public static void main(String[] args) {
            String charset = "UTF-8";
            File uploadFile1 = new File("e:/Test/PIC1.JPG");
            File uploadFile2 = new File("e:/Test/PIC2.JPG");
            String requestURL = "http://localhost:8080/FileUploadSpringMVC/uploadFile.do";
            try {
                MultipartUtility multipart = new MultipartUtility(requestURL, charset);
                multipart.addHeaderField("User-Agent", "CodeJava");
                multipart.addHeaderField("Test-Header", "Header-Value");
                multipart.addFormField("description", "Cool Pictures");
                multipart.addFormField("keywords", "Java,upload,Spring");
                multipart.addFilePart("fileUpload", uploadFile1);
                multipart.addFilePart("fileUpload", uploadFile2);
                List<String> response = multipart.finish();
                System.out.println("SERVER REPLIED:");
                for (String line : response) {
                    System.out.println(line);
                }
            } catch (IOException ex) {
                System.err.println(ex);
            }
        }
    }```
****    
### Test cases for Multiple File Uploads

   File upload is an important part of any web application. We can test file upload either using manual testing or using        automation testing.
   ****

- **Make sure, cancel button works during the upload process :** 
    ```public class ClientAbortMethod {
        public final static void main(String[] args) throws Exception {
            CloseableHttpClient httpclient = HttpClients.createDefault();
            try {
                HttpGet httpget = new HttpGet("");
                System.out.println("Executing request " + httpget.getURI());
                CloseableHttpResponse response = httpclient.execute(httpget);
                try {
                    System.out.println("----------------------------------------");
                    System.out.println(response.getStatusLine());
                    httpget.abort();
                } finally {
                    response.close();
                }
            } finally {
                httpclient.close();
            }
        }
    }```


- **Test, only the particular file types can be uploaded :**
    We can check file type with ``file.getContentType()` and allow only particular file types to be uploaded.
    
- **Verify uploaded file cannot exceed a certain size :** We can count buffer size of file and implement this feature.
   ``` int size = 0;
    while ((read = uploadedInputStream.read(buffer)) != -1) {
        out.write(buffer, 0, read);
        size += read.length;
    }```
    
- **Test empty upload is not working :**
    Check empty upload using ``if (projectImg.isEmpty()) { ... }``


****
## Implementation Plan
----------

The following timeline shows my implementation plan.  I have allocated to various aspects of the project. This is by no means the final time allocation, and with the guidance of the mentors I hope to update this.


Title |     Dates    | Description
--- | --- | ---
Application Review Period<br> | March 31, 2020 - May 4, 2020 |  I will revise the basics of Google Web Toolkit. I will learn more about the File Upload in GWT. I will get myself more familiarized with the current Designer.<br>
Community Bonding<br> | May 3, 2020 - June 1, 2020 |  I will study about Designer Projects and will create a more detailed timeline after interacting with the mentors. I plan to stay active in discussions about Multiple File Upload as well as other projects in Designer. I will interact with the community, the mentors and the other students having different projects.<br>
Coding Period(Week 1)<br> | May 31, 2020 - June 6, 2020 |  Weekly Deliverables : Improve current file chooser allow to select multiple files at a time. After opening computer window it should allow to select multiple files at a time.<br>
Coding Period(Week 2)<br> | June 8, 2020 - June 14, 2020 |  Weekly Deliverables : Improve current file chooser to support drag and drop file support for multiple files.<br>
Coding Period(Week 3)<br> | June 15, 2020 - June 21, 2020 |  Weekly Deliverables : Add File inputs in browsers to support multiple file selection and implement POST operation to understand that more than one file might come in a request and to handle it accordingly.<br>
Coding Period(Week 4)<br> | June 22, 2020 - June 28, 2020 |  Weekly Deliverables : Add Multipart Request to upload parts in parallel to improve throughput because smaller part size minimizes the impact of restarting a failed upload due to a network error.<br>
Evaluations (Phase 1)<br> | June 28, 2020 - July 3, 2020 |  Testing working of file chooser, improving documentation and submission.<br>
Coding Period(Week 5, 6 and 7)<br> | July 4, 2020 - July 24, 2020 |  Implementing various test cases regarding file uploads in browser.<br>
Evaluations (Phase 2) (Week 8)<br> | July 25, 2020 - August 1, 2020 |  Testing implemented test cases, improving documentation and submission.<br>
Coding Period( Week 9, 10, 11 and 12)<br> | August 1, 2020 - August 24, 2020 |  Write and improve documentation, solve issues related Designer section.<br>
----------


# Experience with the development tools
----------
## **Android Development with the Java SDK**

The Android project that I am the most proud of is SafeDriveDroid. I completed this project as part of a hackathon and [won first prize](https://www.aicte-india.org/sites/default/files/sihwinners.pdf) at the Smart India Hackathon 2018. I was an intern android developer at [Arishti CyberTech Pvt.Ltd](http://www.arishti.com/). As part of this internship, I got the opportunity to work on Face Recognition for android device using Deep Learning and uploading multiple file to server at a time using multipart request. Furthermore, I have also developed chatting application which is based on Cloud Database and also includes features like Encryption & Decryption for internal data security. This app has feature like Image To Text and Speech To Text([source code](https://github.com/beinganonymous/SecureChatDroid))


## **Javascript**

I have developed my personal portfolio using javascript and jkyll([source code](https://github.com/beinganonymous/beinganonymous.github.io)). Also I have developed Paying Guest Rental System using javascript which allow you to rent a room in any given location where i have used The Maps JavaScript API.


## Google Web Toolkit

I am currently working on issues in MIT App Inventor Project where i am working on GWT to open dialog box when remove screen button is clicked([#issue2071](https://github.com/mit-cml/appinventor-sources/issues/2071)) and Replace Move to Trash button with Delete from Trash when View Trash button is clicked([#issue2107](https://github.com/mit-cml/appinventor-sources/issues/2107)).

****
# Experience with teams, online developer communities and large code bases
----------

I have contributed to the various issues on MIT App Inventor Project. While working on this issues, I learnt the importance of prompt and clear communication. I often saw lot of ideas come up during code design, implementation and code review process. I got know coding styles used in MIT App Inventor Project, also i got know about contribution guidelines of MIT App Inventor Project. I have also contributed to one issue in Intel/dffml repository where i was working on continuous integration environment to detect trailing white spaces in repository

**Open source contributions:**

**Working on Issues :**

| **Issue Number**                                                    | **Description**                                      | **Status** |
| ------------------------------------------------------------------- | ---------------------------------------------------- | ---------- |
| [#2071](https://github.com/mit-cml/appinventor-sources/issues/2071) | Type name to delete project/screen                   | *Open*     |
| [#2107](https://github.com/mit-cml/appinventor-sources/issues/2107) | Move to Trash menu item changes to Delete from Trash | *Open*     |
| [#2122](https://github.com/mit-cml/appinventor-sources/issues/2122) | Drag and Drop Support to upload files                | *Open*     |

**Pull Requests :**

| **PR**<br>**Number**                                              | **Description**                                            | **Status** |
| ----------------------------------------------------------------- | ---------------------------------------------------------- | ---------- |
| [#2101](https://github.com/mit-cml/appinventor-sources/pull/2101) | Fixes Type name to delete project/screen                   | *Open*     |
| [#2116](https://github.com/mit-cml/appinventor-sources/pull/2116) | Fixes Move to Trash menu item changes to Delete from Trash | *Open*     |

Pull Requests (other than MIT App Inventor) :

| **PR**<br>**Number**                            | **Description**             | **Status** |
| ----------------------------------------------- | --------------------------- | ---------- |
| [#237](https://github.com/intel/dffml/pull/237) | Trailing WhiteSpace Checker | *Closed*   |

Currently Working On :

https://github.com/mit-cml/appinventor-sources/pull/2116

****
# Application challenges
----------
## **Challenge 1: Creating a non-trivial app**
1. **Expense Tracker** :
    The App assists users keep track of their day-to-day expenses by managing their incomes, expenses, and review their balances at any time.
    [AIA](https://uce71715cc1f06f713c0a67b2d11.dl.dropboxusercontent.com/cd/0/get/A0sgyVH8UfffRN2xlB6CIsN5QlactGJNAB5ftXFbbP-7gixHdZNenGWQb8FNL9mWFKxUhcxMG3plNTQEbfgLf7gEOfJ3jDS9lLipXMTIWYksW9MfpcungaVIa_pP-otkosY/file?dl=1#) | [APK](https://uc439443c66eaad90b8d85af0b8a.dl.dropboxusercontent.com/cd/0/get/A0vM2UYkz3y7sp2W_RZXdJtXatCk_bupAxHF2haIaLaIcXTUI778kkV7Jl5yucJwezqidIW_U-hJgK-QzrkYsC241GbEarwQPAzhwEB13Rg_LOIMwPNht8ggR-Kmna2EY98/file#)
    
2. **Russian Roulette :**
    It is a game based of Russian Roulette. In this case we have a revolver for 6 bullets. First Reload revolver putting a single bullet and rotating the drum. The bullet will be located randomly in one of the six sites. Then let 's pressing randomly the different buttons. If the number instead of the bullet matches the number of the button pressed, the screen turns red.
    [AIA](https://uc0bbdbec42f70a6ee909f14cc69.dl.dropboxusercontent.com/cd/0/get/A0skb-HM4MvVzN_uJTlIZatLkvD5lEmKWU8-uAfCC_5r3JWRm1E_MuMPB33n8yNx0gOwA2wyC4VpFdBSm-3r6qnHv4xf6pJwVvect6gkaBclTClOuSqgI_5FXGSFvXrH1DU/file#) | [APK](https://ucbc57273590db97d75544f0ca88.dl.dropboxusercontent.com/cd/0/get/A0vx3aJXHmmxddhFdm8b4dgn5vA9LxwGaWSd9KDG9rodxcxMd0Z5HLyygY9zl39Q-27xPLMvO2VqPOAsY2xCiiNSvindYuhN7FjN84fHQdCcZ2oP5x0C_sFKddhwU5Tnyzk/file#)


## **Challenge 2:Design challenge -- Enhancing the Camera operation**


- **useFront Property :**
    This [issue](https://github.com/mit-cml/appinventor-sources/issues/180) says that, "[the useFront] property relied on an undocumented feature of the android camera system". This feature has been removed from nearly all androids, including older ones including 2.3 devices. There exists no intent to specify which camera to use, and the user should decide what camera to use. There was a well-known risk that it may stop working someday. That day came when there is an upgrade in Android OS from jellybean to kitkat. Furthermore, according to [this comment](https://github.com/mit-cml/appinventor-sources/pull/335#issuecomment-86684286), App Inventor has always used an intent to launch the external camera app, and that intent does not have any way of specifying, and it definitely cannot query device state. Therefore, this property was removed from the AI design and block interfaces.


- **Design Solution :**
    Properties Needed: **frontCamera**, **backCamera**.
    Methods Needed: **IsSelected**, TakePicture (already there)


- **Implementation :**
    Due to the limitations across different APIs and devices in how selecting the camera upon intent passing, it would be better if we discard the existing Camera component (working on Intent) and replace it with new component working on Camera API.


    According to the [Camera API documentation](http://developer.android.com/reference/android/hardware/Camera.html#open(int)), we can utilize the **Camera.open(int id)** method of the **Camera** class, where **id** refers to the camera the user has specified in the property list.


    Camera API Methods Explanation :
      getParameters()-Get existing (default) camera settings


     setParameters(Camera.Parameters)-Modify the returned Camera.parameters object


     takePicture(Camera.ShutterCallback, Camera.PictureCallback, Camera.PictureCallback, Camera.PictureCallback)- It captures the photo and wait for the callbacks to provide the actual image data.

Takes Picture using Back Camera(To use front camera change CAMERA_FACING_FRONT )

    private Camera.PictureCallback mPictureCallback = new Camera.PictureCallback() {
        @Override
        public void onPictureTaken(final byte[] bytes,final Camera camera) {
    
            // Do something here ... save, display ...here in our application,we have to pass the clicked picture to AfterPicture
        }
    };
    public void takePictureBack(ControllerState state){
    
        Camera camera = null;
        int cameraCount = Camera.getNumberOfCameras();
        for (int cameraId = 0; cameraId < cameraCount; cameraId++) {
            Camera.CameraInfo cameraInfo = new Camera.CameraInfo();
            if (cameraInfo.facing == Camera.CameraInfo.CAMERA_FACING_BACK) {
                    camera = Camera.open(cameraId);
                    break;
                }
            }
        if (camera!= null) {
            Camera.Parameters params = camera.getParameters();
    
            // Check what resolutions are supported by your camera
            List<Camera.Size> sizes = params.getSupportedPictureSizes();
    
    
            // Iterate through all available resolutions and choose one.    
            for (Camera.Size size : sizes) {
                ... 
            }
            params.setPictureSize( ... );
            camera.setParameters(params);
    
            camera.setPreviewDisplay(mCameraSourcePreview.getSurfaceView().getHolder());
            camera.startPreview();      
            camera.takePicture(null,null,mPictureCallback)
        }
    }


