---

# install aws-vault using chocolately manager
 - Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
- choco install aws-vault
- aws-vault add premAws
--- [
    Enter Access Key Id: <>
Enter Secret Key: <>
]
-- create in root directory .aws and file config 
[
[profile premAws]
region=us-east-1
mfa_serial=arn:aws:iam::414600640364:mfa/premnath
]
- aws-vault exec premAws --duration=12h  -- CMD.EXE
- aws-vault login jonsmith
- aws-vault list

---

- install aws cli

- create iam user and attach role for that user

User name	    |Access key ID|	        |Secret access key|	                                |Console login link|
infoLearny		|AKIAWBCA7W5WAWDG37PU|	|nyQmwbUU2Z/iSSeuxBbLc+0xaQgq60HYy8EAciN/|	        |https://414600640364.signin.aws.amazon.com/console|

- aws configure
[

AWS Access Key ID [None]: AKIAWBCA7W5WAWDG37PU
AWS Secret Access Key [None]: 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
Default region name [None]: us-east-1
Default output format [None]: json

]

[for client]
-- ECR private repo : 414600640364.dkr.ecr.us-east-1.amazonaws.com/< testrunzclient >
1 - aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 414600640364.dkr.ecr.us-east-1.amazonaws.com
2 - docker build -t testrunzclient .
3 - docker tag testrunzclient:latest 414600640364.dkr.ecr.us-east-1.amazonaws.com/testrunzclient:latest
4 - docker push 414600640364.dkr.ecr.us-east-1.amazonaws.com/testrunzclient:latest
----
4.1 - docker pull 414600640364.dkr.ecr.us-east-1.amazonaws.com/testrunzclient:latest
5 - docker run docker run -p 80:3000 -d 414600640364.dkr.ecr.us-east-1.amazonaws.com/testrunzclient:latest

[for server]
-- ECR private repo : 414600640364.dkr.ecr.us-east-1.amazonaws.com/< testrunzserver >
1 - aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 414600640364.dkr.ecr.us-east-1.amazonaws.com
2 - docker build -t testrunzserver .
3 - docker tag testrunzserver:latest 414600640364.dkr.ecr.us-east-1.amazonaws.com/testrunzserver:latest
4 - docker push 414600640364.dkr.ecr.us-east-1.amazonaws.com/testrunzserver:latest
----
4.1 - docker pull 414600640364.dkr.ecr.us-east-1.amazonaws.com/testrunzserver:latest
5 - docker run docker run -p 80:3000 -d 414600640364.dkr.ecr.us-east-1.amazonaws.com/testrunzserver:latest

[for proxy]
-- ECR private repo : 414600640364.dkr.ecr.us-east-1.amazonaws.com/< testrunzproxy >
1 - aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 414600640364.dkr.ecr.us-east-1.amazonaws.com
2 - docker build -t testrunzproxy .
3 - docker tag testrunzproxy:latest 414600640364.dkr.ecr.us-east-1.amazonaws.com/testrunzproxy:latest
4 - docker push 414600640364.dkr.ecr.us-east-1.amazonaws.com/testrunzproxy:latest
----
4.1 - docker pull 414600640364.dkr.ecr.us-east-1.amazonaws.com/testrunzproxy:latest
5 - docker run docker run -p 80:3000 -d 414600640364.dkr.ecr.us-east-1.amazonaws.com/testrunzproxy:latest

----------
(Invoke-WebRequest 'https://get.pnpm.io/v6.16.js' -UseBasicParsing).Content | node - add --global pnpm
