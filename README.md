# AWS EC2 VPN

Set up a VPN server on an AWS EC2 Instance via a single, self contained, Cloud Formation template.

See [aws-ec2-vpn.json](https://github.com/aadarsh-shetty/AWS-EC2-VPN/blob/master/aws-ec2-vpn.json) for raw template.

## Setup via AWS Console

Follow the [AWS Cloud Formation Guide](http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/cfn-console-create-stack.html)
to create a new Cloud Formation Stack from the [aws-ec2-vpn.json](https://github.com/aadarsh-shetty/AWS-EC2-VPN/blob/master/aws-ec2-vpn.json) template.

## Setup via CLI

You must have the [aws-cli](https://aws.amazon.com/cli/) installed and available in your path.

If you do not have aws-cli, for installation of the same [refer](http://docs.aws.amazon.com/cli/latest/userguide/tutorial-ec2-ubuntu.html).

Additionally, you must set your default AWS credentials to a user with permissions to setup a VPC and launch EC2 instances.

Clone down this repo and execute the **setup.sh** script with the following input.

```shell
$ sh setup.sh YOUR_VPN_PRE_SHARED_KEY YOUR_VPN_USERNAME YOUR_VPN_PASSWORD
```

Once the setup is complete, the script will return the persistent EIP of the Instance. For example:

```shell
$ sh setup.sh MySuperSecretPreSharedKey vpnuser TheVPNUserPassword
VPN Setup in progress.
VPN Setup complete. IP address is '35.164.187.145'.
```

## Client Setup

### MacOS

Under **Sytem Preference** / **Network** hit the **+** button to add a new connection.

Change the **Interface** to **VPN**. 

Change the **VPN Type** to **L2TP over IPSEC**.

Ggive the VPN a name in **Service Name**.

Click Create.

![image1](https://raw.githubusercontent.com/aadarsh-shetty/AWS-EC2-VPN/master/images/image1.png)

Add the IP address, which was output from the setup.sh script above, as the **Server Address**.

The user you specified, as **YOUR_VPN_USERNAME** in the script above, as the **Account Name**.

![image2](https://raw.githubusercontent.com/aadarsh-shetty/AWS-EC2-VPN/master/images/image2.png)

Click on **Authentication Settings**. 

Add the password you specified, as **YOUR_PASSWORD** in the script above, as the **Password**.

Add the pre shared key you specified, as **YOUR_VPN_PRE_SHARED_KEY** in the script above,
as the **Shared Secret**.

Click OK.

![image3](https://raw.githubusercontent.com/aadarsh-shetty/AWS-EC2-VPN/master/images/image3.png)

Click on **Advanced Settings** ensure that **Send all traffic over VPN connection** is checked.

Click OK.

![image4](https://raw.githubusercontent.com/aadarsh-shetty/AWS-EC2-VPN/master/images/image4.png)

Click on **Connect** to connect to the VPN.

![image5](https://raw.githubusercontent.com/aadarsh-shetty/AWS-EC2-VPN/master/images/image5.png)

Ensure your traffic coming from the VPN IP via [What Is My IP](https://www.google.com/#q=what+is+my+ip).

![image6](https://raw.githubusercontent.com/aadarsh-shetty/AWS-EC2-VPN/master/images/image6.png)

## Costs

The only charge will be for the EC2 instance hours, currently set to t2.nano, and network bandwidth.

At the time of this writing the instance hours cost under $5.00 USD per month in us-west-2 if the VPN is ran continuously.

See [AWS On Demand Pricing](https://aws.amazon.com/ec2/pricing/on-demand/) for current pricing.
