# introDrocker 

A tutorial is based on [Let’s Chat app](https://github.com/containers101/demochat) that was used to familiarize myself with Codefresh functionality.

## Example 

We are going to take this []
[![Let's Chat Greylock](https://codefresh.io/wp-content/uploads/2017/03/lets-chat.png)](https://github.com/containers101/demochats)

![Screenshot](https://codefresh.io/wp-content/uploads/2017/03/11.png)s

## Overview 

This tutorial will go through the process of adding the following:

1. **Build** step - that will build Docker image for your Let’s Chat app

2. **Registry** step - that will push your image to Docker Hub

3. **Test** step - A freestyle step that runs the unit test of the demo chat after the build 

4. **Composition** step - This step will create and launch a composition.

5. **Deploy** step - This stepp will deploy a composition to Kubernetes. 

## Steps

### Build

#### [x] Fork the repo  

Enter the following link and fork Let’s Chat app!: ```https://github.com/containers101/demochat```

#### [x] Add a service
Now enter Codefresh and add the Let’s Chat app as a Codefresh service.

Click on ___Add Repository___

![Screenshot](https://codefresh.io/wp-content/uploads/2017/03/add-repo.png)


Now add your forked demochat repo. We can search for it by typing "introDocker" to search. We can also Add by URL here.

Also, choose the branch for your first build (in this case ```master```)

When you finish press ___Next___.

![Screenshot](https://codefresh.io/wp-content/uploads/2017/03/select-repo2.png)

#### [x] Find the Dockerfile
A **Dockerfile** is a text document that contains all the commands a user could call on the command line to assemble an image. An image is like a stripped down VM that only installs enough software to meet and run your app's dependencies. 

Select how you would like to setup your repository. In this case, our repo has a ___Dockerfile___, so we'll select the middle option. 


![Screenshot](https://codefresh.io/wp-content/uploads/2017/03/15.png)

By default, Codefresh searches for your Dockerfile at the root level of your repository, by the name "Dockerfile", which this repo has. Here's what's in it:
```
# Pick a node version
FROM node:7.10

# Make an app directory and cd into it
RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

# Grab the npm dependencies, install them, then copy them into app/
COPY package.json /usr/src/app/
RUN npm install
COPY . /usr/src/app

# Arguments to pass to bash inside the container at app/
CMD [ "npm", "start" ]
```

![Screenshot](https://codefresh.io/wp-content/uploads/2017/03/16.png)

Review your Dockerfile, and click ___Create___ to add your repository.

![Screenshot](https://codefresh.io/wp-content/uploads/2017/03/17.png)

Clicking on ___Build___  button will trigger a regular build.

![Screenshot](https://codefresh.io/wp-content/uploads/2017/03/18.png)

Great, you  are running  your build for the first time!

### Register 

#### [x] Push your image to Docker registry
A **Docker registry** is a service that holds Docker images, typically grouped together in a repository with the same image names, with generally unique alphanumeric tags. Sort of like how :octocat: Github works for `git` based repositories. 

For this example, we will use the default Docker Registry: [Docker hub](https://hub.docker.com). Click on ___Repositories___, and then click on the ___Pipelines___ gear.

![Screenshot](https://codefresh.io/wp-content/uploads/2017/03/19.png)

Scroll down to ___Workflow___, and you will see a ___Push to Docker___ button. If you have set up your credentials, click ___Save___ at the bottom of the screen. Otherwise- click on the ___integration page___ link.

Write your User/Password info, and click ___Save___ to connect.

![Screenshot](https://codefresh.io/wp-content/uploads/2017/03/20.png)


## Unit test your image
Let's head over to ___Piplines___ again.
![Screenshot](https://codefresh.io/wp-content/uploads/2017/03/19.png)

Scroll down to Workflow under ___Build and Unit Test___

We'll type in ```echo $(date)``` in the Unit Test Script area. This will print the date, and we'll be able to see our test in action.

Let's click ___Save___, and ___Build___ to see it in action.

Great- the date has been printed!

![Screenshot](https://codefresh.io/wp-content/uploads/2017/03/22.png)
 
 
Now let's add a full composition that also contains mongo db.


## Add composition

Our Let's Chat app needs mongo in order to work, so let's add it!

You can read more about compositions in our docs, but we will also walk through the process here :
https://docs.codefresh.io/docs/create-composition


Click the ___Composition___ view icon in the left pane, and click the ___Add Composition___.

![Screenshot](https://codefresh.io/wp-content/uploads/2017/03/1.png)

Choose a name for your composition

![Screenshot](https://codefresh.io/wp-content/uploads/2017/03/2.png)

We are going to build our comp from scrath, so click ___Empty Composition___

![Screenshot](https://codefresh.io/wp-content/uploads/2017/04/empty_comp.png)

Now we will click ___Add Service___ and add demochat, the port (50000), and mongo.
Everything looks good here- so let's go ahead and launch by clicking the rocket ship...

![Screenshot](https://codefresh.io/wp-content/uploads/2017/04/savelaunch_final.png)


Once it has completed, a link to our app will be displayed. Let's click it to see if it worked.


![Screenshot](https://codefresh.io/wp-content/uploads/2017/04/completed_in.png)

Success! We have successfully launched a composition.

![Screenshot](https://codefresh.io/wp-content/uploads/2017/03/10.png)






[app]: https://github.com/containers101/demochat

