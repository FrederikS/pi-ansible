# pi-ansible

## Requirements

### Setup aws user to use for aws cli

Besides already having a hosted DNS zone under AWS Route 53, you need to set up
the following in the AWS `IAM console`:

- Create a user.
- Write down the "Access Key ID" and "Secret Access Key" credentials.
- Click on the newly created user to edit its properties. Click
  `Inline Policies` to create one. Use the Policy Generator:
  - **Effect**: Allow
  - **AWS Service**: Amazon Route 53
  - **Actions**: select only "ChangeResourceRecordSets"
  - **Amazon Resource Name (ARN)**: `arn:aws:route53:::hostedzone/%ID%`
    - You can get the
      [ID](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/UsingWithIAM.html)
      of your hosted zone from the list of the "Hosted zones" in your AWS Route
      53 service.
    - Example: `arn:aws:route53:::hostedzone/Z148QEXAMPLE8V`
- Click Next. The final Policy Document would look something like:

  ```json
  {
    "Version": "2012-10-17",
    "Statement": [
      {
        "Sid": "Stmt1456599587000",
        "Effect": "Allow",
        "Action": ["route53:ChangeResourceRecordSets"],
        "Resource": ["arn:aws:route53:::hostedzone/Z148QEXAMPLE8V"]
      }
    ]
  }
  ```

- Click "Apply Policy".

### Links

- <https://github.com/famzah/aws-dyndns>
- <https://unix.stackexchange.com/questions/409812/how-does-one-automatically-update-route53-from-a-raspberry-pi-server-at-home>
- <https://superuser.com/questions/1180158/how-to-resolve-dynamic-dns-domain-to-internal-ip-without-nat-loopback-or-dns-cha>
- <https://fabianlee.org/2021/09/16/kubernetes-k3s-with-multiple-istio-ingress-gateways/>
- <https://nerdiy.de/raspberrypi-ssh-reagiert-nicht-oder-ist-sehr-langsam-problem-beheben/>
- <https://github.com/DougieLawson/backlight_dimmer>
- <https://askubuntu.com/questions/237963/how-do-i-rotate-my-display-when-not-using-an-x-server>
