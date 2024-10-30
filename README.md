# Halloween_website

## Prerequisites:
- Minikube
- Docker
- Kubectl

### **Workshop Outline**

1. **Setup and Introduction to Minikube**
2. **Deploying a Halloween Website on Kubernetes**
3. **Exposing the Website as a Service**
4. **Accessing and Customising the Halloween Website**

---

### **1. Setup and Introduction to Minikube**

**Goal**: Start Minikube and confirm Kubernetes is running locally.

- **Start Minikube**
    
    Ensure Minikube is running with:
    
    ```bash
    minikube start --driver=docker
    
    ```
    
- **Verify Minikube Cluster**
    
    Confirm that Minikube started successfully:
    
    ```bash
    kubectl get nodes
    
    ```
    

---

### **2. Deploying a Halloween Website on Kubernetes**

**Goal**: Deploy a simple Halloween-themed static website using an NGINX web server.

- **Prepare the Halloween Website Content**
    
    You can use basic HTML, CSS, and JavaScript. Here’s a simple directory structure:
    
    ```
    halloween-website/
    ├── index.html
    ├── styles.css
    └── images/ (contains Halloween-themed images)
    
    ```
    
- **Create a Docker Image for the Halloween Site**
    
    If you’re working with local HTML files, you can create a Dockerfile to package them with an NGINX server.
    
    In your `halloween-website` directory, add the following `Dockerfile`:
    
    ```
    FROM nginx:alpine
    COPY . /usr/share/nginx/html
    
    ```
    
    Then, build the image:
    
    ```bash
    eval $(minikube docker-env)
    docker build -t halloween-website .
    
    ```
    
- **Deploy the Halloween Web Server on Minikube**
    
    Use the built Docker image to create a Kubernetes deployment.
    
    ```bash
    kubectl create deployment halloween-website --image=halloween-website
    
    ```
    
    Confirm the deployment:
    
    ```bash
    kubectl get pods
    
    ```
    

---

### **3. Exposing the Halloween Website as a Service**

**Goal**: Make the website accessible via Minikube by exposing it as a service.

- **Expose the Deployment**
    
    Create a service to expose the Halloween website:
    
    ```bash
    kubectl expose deployment halloween-website --type=NodePort --port=80
    
    ```
    
- **Access the Service**
    
    Use Minikube to open the Halloween website:
    
    ```bash
    minikube service halloween-website
    
    ```
    

---

### **4. Accessing and Customising the Halloween Website**

**Goal**: Customize and test the Halloween website on the local Kubernetes setup.

- **Check the Halloween Site**
    
    Make sure everything displays correctly (images, styles, etc.).
    
- **Optional Enhancements**
    - **Add a spooky audio**: Upload an audio file to the images folder and play it with JavaScript.
    - **Create a darker theme**: Add CSS animations like glowing text or a darker background.
- **Teardown**
    
    To clean up, delete the deployment and stop Minikube:
    
    ```bash
    kubectl delete deployment halloween-website
    minikube stop
    
    ```
