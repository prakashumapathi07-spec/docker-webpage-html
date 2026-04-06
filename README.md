# docker-CICD-any-app-question-3

Step 1: create a Dockerfile
*****************
FROM nginx:latest
COPY index.html /usr/share/nginx/html/index.html
EXPOSE 80
*****************

step 2: create a deployment.yaml file
apiVersion: apps/v1
kind: Deployment
metadata:
  name: html-demo

spec:
  replicas: 2

  selector:
    matchLabels:
      app: html-demo

  template:
    metadata:
      labels:
        app: html-demo

    spec:
      containers:
        - name: html-demo
          image: prakashraj007/html-demo:latest
          ports:
            - containerPort: 80

---
apiVersion: v1
kind: Service
metadata:
  name: html-demo-service

spec:
  type: NodePort
  selector:
    app: html-demo

  ports:
    - port: 80
      targetPort: 80
      nodePort: 30010

step 4 : create a index.html
**********
<!DOCTYPE html>
<html>
<head>
<title>CI/CD Demo</title>
<style>
body{
text-align:center;
font-family:Times New Roman;
background-color:#af0d0d;
}
h1{
color:#0ef777;
}
</style>
</head>
<body>
<h1>CI/CD Pipeline Working</h1>
<h2>Deployed using Jenkins + Docker + Kubernetes</h2>
<p>This webpage is automatically deployed using a CI/CD pipeline.</p>
</body>
</html>
***********


step 5: add pipeline and save run in jenkins

step 6:  reun command "which is uploaded in image"

