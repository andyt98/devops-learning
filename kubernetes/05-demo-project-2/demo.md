Demo project

![image](https://user-images.githubusercontent.com/90194383/136146870-56ad70ec-9d31-45bf-9734-787789f9279c.png)
![image](https://user-images.githubusercontent.com/90194383/136146883-74129177-eba1-410a-9df8-1c846bcf0d44.png)

On https://hub.docker.com/_/mongo

![image](https://user-images.githubusercontent.com/90194383/136146917-c9f01820-155f-48bf-b649-7caa1077def9.png)
![image](https://user-images.githubusercontent.com/90194383/136146900-d6e3ecee-9324-49dd-b93a-29bd3ffacce1.png)

Deployment Config File is checked into repository. Username and Password should not go there!
Secret lives in K8s, not in the repository!
 
![image](https://user-images.githubusercontent.com/90194383/136146965-79889928-8f64-43a3-b389-76449f3b68ab.png)
![image](https://user-images.githubusercontent.com/90194383/136146974-e225a524-0e17-424c-b307-2246e4a81dde.png)
![image](https://user-images.githubusercontent.com/90194383/136146987-1299642d-19fa-47c8-a1c4-f3453391b96d.png)
![image](https://user-images.githubusercontent.com/90194383/136146998-9ba6f622-d342-43ce-87f7-7de357dd0b7e.png)

Run these commands in order:<br>
kubectl apply -f mongo-secret.yaml<br>
kubectl apply -f mongo.yaml<br>
Next step, we need to create an internal service, so other components or other pods can talk to this MongoDB<br>

![image](https://user-images.githubusercontent.com/90194383/136147031-b7ec0220-bb7d-4f73-8b8c-ea84cef57bdd.png)

We are gonna create the service in the same mongo.YAML file

![image](https://user-images.githubusercontent.com/90194383/136147098-4c3b6aae-a99a-4e49-8efc-48ebb07a93b5.png)
![image](https://user-images.githubusercontent.com/90194383/136147105-2a3ceb95-1335-424a-aad1-6dc0455a0028.png)

port and targetPort can be different

![image](https://user-images.githubusercontent.com/90194383/136147123-423ab6d8-11ed-49e9-9187-659bdad08531.png)
 
Next, we are gonna create Mongo Express Deployment and Service and also an external configuration (ConfigMap) where we are gonna put the database url for MongoDB 

![image](https://user-images.githubusercontent.com/90194383/136147136-df2affae-e892-4b89-8854-e9243f12a8e8.png)
 
On https://hub.docker.com/_/mongo-express
We see the port is 8081

![image](https://user-images.githubusercontent.com/90194383/136147152-6ad18ea8-70c6-4cff-a11a-c056c18deb3d.png)
![image](https://user-images.githubusercontent.com/90194383/136147175-99e4edb3-8b2f-411b-ac9b-bd798e55b1c6.png) <br>
![image](https://user-images.githubusercontent.com/90194383/136147185-e135470e-c826-4588-9137-421e82fbede7.png)
![image](https://user-images.githubusercontent.com/90194383/136147192-629f275e-d363-49f8-9f0a-2188286c2fe3.png)

Server name is actually the name of the service: mongodb-service<br>
Run these commands in order:<br>
kubectl apply -f mongo-configmap.yaml<br>
kubectl apply -f mongo-express.yaml<br>
To see if the server is running: kubectl logs mongo-express-xxxxxx<br>
So now, the final step is to access mongo-express from the browser, so we need Mongo Express External Service<br>

![image](https://user-images.githubusercontent.com/90194383/136147285-13907ffc-7929-477b-97a6-e07358c20076.png)
![image](https://user-images.githubusercontent.com/90194383/136147296-863f3d90-3dd7-4739-b90b-3977235742d0.png)
![image](https://user-images.githubusercontent.com/90194383/136147305-c880fa2e-b522-47e8-960a-bfec14cb5057.png)
![image](https://user-images.githubusercontent.com/90194383/136147319-d5d5ce91-e0e9-4b67-90b7-f7d3914c4bf2.png)

Internal Service or ClusterIP is DEFAULT 
ClusterIP will give the service an internal IP address, LoadBalancer assigns in addition an External-IP

![image](https://user-images.githubusercontent.com/90194383/136147351-e53fce81-e81c-4f6b-bee0-a9a51c0b28f7.png)

 This command assigns a public IP address to the external service
 
![image](https://user-images.githubusercontent.com/90194383/136147365-0138c9fc-1f30-4d45-a520-eaf6264dd3fd.png)

