

****
COnfigure account and create budget alarms

got to accounts-->
IAM user and role access to Billing information 
Activate IAM access

Go to Billing preferences

enable all notification options

go to budget
create abudget
create amontly budget for 5 dollars

***
Setup indivisyal user account
create iam user
create a user group and assign full permissions to it.
assign this user group to the iam user
and use this iam user.

login to iam user gen acceks for awscli

downlod awscli for windows
configure awscli on windows  with this acces keys

aws s3 ls
aws s3 mb s3://testoranitnewbucket03042024
(create a new bucket)

also u can do the same using aws cloudshell


*******
Aws Org
heirrchy
u have the management account (which is the root accoutn)
we can create additonal accounts or join exist accounts under the management account
eg:- prod and dev account
and deploy resources in those accounts respectively.
We can have a heirrchy

![Org](https://github.com/testoranit/AWSSolution-Arch/assets/124513439/b3a66424-adf0-456c-9d01-624d635f7590)

**************
HOL Create Aws org and add account
GO to AWS Oranization in search bar-->create org
add new account-->create account-->DCT.production-->Enter email-->IAM role=OrganizationAccountAccessRole

ALso go to Policies AWS Organizations
Policies
Service control policies and enable it.

![Accounts](https://github.com/testoranit/AWSSolution-Arch/assets/124513439/568fd781-72be-4027-9c30-846b9326f408)


Now got to switch role
and enter details of the new account which prod.
992382672911

Now u can use this account to crate ur prod resources.

*******************************
Service COntrol Policies.
Note:- IAM role for use of the resource.
SCP for the use of service.

U can have OU's under management account and then u can have diiferent account's under that OU's and can have tag and scp policies.

![SCPS](https://github.com/testoranit/AWSSolution-Arch/assets/124513439/ea55e970-9779-407b-a767-b47433170b10)


****************************8
HOL SCP Strategies and Inheritance
Switch back to ur root account
got SCP's and create a policy

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "RequireMicroInstanceType",
      "Effect": "Deny",
      "Action": "ec2:RunInstances",
      "Resource": "arn:aws:ec2:*:*:instance/*",
      "Condition": {
        "StringNotEquals":{               	
          "ec2:InstanceType":"t2.micro"
        }
      }
    }
  ]
}

and now attach this policy to DCT.Prod account
Switc to DCT.Prod and launch an ec2 with t2.micro u will be able to do it.
try launching incntance other then t2.micro it will fail.

*******************************
AWS COntrol TOwer
![control tower](https://github.com/testoranit/AWSSolution-Arch/assets/124513439/03610179-b266-40ff-9f5c-9f360697db2a)



HOL
GOt to CT page-->Landing ZOne
define home region.
define OU structure
Securtiy
Sandbox
enter 2 diff emails.
Edit Account factory public subnet
Check Guardrails for governance over the account.
***************
How IAM works
Priniplues:- Users,role,Federated users(users with FB,amazongoogle account),Application (programatically)

Users could be grouped and policies could be applied to the group.

AWS STS(security token service)
(ec2 wants to access s3, then u create an Iam role but u can also create STS, so that ec2 gets temporary access to 
s3)

RBAC:- policy applied to roup and group has users.
ABAC:- user has tag like dba admin they can get access to RDS and only do start,restart,stop)

********
HOL RBAC
user group attach policy to group.

********
HOL ABAC
Add tags to user like depat=prod, and other user dept=dev
create abac policy like if dba=prod and tag=prod then they can restar prod.
create other policy for dev user.

************
Cross account access to S3.

create s3 and a role in 1 account
now create an trusted policy for this role using IAM with other account details.
now create & attach an inline policy that gets access to the S3 bucket to the other account.
attach this policy  to the role.
and now access the S3 bucket from another account.


***********
Note:- Managed AWS policies cannot be ediited,but u can use it as a reference to create a custom policy.

*******
AWS directory service.
AWS Managed microsoft AD.
![AD COnnector](https://github.com/testoranit/AWSSolution-Arch/assets/124513439/da5364cf-9fb8-4b00-82a5-3f494abdc3e1)


Dederation
eg:- u have AD on ur corporate and u want to connect to ur AWS services, so u use 1 uderidentity 

![IAM SAML 2 0 Federation service](https://github.com/testoranit/AWSSolution-Arch/assets/124513439/2404f860-2963-4b34-9bcc-dee0f8afa0e2)

![IAM Web Federation](https://github.com/testoranit/AWSSolution-Arch/assets/124513439/a579c186-7849-44a3-a21f-ddc3e48ade4a)

![IAM Identity centre](https://github.com/testoranit/AWSSolution-Arch/assets/124513439/3f124a85-83b2-4883-89e2-42bcc6c5f629)

![AMAzon COgnito](https://github.com/testoranit/AWSSolution-Arch/assets/124513439/17be6721-a809-4e1a-b28b-9beaa0f405e3)

*********
AWS pushes to use Identity centre when u create new users but there ma be org where they would be using IAM without Identity centre and it would be tedious for them to migrate it to Identity center, but for new org u can use ID Centre.

HOL Search
:- Identity Centre
choose ur id store.
*********************************
AWS GLobal Infra.

![AWS Global Infra](https://github.com/testoranit/AWSSolution-Arch/assets/124513439/2a9e913a-535b-4dea-9f2c-98c8bc8d1223)

You can use AWS outposts to use some service of AWS on ur on-prem
AWS Wavelenght zone(low latency over 5g)
AWS Local ZOne(low latency)

*****
AWS CLoudfront
Cache content to edge locations.
![AWS CLoudfront](https://github.com/testoranit/AWSSolution-Arch/assets/124513439/52b5c5b7-ccab-4efe-9345-13a48bb51166)

*********************
AWS VPC CIDR Blocks

Network:- 192.168.0.0
/24 subnet mask:- 255.255.255.0
So 8 host bits= 256 addresses.
Here 192.168.0.1 will be first address and 0.0 can't be used since it's the newtwok address and 255.255 could not be used since it's the broadcast address.


/16 subnet mask:- 255.255.0.0
So 16 host bits=65536 addresses.

/20 Subnet mask (Varibale lenght subnet mask):- 255.255.(4/4).0
So 12 hosts bits=4096 addresses.

![Define CIDR Blocks](https://github.com/testoranit/AWSSolution-Arch/assets/124513439/05904d72-7b22-46f7-a311-44f8c4acebd2)

Rules and Guidliness.

CIDR Block size should be between /16 and /28
Should not overlap with another CIDR block.
u can't re-size it later.
first 4 and last ip addresses can't be used.

go to network00.com
![network00 0](https://github.com/testoranit/AWSSolution-Arch/assets/124513439/89917c68-cf68-4250-b268-289649017c3c)


**********************
SG is at instance level, is an stateful way of defining traffic(u define the incoming traffic and outgoing traffic)
it allows traffic and has a default deny rule.

NACL is at subnet level , and is an steless way of defining traffic,
(u can define the allow and deny rules with priorities.)

***********************************
VPC ENdpoints.

u wan't to connect to other AWS service like  without going through Public internet, u use endpoints.
VPC interface Enfpoint:-
UC:- what if ec2 in priv subnet wants to connect to other AWS service.. and u don't have pip since it'sin priv sub and don't wan't to use NAT Gatweay for the traffic from this ec2 to the Internet so u ucanuse endpoint eni in priv subnet,which can then communicate to othr aws services,it uses prip to connect to other aws service.


And VPC Gateway endpoint:-
priov ec2 wan't to connect wit S3
same u don't have pip since it's in priv subnet and don't want to go through internet.
so u use s3 gateway endpoint.
in this case u create a route table entry.

*************Hybrid connectivity.
1)AWS CLIENT VPN.
![AWS Lient VPN](https://github.com/testoranit/AWSSolution-Arch/assets/124513439/e298f954-843d-4f5d-90d3-a5e638dd66a9)

2)AWS SITE to SITE VPN.
![AWS SITE-to-SITE VPN](https://github.com/testoranit/AWSSolution-Arch/assets/124513439/135be652-cfe3-4403-972d-dc08b6c5155c)


3)AWS VPNCLOUDHUb
![AWSVPNCLoudhub](https://github.com/testoranit/AWSSolution-Arch/assets/124513439/c1bd2638-36ce-44ce-a694-dfce5d158b47)

4)AWS DIrect COnnect
similar like AZure expressroute(private connection from onprem to AWS)

5)AWS Tansit Gateway.
  
![AWS Transit Gateway](https://github.com/testoranit/AWSSolution-Arch/assets/124513439/4483758c-22cd-4c69-a9d7-f0f6ad4eb50c)

*******************
AWS EBS

EBS attah to 1 instance
U can do Multi attach meaning 1 EBS to many EC2 but it should be in the same availibilty zone.
it has some limitations though.

You can alos cretae a snapshot of an EBS volume and use that snapshot to create the same volume also in other az for other
ec2 if needed.

********AWS S3
u acces object using https:// protocol.
max size of 1 file in S3 is 5TB.
unlimited storage files
s3 bucketname should be unique globally

S3 classes:-
Durability and availibilty in S3
119s of durable 99.9999999 (data is not lost)

Availibilty:- 99.99%

![S3 Storage classes](https://github.com/testoranit/AWSSolution-Arch/assets/124513439/6807281e-86be-4e70-a21e-5f4b40e03605)

***
S3 life cycle policies

![Lifecycle Transitions](https://github.com/testoranit/AWSSolution-Arch/assets/124513439/e229f579-0468-428a-9655-8cb4d22b13c2)

![eg Lifecycle policy](https://github.com/testoranit/AWSSolution-Arch/assets/124513439/80bdbd15-6de0-4df5-acbf-744c9de678c9)

***HOL S3 replication and lifecycle configuration
Creats asource  S3 bucket
us east 1
enable bucket versioning

now create dest bucket with same as above

create an IAM role
Cstom trust policy
and give s3 the asumerole api action in the code.
go to the role once created and create an inline policy

create replication for src bucket
enter details and then uplod files in src bucket, it would be replicated to dest bucket.

u can do same region or cross regrion replication but pre req is to enable versioning.


create a lifecycle rule for src bucket if required.

Versioning

Upload some files.
and again upload same file to the same buckrt, u see the versions of different bucket.

*************
ENcryption:-
Server side encryption and client side encryption.
while uploading objects to S3 u need to provide an encryption key to it.

***********************************888
Server Access loging:- this is for enabling logging for the bucket.

***************
S3 Event Notfications
Got to SNS and create a topic.
Create a subscription for this topic.
go to ur email and confirm subscription.
Now go to topic and configure access policy for the topic.
so that bucket can access the topic.
Now go to bucket and create event notfications.

*************AWS Storage Gateway
On-prem storage to AWS Storage usinw AWS Direct COnnect
1)FIle gateway
2)Volue Gateway.
**************AWS Route 53
Pulic hosted Zone:- user access an application via browser, when it firsts asks route 53 to resolve the ip and access the web page.

Private hosted zone:-
![Private AMzonon Route 53 hosted zone](https://github.com/testoranit/AWSSolution-Arch/assets/124513439/3d2e9d88-0a32-4f1d-ac10-543f0183d83f)

ur ec2 asks for the dns resolution  with Route 53 for ur db in private subnet is an example of Private Hosted Zone.



MIgratio of Route 53:-
You can always migrate records from another hosted zone or other account or other provider to AWS Route 53, and viceversa.

![ROuting policis](https://github.com/testoranit/AWSSolution-Arch/assets/124513439/a329abb3-4a3a-4c25-9b1f-1f8a457112dc)


Geolocation: Focuses on the user's location.
Geoproximity: Considers both the user's location and the resource's location, along with optional biases.
Also have weighted routed policies.
u can use this for a blue green scenaro.

FAilover routing policy:- Prim and Secondary(for DR scenario)
US-east-1
Create ASG with 1 instance and create target group for this instance,attach it to an lB.
Eu-west-1
Create ASG with 1 instance and create target group for this instance,attach it to an lB.

Create a hosted zone record

for Prim
![Primary Record for Region Failover](https://github.com/testoranit/AWSSolution-Arch/assets/124513439/8de38ba9-132e-42ac-8448-87d88a256796)

FOr Secon;_
do as above.

And test a failover my doing something down on primary anc check the DNS name link in broweser.

![Prim URL in browser](https://github.com/testoranit/AWSSolution-Arch/assets/124513439/cb3bda4d-2c6b-4c07-847c-2e9f8e5d05b4)

After:-
![Secondary failure](https://github.com/testoranit/AWSSolution-Arch/assets/124513439/f5c30b35-dae6-4548-9248-8f348c748a38)


*******Route 53 Resolver

![Route 53 resolver](https://github.com/testoranit/AWSSolution-Arch/assets/124513439/d2b52483-98f3-4cda-a7e4-0a2f2886289a)

Same goes with Inbound endpoints.

*******************
Amazon CLoudfront Origins and distributins.
![Cloudfromt](https://github.com/testoranit/AWSSolution-Arch/assets/124513439/0df51e94-a077-48f2-a21a-1bd49cf428bc)

![Cloufront distributions and origin](https://github.com/testoranit/AWSSolution-Arch/assets/124513439/9892857c-a000-4c12-9562-57877088e603)

**************
Cloudfront caching and Behaviours.

![Cloudfront caching](https://github.com/testoranit/AWSSolution-Arch/assets/124513439/dec8c334-8d5a-4af1-8516-25d2d70fd59f)

# Amazon CloudFront Cache and Behavior Settings

1. Set up Amazon S3 buckets:
- Create two S3 buckets for the files (e.g., 'pdf-bucket' and 'jpg-bucket')
- Upload sample PDF files to the 'pdf-bucket' and JPG images to the 'jpg-bucket'
- Create a bucket for the static website

2. For the static website:
- Enable public access
- and edir bucket policy as:- {
	"Version": "2012-10-17",
	"Statement": [
		{
			"Sid": "Statement1",
			"Principal": "*",
			"Effect": "Allow",
			"Action": "s3:GetObject"
			"Resource": "arn:aws:s3:::my-static-web-08042024/*"
		}
	]
}
- Configure as a static website
- Add the index.html (when ready)

3. Configure Amazon CloudFront:
- Create a new CloudFront distribution
- Add the static website as an origin (use website endpoint)
- Disable caching
- Add 2 more origins for the buckets containing the files and create/configure OAC
- Configure cache behavior settings for each origin based on file type (PDF or JPG) and default going to the static website
**************************************************************

AWS Global Xcellerator

![AWS GLobsl Accelerator](https://github.com/testoranit/AWSSolution-Arch/assets/124513439/80039f31-4c98-4773-ab61-ff2708015050)



do the lab similar to ROute 53 failower and 
this time add global accelerator

***********
AWS Database
RDS :- runs on EC2

RDS SUpports following db engines:-
1)Amazon Aurora
2)MYSQL
3)MariaDB
4)Oracle
5)Microsoft SQL Server
6)PostgresSQL

RDS Scalling
1)Vertical:- Scale VCPU's RAM.

2)Horizontal scaling :- u can have read replicas

![RDS RD-Horizonatal scaling](https://github.com/testoranit/AWSSolution-Arch/assets/124513439/d31c92fa-61d5-4f9b-8725-1ddf09eb189f)


![RDS Multi-AZ and Read replicas](https://github.com/testoranit/AWSSolution-Arch/assets/124513439/941c6036-4fcd-4d53-b546-4207fe1f5fa9)

RDS can be inside VPC and can have a Pip for public access and can also be priv

DB volumes & snaphots could be encyted.
encryption can only be done at the time of db creatin.


