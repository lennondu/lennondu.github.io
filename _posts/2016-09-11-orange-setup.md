---
layout: post
title: Orange Install
category: ubuntu
permalink: others/orange-install
---

## Orange Setup

This is a tutorial of Orange in Ubuntu 16.04. For more details, you can go to [official tutorial](http://biolab.github.io/datafusion-installation-guide/).

*First*, you need to install the necessary system packages:
{% highlight bash linenos %}
    sudo apt-get update
    sudo apt-get install git python-pip python-virtualenv \
        python3-dev python3-numpy python3-scipy \
        python3-pyqt4 python-qt4-dev python3-sip-dev libqt4-dev \
        libgraphviz-dev graphviz
{% endhighlight %}

There is one thing to note that if you have installed virtualenv by pip, you'd better uninstall that and reinstall it by apt.

In order to keep your environment clean, you'd better use virtual enviroment.

*Second*, you need to create a virtual enviroment.

{% highlight bash linenos %}
    mkdir orange3env
    virtualenv -p python3 --system-site-packages orange3env
    source orange3env/bin/active
{% endhighlight %}

Of course, you can create virtual environment without the parameter --system-site-packages.

*Third*, you can install Orange and its requirements.

{% highlight bash linenos %}
    git clone https://github.com/biolab/orange3
    cd orange3
    pip install -r requirements.txt
    pip install -r requirements-gui.txt
    python setup.py develop
    cd ..
    git clone https://github.com/biolab/orange3-datafusion
    cd orange3-datafusion
    python setup.py develop
{% endhighlight %}

*Fourth*, you can run it.

{% highlight bash linenos %}
    python -m Orange.canvas
{% endhighlight %}
