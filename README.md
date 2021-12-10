# Openshift Developer Enablement
👋 &nbsp;👋 &nbsp;👋 &nbsp;👋 &nbsp;👋 &nbsp;👋 &nbsp;👋 &nbsp;👋

This is repo contains content for the developer onboarding workshop. Over the coming weeks, we will have multiple sessions together that will include **Workshops**, **self-guided training** and **online classrooms**. 

👀 &nbsp; 🚨

The main hub for us is the **Miro board**, a link to the board was distributed this morning and will be shared via E-Mail. Please <a href="mailto:fmoss@redhat.com">E-Mail me</a> if you can't find the link or don't have access to the Miro board.

## Week 1 - Workshop - Introduction to OpenShift

We will start with a light introduction, going through the objectives over the next few weeks and introducing OpenShift. 

📫 &nbsp; **Content and Links**

- [Presentation](https://github.com/florianmoss/openshift-developer-enablement/blob/master/week1/OpenShift4%20%20-%20Developers%20Edition.pdf)

📋 &nbsp; **Tasks**

- Confirm your _Miro board access_
- Get yourself a _[developer sandobox](https://developers.redhat.com/developer-sandbox/get-started)_

🥅  &nbsp; **Goals**

- Being able to describe what OpenShift is
- Not being afraid of what's ahead

## Week 2 - Online Classroom - Introduction to Docker/Podman/Containers

The 🥅 &nbsp; for this week is to understand what a container is, how it differs from traditional application, and how a container works.

You can find a 💡 **full script** for this session [here.](https://github.com/florianmoss/openshift-developer-enablement/blob/master/week2/containers.md) The script gives a little bit more **background** to the presentation, includes a small **quiz**, and expands on the slides.

If you are interested in the  📑 &nbsp; **PDF** to the **presentation**, please find this [here.](https://github.com/florianmoss/openshift-developer-enablement/blob/master/week2/presentation/ContainersContainersContainers.pdf)

All hands-on exercises are available via the [online lab section.](https://lab.redhat.com/) More on this below.



## Week 2 - Self Guided Exercises

1. **[mandatory]** &nbsp; 💪 &nbsp; 👶

    Read through the linked material for week 2 and make sure you understand the differences between: image, container, image registry and container runtime. 

2. **[mandatory]** &nbsp; 💪 &nbsp; 👶 

    Do the following hands-on labs:

    - [Creating images with Container Tools [buildah]](https://lab.redhat.com/buildah)
    - [Deploying containers using Container Tools [podman]](https://lab.redhat.com/podman-deploy)
    - [Build an application into a container image using RHEL Container Tools](https://lab.redhat.com/containerize-app)

3. **[mandatory, except the last step]** &nbsp; 💪 &nbsp; 🥷

    - Open a RHEL sandbox environment in the [lab section](https://lab.redhat.com/sandbox).
    - Run ❗ ```yum update -y``` ❗, this will update your system to the latest versions, unfortunately this takes 5-7 min, keep reading whole your system updates
    - Make sure that ```buildah``` and ```podman``` are installed in your environment. You can use ```yum install <name>``` for this
    - Check how many ```buildah images``` you have present on your host
    - Use this [Dockerfile](https://github.com/florianmoss/openshift-developer-enablement/blob/master/week2/nodeJS-sample/Dockerfile) and this [amazing node.JS application](https://github.com/florianmoss/openshift-developer-enablement/blob/master/week2/nodeJS-sample/app.js) to build a new image. You can create the 3 relevant files with ```vi Dockerfile```, ```vi app.js``` and ```vi package.json``` and copy the content over
    
        **Hint:** ```buildah bud -f Dockerfile -t <image-name> .```

    - Revise the Dockerfile and understand what is happening, the [following resource](https://catalog.redhat.com/software/containers/ubi8/nodejs-12/5d3fff015a13461f5fb8635a) will help you

    - Use ```podman``` to list your local images. Use the image you have created with buildah to ```create``` and ```start``` a container. Use the [podman docs](https://docs.podman.io/en/latest/Commands.html) if needed
    
    - On which port did your container start? 

    - 🔑 &nbsp; Rather than using the Dockerfile, can you build an image using `buildah` CLI commands?

## Week 3 - Online Classroom - Core Kubernetes Concepts

The 🥅 &nbsp; for this week is to understand what Kubernetes is, how Kubernetes works and what you absolutely must understand as a developer. This week is a step up from last week and will require additional reading. 💥 &nbsp; Please spend some time outside of the theory and practical session on revising the theory.

You can find a 💡 **full script** for this session [here.](https://github.com/florianmoss/openshift-developer-enablement/blob/master/week3/kubernetes.md) The script gives more **background** to the presentation and expands on the slides - it also includes references to additional reading.

If you are interested in the &nbsp; 📑 &nbsp; **PDF** to the **presentation**, please find this [here.](https://github.com/florianmoss/openshift-developer-enablement/blob/master/week3/presentation/kubernetes.pdf)

## Week 3 - Self Guided Exercises
This week is tough &nbsp; 💪 &nbsp;, no doubt. You will have to go through the theory more than once and do a good amount of reading.

But let's finally get to the fun &nbsp; 🤠 &nbsp; part!

You should have requested your [OpenShift Developer Sandbox](https://developers.redhat.com/developer-sandbox/get-started) over the past 2 weeks, please access it now.


![terminal icon](week3/images/terminal.png)

In the top right, please select the ```Terminal``` icon (left from the "?"). You will see that a terminal opens at the bottom of your screen.

Expand the terminal by dragging it up.

![terminal opens](week3/images/terminal2.png)


1. **Some basis kubectl commands**
    - Run ```kubectl --help``` and have a look at the options available to you. 
    - Check which namespace you are currently using: ```kubectl config view --minify | grep namespace:```
    - Deploy your first container in a pod: ```kubectl run nginx --image=nginx```
    - Confirm that the pod deployed successfully: ```kubectl get pods```
    - What do you see in the status? Minimise the terminal first. Select ```Project``` -> ```username-dev``` -> ```Pods``` (scroll down)

    ![Opening a project](week3/images/task1.png)
    
    ![Investigating pods](week3/images/task1-2.png)

    Select the ```nginx``` pod and click on ```Events```.

    Damn, it looks like we tried pulling an image from docker.com but they don't like that anymore!

2. **Deploying a Pod**
    - We can easily avoid this issue by deploying an image that we are pulling from a different registry, like quay.io: ```kubectl run hello-world --image=quay.io/redhattraining/hello-world-nginx```
    - Now, list all Pods in your current namespace
    - We have never actually written a YAML file for this, that's why we want to review what we just created: ```kubectl run hello-world --image=quay.io/redhattraining/hello-world-nginx```
    - Are there any resource restriction applied to our pod? Such as memory or CPU constraints?
    - Delete the pod ```hello-world``` that we created earlier

3. **Createing a Deployment**
    - Use the following YAML specification to deploy your first ```Deployment```, make use of the ```kubectl apply -f <file>.yaml``` command:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxUnavailable: 50%
  replicas: 4
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: quay.io/redhattraining/hello-world-nginx:latest
        ports:
        - containerPort: 80
```

- Minimize your terminal and have a look around, visually inspect the new Deployment in the GUI


![Investigating deployment](week3/images/deployment1.png)

![Investigating deployment](week3/images/deployment1-2.png)

- Manually delete one of the pods as seen in the image below. What do you think is gonna happen?

![Investigating deployment](week3/images/deployment1-3.png)

- Can you explain why we have still 4 pods running? 

- Change the deployment config to 5 replicas (you can use the terminal or OpenShift GUI). Verify that 5 containers are running.

## Week 4 - Online Classroom - Kubernetes/OpenShift for Developers



// to be added

## Week 4 - Self Guided Exercises

// to be added

