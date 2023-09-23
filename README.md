![image](https://github.com/Lutando-dev/Belt-Exam-2/assets/6805093/b9bda657-5f69-4610-b525-577f862a5d35)# Belt-Exam-2

Question 1

1.Write a Dockerfile to create a Docker image of the backend application and push it to the Docker registry (DockerHub or ECR).

  ![image](https://github.com/Lutando-dev/Belt-Exam-2/assets/6805093/7ef07f8f-7f58-4a5d-a0d9-7a5442df21ba)

  docker build -t lutand0/sample-web-app-backend -f ./api/Dockerfile .
  docker push lutand0/sample-web-app-backend

  ![image](https://github.com/Lutando-dev/Belt-Exam-2/assets/6805093/3a75640d-c727-44bf-bd21-7c1b663811a4)


2.Write a Dockerfile to create a Docker image of the frontend application. Use a server like “Nginx” as a base image to create this image. Push this image to the Docker registry.

  ![image](https://github.com/Lutando-dev/Belt-Exam-2/assets/6805093/900bcec9-3c5f-410c-b782-370b9c8779ee)

  docker build -t lutand0/sample-web-app-frontend -f ./ui/Dockerfile .
  docker push lutand0/sample-web-app-frontend

  ![image](https://github.com/Lutando-dev/Belt-Exam-2/assets/6805093/edcd8980-d1c2-49f4-9697-d5356aec8c0b)

3. Deploy a database container (using postgres:latest image). 
   Use the below environment variables for this database.
        POSTGRES_USER: postgres
        POSTGRES_PASSWORD: admin123
        POSTGRES_DB: basic3tier
   Make sure to use external volume to store the data.

   docker run --network sample-web-app-network --name basic-3tier-postgres -e POSTGRES_USER=postgres -e POSTGRES_PASSWORD=admin123 -e POSTGRES_DB=basic3tier -v basic-3tier-data:/var/lib/postgresql/data -d postgres:latest

   ![image](https://github.com/Lutando-dev/Belt-Exam-2/assets/6805093/194be804-f954-4073-9a6c-519f12741df0)

4. Deploy pgadmin (dpage/pgadmin4:latest) for connecting to the above Postgres database.

   docker run --network sample-web-app-network --name pgadmin4 -p 8080:80 -e PGADMIN_DEFAULT_EMAIL=user@domain.com -e PGADMIN_DEFAULT_PASSWORD=admin123 -d dpage/pgadmin4:latest

   ![image](https://github.com/Lutando-dev/Belt-Exam-2/assets/6805093/63e454a0-33f8-4ba4-8251-1bd8d49e5e1e)


5. Deploy the frontend application as a docker container running on port 80
   docker run -d --name sample-web-app-frontend --network sample-web-app-network -p 80:80 lutand0/sample-web-app-frontend

   ![image](https://github.com/Lutando-dev/Belt-Exam-2/assets/6805093/19f9d0af-e1ea-479e-abbd-852665209737)

6. Deploy the backend application as a docker container running on port 81
   docker run -d --name sample-web-app-backend --network sample-web-app-network -p 81:81 -e ASPNETCORE_URLS=http://+:81 lutand0/sample-web-app-backend

   ![image](https://github.com/Lutando-dev/Belt-Exam-2/assets/6805093/747f40c2-3119-4fd2-a01a-dfb259bb64c9)

7. Create the required networks and volumes.
   docker network create sample-web-app-network

   ![image](https://github.com/Lutando-dev/Belt-Exam-2/assets/6805093/79c74a83-dd98-444d-9f06-363ccb90aad6)

   docker volume create basic-3tier-data

   ![image](https://github.com/Lutando-dev/Belt-Exam-2/assets/6805093/98793781-2fd9-4be6-9349-b9bf48e2a3d7)

8. Verify that your application is up and running.

   ![image](https://github.com/Lutando-dev/Belt-Exam-2/assets/6805093/3440b1ce-192a-42a5-8c98-dbea50fb2d72)

   ![image](https://github.com/Lutando-dev/Belt-Exam-2/assets/6805093/46c33d8a-8519-45b9-8501-4f9fbbcffa7b)

9. Perform the CRUD operations to verify all three services are communicating with each other.
   Create

    ![image](https://github.com/Lutando-dev/Belt-Exam-2/assets/6805093/04f975c9-ab6d-45e8-aba2-c14808c64c2d)

   Read

    ![image](https://github.com/Lutando-dev/Belt-Exam-2/assets/6805093/586c3145-53ab-4456-9698-c944369cf73b)

   Update

    ![image](https://github.com/Lutando-dev/Belt-Exam-2/assets/6805093/49f6b5c8-0ce7-413f-8e28-fbcc5606a6fc)

   Delete

    ![image](https://github.com/Lutando-dev/Belt-Exam-2/assets/6805093/cc3437be-e230-49f7-be07-146b86bb36e6)



Question 2

     ![image](https://github.com/Lutando-dev/Belt-Exam-2/assets/6805093/943fd234-5b55-48d6-89f7-4c65c6794425)

     ![image](https://github.com/Lutando-dev/Belt-Exam-2/assets/6805093/275526d8-5d16-4e86-8840-99f801363723)

Question 3

1. Create three deployment yaml files, one each for frontend, backend, and database.
   database-deployment
      ![image](https://github.com/Lutando-dev/Belt-Exam-2/assets/6805093/d0942a4e-5926-4f51-ae4b-7728f46bf418)

   backend-deployment
       ![image](https://github.com/Lutando-dev/Belt-Exam-2/assets/6805093/8271ab22-fa9a-481a-9f11-8d7c1e81ab05)

   frontend-deployment
       ![image](https://github.com/Lutando-dev/Belt-Exam-2/assets/6805093/b2cd33ea-1cbd-49c6-8062-cadcb0f0d4a0)


2.  Frontend replicas
       [image](https://github.com/Lutando-dev/Belt-Exam-2/assets/6805093/7298bda0-c392-43ca-86c0-cb643dd9ce69)

     Backend replicas

        ![image](https://github.com/Lutando-dev/Belt-Exam-2/assets/6805093/ddbb0915-ab2f-4e1c-a715-71e110033955)

     Database replicas 
        
         ![image](https://github.com/Lutando-dev/Belt-Exam-2/assets/6805093/15c157f6-1a8e-4148-ad01-a59ac776f844)

3.  Create the required Service to expose “frontend application”

    ![image](https://github.com/Lutando-dev/Belt-Exam-2/assets/6805093/e4829fae-6b9e-43af-9cb5-a65323a6eedf)

4. Create the required Service to expose “backend application”
      
    ![image](https://github.com/Lutando-dev/Belt-Exam-2/assets/6805093/c58c6813-dfe3-4cb6-8564-ab34cbecb439)

5. Create a required Service to connect frontend and backend applications

    ![image](https://github.com/Lutando-dev/Belt-Exam-2/assets/6805093/4957c1fb-40fb-43ec-b0d3-abfe210c04ae)

6. Create a required Service to connect the backend with the database.

   ![image](https://github.com/Lutando-dev/Belt-Exam-2/assets/6805093/10f91819-03fa-4f32-a712-778b34c50314)

7. Create a Nginx-Ingress to expose the frontend application.

    ![image](https://github.com/Lutando-dev/Belt-Exam-2/assets/6805093/b1be97ab-cfaa-44c7-bb11-ab195a0194f2)

8. As it is, I cannot deploy struggling with kubectl configiration








