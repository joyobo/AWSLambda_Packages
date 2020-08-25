# AWSLambda_Packages
A repository explaining how to make Python Libraries into AWS Lambda compatible packages as a Layer.

## Using Linux Environment
If you are using LinuxOS, this YouTube tutorial would satify your needs. <br>
<i>AWS lambda with OpenCV via Layers, video by Srce Cde - https://youtu.be/FQBT8vVRkAg </i> <br><br>
In short, 
1. Using Linux Terminal, pip3 install the Python libraries you want into a specific folder of directory build/python/lib/python3.8/site-packages
<br>For more information on the directory to use, take a look at: <i>AWS Developer Guide - Including library dependencies in a layer - https://docs.aws.amazon.com/lambda/latest/dg/configuration-layers.html#configuration-layers-path </i>
2. then zip up the python folder at build/python.
In your /build directory, you should have the /python/lib/python3.8/site-packages folder and the zipped folder (python.zip)
3. Create a S3 bucket (this bucket needs to be in the same region as your AWS Lambda function)
4. Upload the zip file. 
5. Go to AWS Lambda, create a new layer, upload file from S3.
6. Use this layer in your AWS Lambda function.
7. Now, you can import that library in your function's code!

## Using Windows Environment
If you are using WindowsOS, following the steps for LinuxOS will not work. This is because, AWS Lambda runs in the amazonlinux OS. And the package you created by following the LinuxOS is configurated/build for your local WindowsOS environment.

There are multiple ways to go about this:
1. Docker and EC2
Compiling the libraries in an instance type of amazonlinux OS environment <br>
    - Medium - <i>How to create an AWS Lambda python 3.6 deployment package using Docker - https://medium.com/i-like-big-data-and-i-cannot-lie/how-to-create-an-aws-lambda-python-3-6-deployment-package-using-docker-d0e847207dd6 </i>
    - GitHub Link - <i>lambda layers for python runtime by hidekuma - https://github.com/hidekuma/lambda-layers-for-python-runtime </i>
2. Using pypi and wheel <br>
    This is by far the easiest. <br>
    <i>AWS Support - How do I add Python packages with compiled binaries to my deployment package and make the package compatible with Lambda? - https://aws.amazon.com/premiumsupport/knowledge-center/lambda-python-package-compatible/ </i><br>
    <br>
    Rephrasing:
    1. At pypi.org. https://pypi.org/ , search the library that you want and navigate to the Download Files page <br>
    eg, https://pypi.org/project/numpy/#files
    2. Download appropriate .whl file <br>
    eg, <br>
    For Python 3.8, download numpy-1.19.1-cp38-cp38-manylinux1_x86_64.whl <br>
    For Python 3.7, download numpy-1.19.1-cp37-cp37m-manylinux1_x86_64.whl 
    3. Check if you have wheel library in your environment.<br>
        - Using command prompt, check if you have wheel installed
        ```
        pip3 show wheel
        ```
        - To install wheel, type
        ```
        pip3 install wheel
        ```
     4. Uncompress wheel file
     ```
     wheel unpack <dir-to-wheel_file>
     ```
     5. Move the relevant folders into a directory build\python\lib\python3.8\site-packages <br>
     eg, in the case for (opencv) cv2, dlib, imutils, numpy, your build\python\lib\python3.8\site-packages should look like this
     
     6. Zip up the python folder at build\python. <br>
     In your \build directory, you should have the build\python\lib\python3.8\site-packages folder and the zipped folder (python.zip)
     
     7. Create a S3 bucket (this bucket needs to be in the same region as your AWS Lambda function)
     8. Upload the zip file. 
     9. Go to AWS Lambda, create a new layer, upload file from S3.
     10. Use this layer in your AWS Lambda function.
     11. Now, you can import that library in your function's code!
