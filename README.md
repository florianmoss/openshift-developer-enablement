# Openshift Developer Enablement
👋👋👋

This is repo contains content for the developer onboarding workshop. Over the coming weeks, we will have multiple sessions together that will include **Workshops**, **self-guided training** and **online classrooms**. 

👀🚨

The main hub for us is the **Miro board**, a link to the board was distributed this morning and will be shared via E-Mail. Please <a href="mailto:fmoss@redhat.com">E-Mail me</a> if you can't find the link or don't have access to the Miro board.

## Week 1 - Workshop - Introduction to OpenShift

We will start with a light introduction, going through the objectives over the next few weeks and introducing OpenShift. 

📫  **Content and Links**

- [Presentation](https://github.com/florianmoss/openshift-developer-enablement/blob/master/week1/OpenShift4%20%20-%20Developers%20Edition.pdf)

📋  **Tasks**

- Confirm your _Miro board access_
- Get yourself a _[developer sandobox](https://developers.redhat.com/developer-sandbox/get-started)_

🥅  **Goals**

- Being able to describe what OpenShift is
- Not being afraid of what's ahead

## Week 2 - Online Classroom - Introduction to Docker/Podman/Containers

The goal for this week is to understand what a container is, how it differs from traditional application, and how a container works.

You can find a **full script** for this session [here.](https://github.com/florianmoss/openshift-developer-enablement/blob/master/week2/containers.md) The script gives a little bit more **background** to the presentation, includes a small **quiz**, and expands on the slides.

If you are interested in the PDF to the **presentation**, please find this [here.](https://github.com/florianmoss/openshift-developer-enablement/blob/master/week2/presentation/ContainersContainersContainers.pdf)

All hands-on exercises are available via the [online lab section.](https://lab.redhat.com/).



## Week 2 - Self Guided Exercises

1. **[mandatory]** 

    Read through the linked material for week 2 and make sure you understand the differences between: image, container, image registry and container runtime. 

2. **[mandatory]** 

    Do the following hands-on labs:

    - [Creating images with Container Tools [buildah]](https://lab.redhat.com/buildah)
    - [Deploying containers using Container Tools [podman]](https://lab.redhat.com/podman-deploy)
    - [Build an application into a container image using RHEL Container Tools](https://lab.redhat.com/containerize-app)

3. **[mandatory, except the last step]**

    - Open a RHEL sandbox environment in the [lab section](https://lab.redhat.com/sandbox).
    - Run ```yum update -y```, this will update your system to the latest versions, unfortunately this takes 5-7 min, keep reading whole your system updates
    - Make sure that ```buildah``` and ```podman``` are installed in your environment. You can use ```yum install <name>``` for this
    - Check how many ```buildah images``` you have present on your host
    - Use this [Dockerfile](https://github.com/florianmoss/openshift-developer-enablement/blob/master/week2/nodeJS-sample/Dockerfile) and this [amazing node.JS application](https://github.com/florianmoss/openshift-developer-enablement/blob/master/week2/nodeJS-sample/app.js) to build a new image. You can create the 3 relevant files with ```vi Dockerfile```, ```vi app.js``` and ```vi package.json``` and copy the content over
    
        **Hint:** ```buildah bud -f Dockerfile -t <image-name> .```

    - Revise the Dockerfile and understand what is happening, the [following resource](https://catalog.redhat.com/software/containers/ubi8/nodejs-12/5d3fff015a13461f5fb8635a) will help you

    - Use ```podman``` to list your local images. Use the image you have created with buildah to ```create``` and ```start``` a container. Use the [podman docs](https://docs.podman.io/en/latest/Commands.html) if needed
    
    - On which port did your container start? 
    
    - Rather than using the Dockerfile, can you build an image using `buildah` CLI commands?

## Week 3 - Online Classroom - Core Kubernetes Concepts

// to be added

## Week 3 - Self Guided Exercises

// to be added

## Week 4 - Online Classroom - Kubernetes/OpenShift for Developers

// to be added

## Week 4 - Self Guided Exercises

// to be added

