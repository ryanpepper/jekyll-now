---
layout: post
title: Environment Modules and Anaconda
---

One of the best pieces of software I use on a day to day basis is called Environment Modules. It's an open source project, and probably most often it is used on high-performance computing servers to allow users to load versions of software packages - one user might need to switch compiler, or version of Python, or between other software.

Anaconda on the other hand, is a piece of software for cross platform distribution and management of software. Normally people use it for installign Python, but you can install many other things through it, such as the GCC toolchain. Anaconda is really great for getting people set up with software that can otherwise be very difficult to install. However, one side effect is that in order to use it, you need to add it's directory to your PATH environment variable. Of course, this then means that the software installed by your operating system (such as through apt on Ubuntu) is superseded by the versions installed through Anaconda. This is exactly the point of Anaconda, of course, but it can be very confusing for people that aren't aware of this.

A lot of people therefore recommend not adding Anaconda to your PATH explicitly in the shell configuration, and this is probably pretty good advice. It can be a bit annoying to have to manually edit the PATH variable, however. Setting it is not too bad, but think for example, of a situation where you're working in a shell and realise that you no longer want to use Anaconda Python, but need the system Python.

This is where Environment Modules can come to the rescue. Adding and removing directories from your PATH and setting other environment variables is exactly what Environment Modules does, and it's really easy to set up. There are plenty of guides for actually installing the software out there, so I won't bother replicating that here, but here is the module file I use to load Anaconda:

{% highlight tcl %}
#%Module1.0#####################################################################
##
## modules anaconda/5.0.0
##
## modulefiles/anaconda/5.0.0
##
proc ModulesHelp { } {
        global version modroot
        puts stderr "anaconda/5.0.0"
}

module-whatis   "anaconda/5.0.0"

# for Tcl script use only    
set     version         5.0.0
set     sys             linux86
# This line is what adds the Anaconda directory
prepend-path    PATH            /path/to/anaconda/directory/bin
{% endhighlight %}
