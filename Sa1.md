

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




