README
========
 
This Ansible Galaxy project installs and runs an Optical Character Recognition
session on a portion of a database of 74k images. The session will run on a
cluster of multiple VM's in the Chameleon Cloud.

Requirements
================

You are expected to use a Linux machine which has the following packages installed:
- Git
- Cloudmesh Client (and having a valid cloudmesh.yml file for accessing Chameleon Cloud)
- Ansible

How to use
================

1- Clone the project in home/user/ocr.
```
$ cd ~
$ mkdir ocr
$ cd ocr
$ git init
$ git clone https://github.com/cloudmesh/cloudmesh.ocr.git

```
2- For running the project using cmd5, add the files deploy.py and benchmark.py
as an extension to your CMD5. These modules implement the commands deploy cluster,
deploy stack, and benchmark.
However, an easier and less error-prone way to run the project is to simply run
the following bash files:

deploy_cluster: Creates a cluster of multiple nodes on Chameleon Cloud. After running the bash file, the user will be prompted to enter the number of nodes for the cluster.

deploy_stack: Installs the necessary packages on the cluster nodes. If The authenticity of host is questioned or you get the WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!, just type yes and press ENTER as many times as the number of nodes. However, if the key cannot be found, run {cm key add --ssh} while having a valid key in .ssh directory.

benchmark: Runs the OCR on the cluster nodes. The input data in this case is the
standard database of Chars74k. 200 different fonts of all the Alphanumeric glyphs
(0-9, A-Z, a-z) will be separated into two parts, train and test. The KNN classifier
will classify the test data, after being trained by the train data. The accuracy
of the classifier will be returned as the result.

ocr: Runs the whole algorithm on an image. After running the module, the user will
be prompted to enter the URL of the input image.

Commands:

```
$ bash ~/ocr/code/deploy_cluster.sh
$ bash ~/ocr/code/deploy_stack.sh
$ bash ~/ocr/code/benchmark.sh
$ bash ~/ocr/code/ocr.sh
```

The results of benchmark will be saved in ocr/accuracy and the results of OCR will
be saved in ocr/ocr_results. These directories will be created automatically.
The results will also be printed in the terminal.
