# Secret-Manager

Types

## 1. Arbitary :
   An arbitrary secret is a type of application secret that can be used to hold structured or unstructured data, such as a key, configuration file, or any other piece of sensitive information. After you create the secret, you can use it to connect your application to a protected resource, such as a third-party app or database. Your secret is stored securely in your dedicated Secrets Manager service instance, where you can centrally manage its lifecycle.

   Rotation Policy : For arbitrary secrets we have to add the Value for rotation and the time for rotation like 30, 60 or 90 days. Auto rotation is now allowed for Arbitary Secrets.

   Inputs Required : 
            
              Secret Name - API_KEY
              Value - *apikey value*
                         
   Response we get when we fetch secret from Secret Manager : 
              
            
            
                "created_by":"IBMid-550003YYB7",
                "creation_date":"2021-06-08T09:52:28Z",
                "crn":"crn:v1:bluemix:public:secrets-manager:us-south:a/:692ce041--431c-94a5-:secret:-6540-fe4c-fca7-",
                "id":"-6540-fe4c-fca7-",
                "labels":[],
                "last_update_date":"2021-06-08T09:52:28Z",
                "name":"IAM_APIKEY",
                "secret_data":
                {
                    "payload":"this is a secret"
                },
                "secret_type":"arbitrary",
                "state":1,
                "state_description":"Active",
                "versions":[
                    {
                        "created_by":"IBMid-",
                        "creation_date":"2021-06-08T09:52:28Z",
                        "id":"-fa19-cda8-7b09-"
                    }
                ]
           
            

## 2. Username_Password : 
User credentials consist of username and password values that you can use to log in to or access an external service or application. Your secret is stored securely in your dedicated Secrets Manager service instance, where you can centrally manage its lifecycle, control the secret's lifespan by setting an expiration date, automatic rotation policies, and more.
      
Rotation Policy : Currently, you can enable automatic rotation only for the user credentials (username_password) secret type. For user credentials we can add or just click on Rotate secret, it will generate a 32-character password

Inputs Required : 
      
                  Secret Name - myappCredentials
                  Username - <username>
                  Password - <password>
  
Response we get when we fetch secret from Secret Manager :
  
            "created_by":"IBMid-550003YYB7",
            "creation_date":"2021-06-08T09:08:53Z",
            "crn":"crn:v1:bluemix:public:secrets-manager:us-south:a/:692ce041-9672-431c-94a5-\:secret:]\-2d82-084e-55c9-",
            "id":"--084e-55c9-9954516487dd",
            "labels":[],
            "last_update_date":"2021-06-08T09:08:53Z",
            "name":"poc-check",
            "secret_data":
            {
                "password":"Jaan@5407",
                "username":"ajreddy548"
            },
            "secret_type":"username_password",
            "state":1,
            "state_description":"Active",
            "versions":[
                {
                    "auto_rotated":false,
                    "created_by":"IBMid-",
                    "creation_date":"2021-06-08T09:08:53Z",
                    "id":"a5b6dece-f90f-f4ac-0c7a-796b1ef691db"
                }
            ]

## 3. IAM_Credentials : 
IAM credentials are dynamic secrets that you can use to access an IBM Cloud resource. A set of IAM credentials consists of a service ID and an API key that is generated each time that the protected resource is read or accessed. You can define a time-to-live (TTL) or a lease duration for your IAM credential at its creation so that you shorten the amount of time that the secret exists.

Rotation Policy : IAM credentials are created dynamically on your behalf so that you don't have to manually rotate them

Inputs Required : Schematics Service Engine generates new API key everytime we try to fetch IAM credential secret
  
Response we get when we fetch secret from Secret Manager :
  
          "access_groups":[
          "AccessGroupId--4fac--9c75-d2527463ac46"
          ],
          "api_key":"-T65L0eVMFFurs7S98zhAp9g5",
          "api_key_id":"ApiKey--e057-4d1d-8e9a-d785663da3f8",
          "created_by":"IBMid-550003YYB7",
          "creation_date":"2021-06-10T06:53:02Z",
          "crn":"crn:v1:bluemix:public:secrets-manager:us-south:a/:692ce041-9672-431c-94a5-:secret:1fc3a725-e697-be3c-82da-\",
          "description":"Testing Purpose",
          "id":"-e697-be3c-82da-",
          "labels":[],
          "last_update_date":"2021-06-15T05:15:27Z",
          "name":"iam-cred",
          "reuse_api_key":true,
          "secret_type":"iam_credentials",
          "service_id":"ServiceId--f3eb-4d44-84ce-",
          "service_id_is_static":false,
          "state":1,
          "state_description":"Active",
          "ttl":259200
          
 Set a lease duration or time-to-live (TTL) for the secret:  By setting a lease duration for your IAM credential, you determine how long its associated API key remains valid. After the IAM credential reaches the end of its lease, it is revoked automatically.

(Optional) Determine whether IAM credentials can be reused for your secret: By default, IAM credentials are generated and deleted each time that a secret is read or accessed. By setting Reuse IAM credentials to On, your secret retains its current service ID and API key values, so that you can reuse the same credentials on each read while the secret remains valid. After the secret reaches the end of its lease, the credentials are revoked automatically.
          
