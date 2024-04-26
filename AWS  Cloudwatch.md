AWS CLoudwatch
AWS resource health:- Eg:- Ec2(cpu utilization)
real time data==?
Monitoring ur Billing aaccount.(monthly bill crosses a certain threshold).
custom metrics:- appl is processing certain workloads and each application takes certain threshold.
Application logs :- null reference exeption,404 stateus codes.

GO to cloudwatch-->AWS Resource health_>urown  aws service health(metrics)
u can create alarms on the cloudwatch metrics u track
and can trigger an notification via SNS or email alos could trigger an automated actions like firig a custom script or call an API
or some custom code.
AWS SNS topic:-is a communication channel to send messages and subscribe to notifications.


VIsualize the data
multile metrics on single graph.(metrics grpaht) are in real time
eg:- number of files in 2 diffrent S3 buckets which can get in visual form.

Clowatch:-provides streaming events to the changes to ur Aws resources
eg:- if u deploy a new ec2 instance, cloudwatch monitors it and can trigger a lambda function that registers this instances
wit ur organization DNS in route 53.

custom metrics for ur application also possible.(no of times failed login attempts,no of orders for an ecommerce stor)

*********AWS SNS:-
fully mannged push notification services to individual messages or fan out messages to large number of recipents.
can send to mobile,any other hhtp endpont
based on pub sub model:- where the sender sends messages to a topic.and all the endpoints that are subscribed that topic will receive the message.
goto Clodwatch-->create alarm-->choose metrics-->specify the config(eg:- number of objects>50)
Sns-->create a new topic-->
Then create subsciption
protocal:- email
go to ur email:- confirm subsciption

deleting alarm will only delete alarm and nort delete topics/subsciption or the metrics.

Cloudwatch:- can also aggegarte logs from multiple sources into single consildate views.
Monitor and react to alarms

State of Alarm:-
OK:- Metric is in defined threshold and alarm is not triggered yet
Alarm:- outside of metric threshold and alarm has been triggered.
insufficnet data:- enough metric is not available to detect the alarm state.Ec2 doesn't send metrics to cloudwatch
u need to figure ot why


CLoudwatch dashboards:-In complex we need to monitor different services with more metrics,u can have dashboards  
consolidated view
each dashboards:- can display multple metrics can be accesoirsed with texts and images.
u can pull data from multiple AWS regions to single dashboard for getting a global view

Awscloudwatch-->dashboards-->CPU utlization
u can have multiple aws services/resource with their metrics on 1 single dashboard

Lab:- set alarm for ec2 cpu utlization

**AWS features
Billing alarms:- alarms on estimated charges monitor estimated charges.
we can integaret it with some scripts to decommision the resources which are not in use and adding to bill.

**Events
state changes for AWS resources
number of scenarois automate the ops and maintainece of cloud infra
eg:- brand new instannce addition to DNS service.

Logs:-view,index and search logs from diff services.

Metrics:_ core foundation of cloudwatch

AUto Scaling integration:-up and down as per requirement
eg:- when utlization is low for ur app then stop 1 instance out of 2 instances and spin up an instance if required.

u can also do failed reboot of ec2(where cloud watch needs IAM role access to rebboot ec2)
also integrate with 3 party monitoring tools

U can creae custom metrics(mem utli exlusive of cache and buffer,disk space used,and swap space utlixatio for app)
u can create alarms on it.

***Monitoring Ec2

Metrics and alarms
custom metrics
and do status checks
Metrics are free
by defal metrics are collected every 5 min , with extra cost u can get 1 min metrics



AWS Status checks🥇
system status checks:-underlying aws systems(physical quipment behind the serice,like physical host of server)
Instance status checks:- aws ec2 has any probmens


**********Custom metrics:-
cloud watch Monitoring scripts from sample librabry of aws
custom IAM role:- so that ec2 can report the custom metrics to cloudwatch(custom metrics role)



