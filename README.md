# Route-53-Domain-level-hosted-zone-manage-using-IAM-user

## Description

In this article I will help you to manage the Amazon Route 53 domain hosted zone using IAM user. 
Amazon Route 53 is a highly available and scalable cloud Domain Name System (DNS) web service. It is designed to give developers and businesses an extremely reliable and cost effective way to route end users to Internet applications by translating names like www.example.com into the numeric IP addresses like 192.0.2.1 that computers use to connect to each other. Amazon Route 53 is fully compliant with IPv6 as well.

A hosted zone is an Amazon Rote 53 concept. A hosted zone is analogous to a traditional DNS zone file; it represents a collection of records that can be managed together, belonging to a single parent domain name. All resource record sets within a hosted zone must have the hosted zone's domain name as a suffix.

## Prerequisite

AWS account with management console access and full access to Route 53 and IAM services.

## Diagram

![iam-route53 drawio](https://user-images.githubusercontent.com/100775801/161685467-bd6c881f-15aa-4a52-97bf-a483bc25dbb1.png)

As you can see in the diagram, we are going to create a user Sanu and providing complete manage access to domain "Domain2.com" which hosted in Amazon Route 53.
The same IAM user can only see other hosted zones in Route53 but not able to manage them.

## Creating IAM Policy

First we need to create an IAM policy for the user. Login into your AWS management console and search IAM on the top navbar. Then select IAM from the drop-down. From the IAM dashboard, click on policies and click Create Policy.

![image](https://user-images.githubusercontent.com/100775801/161687654-6d00b5a0-4537-44ca-8e9b-4d9abc689ddc.png)

Then select JSON and add the Below IAM policy

~~~
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "VisualEditor0",
            "Effect": "Allow",
            "Action": [
                "route53:GetHostedZone",
                "route53:ChangeResourceRecordSets",
                "route53:ListResourceRecordSets"
            ],
            "Resource": "arn:aws:route53:::hostedzone/<Hosted zone ID of domain from route 53>"
        },
        {
            "Sid": "VisualEditor1",
            "Effect": "Allow",
            "Action": [
                "route53:ListHostedZones",
                "route53:GetHostedZoneCount",
                "route53:ListHostedZonesByName"
            ],
            "Resource": "*"
        }
    ]
}
~~~

##### please replace <Hosted zone ID of domain from route 53> with your domains hosted zone id.
To get the hosted zone id go to Route53 and select the domain. There you can see the option Hosted zone details.
![image](https://user-images.githubusercontent.com/100775801/161690253-3b1635a7-83a0-4b18-b735-7248869e63d1.png)


After adding the policy save the policy with a name and create a user with the new policy.

## Conclusion

This tutorial we discussed how to manage the Amazon Route 53 domain hosted zone using IAM user. We have done that with the help of IAM policy.


### ⚙️ Connect with Me

<p align="center">
 <a href="https://www.instagram.com/itz__me_omkar/"><img src="https://img.shields.io/badge/Instagram-E4405F?style=for-the-badge&logo=instagram&logoColor=white"/></a>
<a href="https://www.linkedin.com/in/sanu-das-t-3722891b5"><img src="https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white"/></a> 

