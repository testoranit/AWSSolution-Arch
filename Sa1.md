

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





