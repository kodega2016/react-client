# React JS Dockerized Appliction deployment on AWS Elastic Beanstalk

In this project, we will deploy a React JS application to AWS Elastic Beanstalk using Docker. We will use Docker to containerize the React JS application and Elastic Beanstalk to deploy and manage the application in a load-balanced and scalable environment.


So let's get started.

First of all, we need to create and dockerize a React JS application. We will use the create-react-app to create a new React JS application. If you don't have create-react-app installed on your system, you can install it using the following command.

```bash
npx create-react-app react-docker
```

After that,we have to create a Dockerfile in the root directory of the project. The Dockerfile will look like this:

```Dockerfile
FROM node:alpine as builder
WORKDIR /app
COPY ./package.json .
RUN npm install
COPY . .
RUN npm run build

FROM nginx
EXPOSE 80
COPY --from=builder /app/build /usr/share/nginx/html
```

After that, lets create new Elastic Beanstalk environment with the
AWS Management Console.

After that, we have to create a new Elastic Beanstalk application and environment. To do this, follow the steps below:

1. Open the AWS Management Console and navigate to the Elastic Beanstalk dashboard.
2. Click on the "Create New Application" button.
3. Enter the application name and description.
5. Select the "Web server environment" option.
6. Enter the environment name and description.
7. Select the "Docker" platform.
8. Click on the "Create environment" button.

After that, we have to create github workflow to deploy the application to Elastic Beanstalk.
You can find the github workflow file in the .github/workflows directory.

After that, we need to create an AWS IAM user with the AWS Elastic Beanstalk Full Access policy attached. We will use this IAM user to deploy the application to Elastic Beanstalk.

And create a new secret in the GitHub repository with the AWS access key and secret key of the IAM user.

After, that the application will be deployed to the Elastic Beanstalk environment automatically when you push the code to the GitHub repository.
