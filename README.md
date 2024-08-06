# Visual Studio Code on EC2

This repository introduces how to access and use VSCode hosted on EC2 from a browser. The connection is made via Session Manager, so IAM permissions are used for authentication. The access destination will be localhost. Please note that this repository does not introduce connecting from your local VSCode to an EC2 instance via Remote SSH. 

I run this workshop in Ubuntu Desktop 22.04. In the workshop, you will see the Window Terminal. That is because I have SSH to the Ubuntu Desktop from my Window 11 for easier usage. You can just use the terminal in the Ubuntu Desktop.

## Features
- You can use VSCode from a browser
- Node.js environment is installed
- 128 GB of storage is provided by default
- aws cli can be executed with AdministratorAccess equivalent permissions
- The EC2 instance hosting VSCode belongs to a Private Subnet, so it is not exposed to the internet. The connection is made via Session Manager.

## Prerequisites
- Node.js runtime environment
- [`aws` command](https://aws.amazon.com/cli/) (AdministratorAccess equivalent permissions are required to run AWS CDK)
- `git` command
- `jq` command

### Install nodejs
Refer: https://www.youtube.com/watch?v=kYtRSSpUduw
1. Install nodejs with the the command `sudo apt install nodejs`.


2. Install npm package manager with the command `sudo apt install npm`.

4. However, you will see that the version is not up-to-date. To update the node version. run the command `sudo npm install -g n`. 


<img width="30%" src=https://github.com/user-attachments/assets/61bdc8a7-b088-4731-bb9f-95b69f11dc33>

'n' provides an interactive way to manage Node.js versions

5. To istall the latest LTS version of Node.js, run `sudo n lts`.
   
![image](https://github.com/user-attachments/assets/58762f10-5831-4a25-ab15-ed4d89bba205)

Check version:

<img width="30%" src=https://github.com/user-attachments/assets/9af23ebe-53b6-4542-a7f1-e84133ed4527>


### Install Session Manager plugin
1. Download the session manager plugin with the command
```bash
curl "https://s3.amazonaws.com/session-manager-downloads/plugin/latest/ubuntu_64bit/session-manager-plugin.deb" -o "session-manager-plugin.deb"
```

2. Install the plugin with the command
```bash
sudo dpkg -i session-manager-plugin.deb
```

![image](https://github.com/user-attachments/assets/81de7e05-2672-418d-b1a5-c20c139c8393)

## Installation

1. First, clone this repository.

```bash
git clone https://github.com/aws-samples/vscode-on-ec2-for-prototyping
```

The application uses the [AWS Cloud Development Kit](https://aws.amazon.com/cdk/)(CDK) for deployment. Node.js is required to run. First, run the following command. 

2. Run all commands from the root of the repository.

```bash
npm ci
```
<img width="80%" src=https://github.com/user-attachments/assets/5dd85c67-8096-45f1-a4e0-579a14a44087>


3. (Optional) If you have never used CDK before, a [Bootstrap](https://docs.aws.amazon.com/cdk/v2/guide/bootstrapping.html) process is required only the first time. The following command is not required if already bootstrapped.

```bash
npx cdk bootstrap
```

![image](https://github.com/user-attachments/assets/b6c24c3a-9f45-4f01-85f6-37d06b9a78b8)


4. Then deploy the AWS resources with the following command:

```bash
npx cdk deploy
```
![image](https://github.com/user-attachments/assets/eb8c0ed9-34a7-4e6b-98f0-1e962a1331f5)

5. When it asks "Do you wish to deploy?" Type y:

![image](https://github.com/user-attachments/assets/bc4971bf-a5d2-4aee-b093-c0ff6c0d6557)


6. After deployment completes, check that the EC2 instance was created in the [management console](https://console.aws.amazon.com/ec2/home#Instances). Also please confirm that the Status check changes from Initializing to checks passed. 


7. Once checks passed is confirmed, run `session.sh` to create a session:

```bash
./session.sh
```
<img width="60%" src=https://github.com/user-attachments/assets/2b4b9c43-1227-46e1-a967-0b38d27f0933>


8. Once the session is created, open http://localhost:8080 in your browser. If it does not connect, please refer to [Troubleshooting](#Troubleshooting).

![image](https://github.com/user-attachments/assets/0f214ead-8bf1-42f7-ae7a-cafca0af7b61)


## Cleanup

To delete the environment, run the following command:

```
npx cdk destroy
```
![image](https://github.com/user-attachments/assets/311b4d8c-bd2b-4056-89fc-973ec3efdbfa)

## Security

See [CONTRIBUTING](CONTRIBUTING.md#security-issue-notifications) for more information.

## License

This library is licensed under the MIT-0 License. See the LICENSE file.

