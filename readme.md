# **Module 7: Docker and Containerization**

## **Module Overview**

Welcome to **Module 7**, focusing on **Docker and Containerization**. In this module, you will explore Docker, a pivotal tool in modern software development that allows developers to package applications and their dependencies into isolated containers. Containerization ensures that applications run consistently across different environments, enhancing portability, scalability, and deployment efficiency. You will be provided with a **QR Code Generator** program to demonstrate Docker usage, including writing a Dockerfile, managing containers, and utilizing features such as environment variables and volume sharing. Additionally, you will leverage Git for version control to track your Dockerization process, ensuring transparency and facilitating collaborative development.

By the end of this module, you will have a solid understanding of Docker and the ability to containerize Python applications effectively.

---

## **Why Docker and Containerization?**

Docker is an essential tool in modern software development, particularly in cloud environments. It allows developers to bundle applications along with their dependencies into standardized units called containers. This approach eliminates the "it works on my machine" problem, ensuring that applications behave consistently across development, staging, and production environments. Containerization enhances deployment efficiency, scalability, and resource utilization, making it a cornerstone of DevOps practices.

---

## **Learning Outcomes**

By the end of this module, you will be able to:

1. **Apply containerization techniques to containerize applications using Docker.**
2. **Containerize and manage Python applications using Docker, including Dockerfile creation, environment variables, and volume management.**
3. **Utilize Git for version control and collaborative development.**
5. **Implement comprehensive logging strategies to monitor and debug applications.**

---

## **Learning Pathway**

### **Recall**

**Title:** Introduction to Docker and Review of QR Code Generator Application  
**Grading Type:** Points  
**Instructions:**  
1. **Review the QR Code Generator Program:** Examine the provided QR Code Generator code to understand its functionality, dependencies, and configuration.
2. **Participate in a Discussion:** Share your initial understanding of Docker and containerization.
   - Have you used Docker before?
   - What challenges do you anticipate when Dockerizing an application?
   - How has Git version control aided your development process so far?

**Purpose:** This activity will help you recall and articulate your prior knowledge, setting the foundation for the Dockerization process required in this module.

---

### **Supplemental Readings**

1. **[Containerization vs. Virtualization](https://www.liquidweb.com/kb/virtualization-vs-containerization/)**  
   *Purpose:* Understand the differences between containers and virtual machines, and learn why containerization is more lightweight and flexible for modern development.

2. **[Docker Getting Started Guide](https://docs.docker.com/get-started/)**  
   *Purpose:* Step-by-step instructions for installing Docker and learning about key concepts like images, containers, and Dockerfiles.

3. **[CMD vs. ENTRYPOINT vs. RUN in Dockerfile](https://codewithyury.com/docker-run-vs-cmd-vs-entrypoint/)**  
   *Purpose:* Learn the differences between these Dockerfile instructions and how they influence container behavior.

4. **[Using Environment Variables in Docker](https://vsupalov.com/docker-arg-env-variable-guide/)**  
   *Purpose:* Understand how to pass configuration details into Docker containers using environment variables.

5. **[Git Cheat Sheet](https://education.github.com/git-cheat-sheet-education.pdf)**  
   *Purpose:* Quick reference for essential Git commands and workflows.

6. **[GitHub Actions Documentation](https://docs.github.com/en/actions)**  
   *Purpose:* Learn how to set up and use GitHub Actions for Continuous Integration.

---

### **Watch**

You are required to watch the instructional videos provided on Canvas for this unit. These videos cover Docker basics, environment variable management, volume sharing, security best practices in Docker, Git version control, and setting up GitHub Actions for CI.

---

## **Step-by-Step Guide: Dockerizing the QR Code Generator Application**

This guide will walk you through Dockerizing the provided **QR Code Generator** program. You will learn how to write a Dockerfile, build and run Docker containers, manage environment variables, and set up Continuous Integration using GitHub Actions.

---

### **Step 1: Install Docker**

1. **Go to Docker.com**  
   Download Docker for your operating system: [Get Started with Docker](https://www.docker.com/get-started/).

2. **Install Docker**  
   Follow the installation instructions for your operating system (Windows, Mac, or Linux).

3. **Verify Installation**  
   After installing Docker, open your terminal and verify the installation by running:
   ```bash
   docker --version
   ```
   You should see the Docker version installed on your machine.

4. **Sign Up for a DockerHub Account**  
   Go to [DockerHub](https://hub.docker.com/) and sign up for a free account. DockerHub is where you will store and share your Docker images.

---

### **Step 2: Dockerizing the QR Code Generator Application**

#### **Step 2.1: Preparing Your Project for Dockerization**

1. **Review the QR Code Generator Application**  
   Examine the provided `main.py` script and ensure you understand its functionality, dependencies, and configuration via environment variables.

2. **Ensure Dependencies are Listed**  
   Make sure your project has a `requirements.txt` file that lists all the dependencies required by the QR Code Generator. If not, generate it using:
   ```bash
   pip freeze > requirements.txt
   ```

3. **Set Up Git for Version Control**  
   Initialize a Git repository if you haven't already:
   ```bash
   git init
   ```
   Add all your files and make your initial commit:
   ```bash
   git add .
   git commit -m "Initial commit of QR Code Generator application"
   ```
   Push your repository to GitHub:
   ```bash
   git remote add origin https://github.com/your-username/qr-code-generator.git
   git push -u origin main
   ```

#### **Step 2.2: Writing the Dockerfile for Your QR Code Generator**

1. **Create the Dockerfile in the Root of Your Project**  
   Create a new file named `Dockerfile` in the root directory of your QR Code Generator project.

2. **Structure Your Dockerfile**  
   Below is the Dockerfile tailored to your **QR Code Generator** application:

   ```Dockerfile
   # Use the official Python image from DockerHub as the base image
   FROM python:3.12-slim-bullseye

   # Set the working directory inside the container
   WORKDIR /app

   # Copy the requirements.txt file and install dependencies
   COPY requirements.txt ./
   RUN pip install --no-cache-dir -r requirements.txt

   # Create directories for logs and QR codes, and set ownership to the non-root user
   RUN useradd -m myuser && mkdir logs qr_codes && chown myuser:myuser logs qr_codes

   # Copy the rest of the application’s source code into the container, setting ownership to 'myuser'
   COPY --chown=myuser:myuser . .

   # Switch to the non-root user for security
   USER myuser

   # Use ENTRYPOINT and CMD to allow flexibility when running the container
   ENTRYPOINT ["python", "main.py"]
   CMD ["--url", "http://github.com/kaw393939"]
   ```

   **Security Considerations in the Dockerfile:**
   - **Non-Root User:** The Dockerfile creates a non-root user (`myuser`) to run the application, enhancing security by minimizing potential damage from vulnerabilities.
   - **Ownership of Directories:** Directories for logs and QR codes are created and owned by `myuser`, ensuring that only the non-root user can write to these directories.
   - **Minimal Base Image:** Using a slim variant of Python reduces the attack surface by minimizing the number of installed packages.

   **Explanation of Dockerfile Commands:**
   - **FROM:** Specifies the base image (`python:3.12-slim-bullseye`), which is lightweight and secure.
   - **WORKDIR:** Sets the working directory inside the container to `/app`.
   - **COPY:** Copies `requirements.txt` first to leverage Docker’s caching mechanism for dependencies.
   - **RUN:** Installs Python dependencies, creates a non-root user, and sets up necessary directories with appropriate permissions.
   - **USER:** Switches to the non-root user (`myuser`) to run the application.
   - **ENTRYPOINT and CMD:** Defines the default command to run when the container starts, allowing for command-line argument overrides.

#### **Step 2.3: Building and Running the Dockerized QR Code Generator**

1. **Build the Docker Image**  
   In the directory where your Dockerfile is located, run the following command to build your Docker image:
   ```bash
   docker build -t qr-code-generator-app .
   ```
   This command builds an image named `qr-code-generator-app` using the current directory (`.`) as the build context.

2. **Run the Container**  
   Once the image is built, you can run the container in detached mode:
   ```bash
   docker run -d --name qr-generator qr-code-generator-app
   ```
   This command runs the container named `qr-generator` based on the `qr-code-generator-app` image.

3. **Passing Custom Input**  
   If your QR Code Generator application accepts custom input (such as a different URL or configuration), you can pass these to the container using environment variables or by overriding the `CMD`. For example:
   ```bash
   docker run -d --name qr-generator \
   -v /host/path/to/qr_codes:/app/qr_codes \
   qr-code-generator-app --url http://www.njit.edu
   ```
   - **-v /host/path/to/qr_codes:/app/qr_codes:** Maps the local `qr_codes` directory to `/app/qr_codes` in the container.
   - **--url http://www.njit.edu:** Overrides the default URL argument with a custom URL.

4. **View Logs**  
   Check the container logs to ensure your QR Code Generator application is running correctly:
   ```bash
   docker logs qr-generator
   ```

5. **Stop and Remove the Container**  
   After testing, you can stop and remove the container:
   ```bash
   docker stop qr-generator
   docker rm qr-generator
   ```

---

### **Step 3: Pushing Your Docker Image to DockerHub**

Once you have successfully Dockerized your **QR Code Generator** application, you can push the Docker image to **DockerHub** to share it with others or use it in cloud environments.

1. **Login to DockerHub**  
   Run the following command to log in to your DockerHub account:
   ```bash
   docker login
   ```
   Enter your DockerHub username and password when prompted.

2. **Tag Your Image**  
   Tag your Docker image with your DockerHub username and image name:
   ```bash
   docker tag qr-code-generator-app your-dockerhub-username/qr-code-generator-app
   ```

3. **Push the Image to DockerHub**  
   Push the tagged image to DockerHub:
   ```bash
   docker push your-dockerhub-username/qr-code-generator-app
   ```
   Your image is now available on DockerHub for others to pull and use.

---

### **Step 4: Setting Up Continuous Integration with GitHub Actions**

Integrating Continuous Integration (CI) ensures that your application is automatically tested and built whenever you push changes to your repository. GitHub Actions allows you to automate this process seamlessly.

1. **Create a GitHub Actions Workflow File**  
   In your project repository, create a new directory named `.github/workflows/` and inside it, create a file named `python-app.yml`.

   **Explanation of Workflow Steps:**
   - **actions/checkout@v2:** Checks out your repository code.
   - **actions/setup-python@v2:** Sets up the specified Python version.
   - **Install dependencies:** Installs Python dependencies and testing tools.
   - **Run tests with coverage:** Executes unit tests and measures coverage, generating a coverage report.
   - **Build Docker image:** Builds the Docker image for your application.
   - **docker/login-action@v2:** Logs in to DockerHub using secrets stored in GitHub.
   - **Push Docker image:** Pushes the Docker image to DockerHub.
   - **Check coverage:** Ensures that test coverage meets the required threshold (100%).

3. **Set Up DockerHub Credentials in GitHub Secrets**  
   To securely pass your DockerHub credentials to GitHub Actions:
   - Go to your GitHub repository.
   - Click on **Settings** > **Secrets and variables** > **Actions** > **New repository secret**.
   - Add the following secrets:
     - **DOCKER_USERNAME:** Your DockerHub username.
     - **DOCKER_PASSWORD:** Your DockerHub password or access token.

4. **Commit and Push the Workflow File**  
   Add, commit, and push the workflow file to your repository:
   ```bash
   git add .github/workflows/python-app.yml
   git commit -m "Add GitHub Actions workflow for CI and Docker build"
   git push origin main

## **Submit**

**Activity Title:** Dockerize the QR Code Generator Program  
**Grading Type:** Points  

**Submission Instructions:**  
1. **Dockerize the QR Code Generator Program:** Follow the steps outlined in this module to Dockerize the provided **QR Code Generator** application.
2. **Push Docker Image to DockerHub:** Ensure your Docker image is pushed to DockerHub. Submit the link to your DockerHub image (e.g., `https://hub.docker.com/r/your-dockerhub-username/qr-code-generator-app`).
3. **Provide GitHub Repository Link:** Submit the link to your GitHub repository containing the Dockerfile, application code, and GitHub Actions workflow.
4. **Include Screenshots:**
   - **Container Logs:** Provide a screenshot showing the container logs that confirm your application is running successfully inside the container.
   - **GitHub Actions Workflow:** Include a screenshot of a successful GitHub Actions run, demonstrating automated testing and Docker image building.

**Example Submission Structure:**
- **GitHub Repository:** [https://github.com/your-username/qr-code-generator](https://github.com/your-username/qr-code-generator)
- **DockerHub Image:** [https://hub.docker.com/r/your-dockerhub-username/qr-code-generator-app](https://hub.docker.com/r/your-dockerhub-username/qr-code-generator-app)
- **Screenshots:**
  - *Container Logs:* [Upload Image]
  - *GitHub Actions Workflow:* [Upload Image]

---

## **Reflect**

**Title:** Module 7 In-Depth Reflection  
**Grading Type:** Points  
**Instructions:**  
Compose a comprehensive reflection (600-700 words) on your experience Dockerizing the **QR Code Generator** application. Your reflection should address the following points:

1. **Application of Concepts:**  
   Analyze how containerization with Docker enhances the portability and scalability of Python applications. Discuss how writing a Dockerfile, managing environment variables, and volume management contribute to a robust deployment process.

2. **Challenges and Solutions:**  
   - Identify any challenges you faced while Dockerizing your application, such as handling dependencies, configuring environment variables, or setting up volume mounts.
   - Explain the strategies and solutions you employed to overcome these challenges.

3. **Utilizing Git for Version Control:**  
   - Discuss how Git facilitated the Dockerization process.
   - Reflect on the importance of committing changes regularly with descriptive messages.
   - Explain how branching and merging can aid in managing different features or stages of development.

4. **Continuous Integration with GitHub Actions:**  
   - Reflect on setting up GitHub Actions for automating tests and Docker builds.
   - Discuss how CI/CD pipelines contribute to maintaining software quality and reliability.
   - Consider the benefits of automating these processes in a collaborative development environment.

5. **Future Applications:**  
   - Explore how containerization can be applied to larger-scale projects or in cloud environments.
   - Consider the potential integration of Docker with other DevOps tools and practices.

6. **Self-Evaluation:**  
   - Evaluate your current level of confidence in using Docker, writing Dockerfiles, managing containers, and setting up CI/CD pipelines with GitHub Actions.
   - Identify areas where you feel proficient and areas where you need further practice or support.

**Purpose:** This activity aims to encourage deep metacognition and help you connect new knowledge with prior experiences and future applications.

---

## **Reflect**

**Title:** Module 7 In-Depth Reflection  
**Grading Type:** Points  
**Instructions:**  
Compose a comprehensive reflection (600-700 words) on your experience Dockerizing the **QR Code Generator** application. Your reflection should address the following points:

1. **Application of Concepts:**  
   Analyze how containerization with Docker enhances the portability and scalability of Python applications. Discuss how writing a Dockerfile, managing environment variables, and volume management contribute to a robust deployment process.

2. **Challenges and Solutions:**  
   - Identify any challenges you faced while Dockerizing your application, such as handling dependencies, configuring environment variables, or setting up volume mounts.
   - Explain the strategies and solutions you employed to overcome these challenges.

3. **Utilizing Git for Version Control:**  
   - Discuss how Git facilitated the Dockerization process.
   - Reflect on the importance of committing changes regularly with descriptive messages.
   - Explain how branching and merging can aid in managing different features or stages of development.

4. **Continuous Integration with GitHub Actions:**  
   - Reflect on setting up GitHub Actions for automating tests and Docker builds.
   - Discuss how CI/CD pipelines contribute to maintaining software quality and reliability.
   - Consider the benefits of automating these processes in a collaborative development environment.

5. **Future Applications:**  
   - Explore how containerization can be applied to larger-scale projects or in cloud environments.
   - Consider the potential integration of Docker with other DevOps tools and practices.

6. **Self-Evaluation:**  
   - Evaluate your current level of confidence in using Docker, writing Dockerfiles, managing containers, and setting up CI/CD pipelines with GitHub Actions.
   - Identify areas where you feel proficient and areas where you need further practice or support.

**Purpose:** This activity aims to encourage deep metacognition and help you connect new knowledge with prior experiences and future applications.

---

## **Quiz**

**Title:** Docker and Containerization Quiz  
**Grading Type:** Points  

**Instructions:**
1. **Complete the Quiz:** Access the quiz on Canvas, which tests your understanding of Docker and containerization concepts.
2. **Quiz Content:** The quiz will cover:
   - Dockerfile commands and their purposes.
   - Differences between CMD, ENTRYPOINT, and RUN.
   - Managing environment variables and volumes in Docker.
   - The benefits of containerization over virtualization.
   - Basics of Docker networking and security practices.
   - Understanding Git and GitHub Actions workflows.

**Question Types:**
- **Multiple-Choice:** Assess your knowledge of key Docker concepts and commands.
- **Short Answer:** Explain the purpose of specific Dockerfile instructions.
- **Code Analysis:** Review snippets of Dockerfiles and identify any issues or improvements.

**Purpose:** This quiz will assess your comprehension and application of Docker and containerization principles, ensuring you are prepared to effectively use Docker in your projects.

--
---

## **Tips for Success**

- **Manage Your Time:** Allocate sufficient time to plan, implement, test, and document your Dockerization process.
- **Seek Help When Needed:** If you encounter challenges, refer to the supplementary articles or reach out to your instructors for guidance.

---

## **Submission Deadline**

Please ensure that your GitHub repository link, DockerHub image link, and completion of the midterm test on Canvas are submitted by **[Insert Deadline Here]**. Late submissions may be subject to grade penalties as per the course policy.

---

**Good luck with your midterm assessment!** Demonstrate your understanding and proficiency by thoughtfully Dockerizing the QR Code Generator application, showcasing the skills you've developed throughout the course.
