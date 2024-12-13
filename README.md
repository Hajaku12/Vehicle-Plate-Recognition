# Vehicle Plate Recognition with AWS Rekognition

## Introduction

This application is designed to recognize vehicle license plates using AWS Rekognition, a powerful image analysis service provided by Amazon Web Services. The system is built with a Spring Boot backend and utilizes various AWS services to achieve its functionality. The backend processes images uploaded to an S3 bucket, analyzes them using AWS Rekognition, and extracts the license plate information. The application is deployed on AWS EC2 instances, ensuring scalability and reliability. This solution is ideal for applications such as automated toll collection, parking management, and security monitoring.

## Key Components

### Backend (Spring Boot)

The backend of this project is built using Spring Boot, a framework that simplifies the development of Java applications. The key components of the backend include:

1. **Spring Boot Application**: The main entry point of the application, which initializes and runs the Spring Boot application.

2. **Controllers**: These handle HTTP requests and map them to the appropriate service methods. They are responsible for processing incoming requests, invoking the necessary business logic, and returning the appropriate responses.

3. **Services**: These contain the business logic of the application. They interact with the repositories to perform CRUD operations and other business-related tasks.

4. **Repositories**: These are responsible for data access. They interact with the database to perform CRUD operations on the data.

5. **Entities**: These represent the data model of the application. They are mapped to the database tables and are used to transfer data between different layers of the application.

6. **Configuration Files**: These include application properties and other configuration files required to set up and run the Spring Boot application.

### Frontend (REACT)

**Link to the Frontend Repository**: [Frontend Repository]()

The frontend of this project is built using React, a popular JavaScript library for building user interfaces. The key components of the frontend include:

1. **Components**: These are reusable UI elements that make up the user interface of the application. They are composed together to create the overall user experience.
2. **Pages**: These represent the different pages of the application. They contain the layout and structure of the page and are composed of components.
3. **Services**: These handle the communication with the backend API. They send requests to the backend, process the responses, and update the UI accordingly.
4. **Routing**: This is implemented using React Router to manage the navigation between different pages of the application.

### Video

![Video.gif](images%2FVideo.gif)

### Prerequisites

You need to install the following tools and configure their dependencies:

1. **Java** (version 8 or above)

    ```bash
    java -version
    ```

   Should return something like:

    ```bash
    java version "1.8.0"
    Java(TM) SE Runtime Environment (build 1.8.0-b132)
    Java HotSpot(TM) 64-Bit Server VM (build 25.0-b70, mixed mode)
    ```

2. **Maven**
   - Download Maven from [here](http://maven.apache.org/download.cgi)
   - Follow the installation instructions [here](https://maven.apache.org/install.html)

   Verify the installation:

    ```bash
    mvn -version
    ```

   Should return something like:

    ```bash
    Apache Maven 3.6.3
    ```

## Installing

1. Clone the repository and navigate into the project directory:

    ```bash
    git clone 
    cd 
    ```

2. Build the project:

    ```bash
    mvn clean package
    ```

   Should display output similar to:

    ```bash
    [INFO] BUILD SUCCESS
    ```

## Deployment in AWS

To run the program on AWS, we need to have two instances, in my case, they are the following:

1. **EC2 Instances**:
   - One instance for the frontend.
   - One instance for the backend.

2. **S3 Bucket**:
   - Used to store the images.

3. **AWS Rekognition**:
   - Used to analyze the images and extract the license plate information.

### Steps to Deploy

1. **Set up EC2 Instances**:
   - Launch two EC2 instances (one for frontend and one for backend).
   - Configure security groups to allow necessary traffic (e.g., HTTP, SSH).

2. **Deploy Backend**:
   - SSH into the backend EC2 instance.
   - Install Java and Maven.
   - Clone the repository and build the project.
   - Run the Spring Boot application.

3. **Deploy Frontend**:
   - SSH into the frontend EC2 instance.
   - Set up the frontend application.

4. **Set up S3 Bucket**:
   - Create an S3 bucket to store the images.
   - Configure the bucket policies and permissions to allow access from the backend.

5. **Integrate AWS Rekognition**:
   - Use AWS SDK in the backend application to interact with AWS Rekognition.
   - Implement the logic to upload images to S3 and analyze them using Rekognition.

## Architecture Diagram

![Diagram.jpg](images%2FDiagram.jpg)

The architecture diagram for the Vehicle Plate Recognition application with AWS Rekognition illustrates the interaction between various components and services. Here is a detailed explanation of each part:

1. **Frontend**:
   - Hosted on an EC2 instance.
   - Responsible for the user interface and user interactions.
   - Sends image upload requests to the backend.

2. **Backend (Spring Boot)**:
   - Hosted on a separate EC2 instance.
   - Processes incoming HTTP requests from the frontend.
   - Contains controllers, services, repositories, and other components to handle business logic and data access.
   - Interacts with AWS services such as S3 and Rekognition.

3. **S3 Bucket**:
   - Used to store uploaded images.
   - The backend uploads images to this bucket for further processing.

4. **AWS Rekognition**:
   - Analyzes images stored in the S3 bucket.
   - Extracts license plate information from the images.
   - The backend retrieves the analysis results and processes them accordingly.

5. **Database**:
   - Stores application data such as user information, image metadata, and recognized license plate details.
   - The backend interacts with the database to perform CRUD operations.

### Data Flow

1. The user uploads an image through the frontend.
2. The frontend sends the image to the backend.
3. The backend uploads the image to the S3 bucket.
4. The backend requests AWS Rekognition to analyze the image.
5. AWS Rekognition processes the image and returns the license plate information.
6. The backend processes the results and stores relevant data in the database.
7. The backend sends the analysis results back to the frontend.
8. The frontend displays the results to the user.

This architecture ensures a scalable and reliable system by leveraging AWS services and separating concerns between the frontend and backend.
## Generating Project Documentation

1. **Generate the Site**
   - Run the following command to generate the site documentation:
     ```sh
     mvn site
     ```

2. **Add Javadoc Plugin for Documentation**
   - Add the Javadoc plugin to the `reporting` section of the `pom.xml`:
     ```xml
     <project>
       ...
       <reporting>
         <plugins>
           <plugin>
             <groupId>org.apache.maven.plugins</groupId>
             <artifactId>maven-javadoc-plugin</artifactId>
             <version>2.10.1</version>
             <configuration>
               ...
             </configuration>
           </plugin>
         </plugins>
       </reporting>
       ...
     </project>
     ```

   - To generate Javadoc as an independent element, add the plugin in the `build` section of the `pom.xml`:
     ```xml
     <project>
       ...
       <build>
         <plugins>
           <plugin>
             <groupId>org.apache.maven.plugins</groupId>
             <artifactId>maven-javadoc-plugin</artifactId>
             <version>2.10.1</version>
             <configuration>
               ...
             </configuration>
           </plugin>
         </plugins>
       </build>
       ...
     </project>
     ```

3. **Generate Javadoc Commands**
   - Use the following commands to generate Javadocs:
     ```sh
     mvn javadoc:javadoc
     mvn javadoc:jar
     mvn javadoc:aggregate
     mvn javadoc:aggregate-jar
     mvn javadoc:test-javadoc
     mvn javadoc:test-jar
     mvn javadoc:test-aggregate
     mvn javadoc:test-aggregate-jar
     ```

## License
This project is licensed under the MIT License - see the `LICENSE.txt` file for details.

## Versioned

We use [Git](https://github.com/) for version control. For available versions, see the tags in this repository.

## Author

**Hann Jang, Jose Samuel Mahecha Alarcon, Juan David Garcia Pulido** 

