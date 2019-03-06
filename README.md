# tensorflow-wheels

Steps to build TensorFlow from source:

    $ docker build -f Dockerfile_buildenv -t tf-buildenv .
    $ docker run -it -v <OUTPUT_DIR>:/out tf-buildenv
    (container) $ git pull
    (container) $ git checkout <RELEASE_BRANCH>
    (container) $ ./configure
    (container) $ bazel build --config=opt --copt=-msse4.1 --copt=-msse4.2 //tensorflow/tools/pip_package:build_pip_package
    (container) $ ./bazel-bin/tensorflow/tools/pip_package/build_pip_package /out
    $ pip install <OUTPUT_DIR>/tensorflow-1.12.0-cp36-cp36m-linux_x86_64.whl
