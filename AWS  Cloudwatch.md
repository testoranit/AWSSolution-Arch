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



