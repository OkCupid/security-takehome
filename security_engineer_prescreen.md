## Please fork this repo. Open a PR when you are ready to submit. Thank you!

### The following questions are meant to serve as an assessment; answer as much as you are able to answer (even if you can't fully answer a specific question). Make sure to explain your answers.




1. Explain the differences between a VM, container, chroot jail, and Kubernetes pod.

A VM is a virtualized computer that can be run as an application that behaves as a completely separate operating system whereas a container is a virtual platform to run a single application that contains all components needed to run that application.  Kubernetes pods are the smallest unit of deployment in Kubernetes to have one or more running containers which share resources and specifications on how to run the containers.  Lastly, a chroot jail creates a false root from which a service can run, securing the server and the service as the service and its children cannot access or run files outside the false root.

2. Explain the CIA triad and provide an example of each.

The CIA triad is a guide for cybersecurity to prioritize different aspects of data.  The three pillars are confidentiality, integrity, and availability.  
Confidentiality means making sure that data is not accessed by anyone it should not be available to, such as personal identifying information a user inputs into their account information like their social security number or address, is not publicly available to everyone.
Integrity means making sure that data has not been altered by a malicious actor, for example, in a dating app, the information the user input has not been changed by a malicious actor and any misidentifying information about the user was input by the user themselves.
Availability means making sure that application or data is available for usage.  If a dating app goes down, then many people would be very upset about missing out on prospective matches.  

3. How would you go about investigating a security incident in AWS?

I would start by using CloudTrail to search for data surrounding the security incident and VPC Flog Logs to see traffic coming in and out of the network.  When unusual activity is detected, I would verify whether it is malicious or not.  Then I would remove access for the user or isolate the VM or subnet.  If it was the user that was compromised, then I would reset the compromised credentials.  If the VM was compromised, I would take a snapshot and reimage the VM.  Then I would further interrogate the logs to see how the compromise occurred to prevent further compromise.

4. How do you stay up to date on security news?

I listen to podcasts such as Darknet Diaries and the CyberWire Daily and subscribe to blogs such as Krebs on Security and We Hack Purple as well as following InfoSec Twitter.  

5. Describe the process, in as much detail as possible, that occurs when a user opens a web browser and types in <https://okcupid.com/> until the site is displayed on their browser.

When the user requests okcupid.com, the query heads out to the internet and is received by a DNS recursive resolver which will track down the DNS record.  The resolver queries a DNS root nameserver which responds with a Top Level Domain (TLD) DNS server, which in this case will be .com.  The resolver then makes a request to the .com TLD DNS server, which responds with the IP address of the domain’s nameserver and the resolver sends the domain nameserver a query which returns the IP address to the resolver which then responds to the browser with the IP address of the requested domain.  The browser is now able to make an HTTP request to the IP address and the server then returns the web page to be displayed in the browser.  

6. Describe a security incident response process (either one you have been a part of or a public incident that you read about)

When responding to a security incident, such as a suspicious binary, I first check the hash against VirusTotal to determine if it is known malicious and to gather further information.  I then check the device logs starting with activity prior to the security event to attempt to determine where the binary originated.  After reviewing the logs and hash information, I then determine if this was a deliberate action and therefore a false positive that may require an exclusion or a true positive and reach out the to the system administrator to work with them to remove the malicious binary. 

7. What is the principle of least privilege and why is it important? Provide an example.

The principle of least privilege is provisioning an account with the minimal permissions so that the account can only perform the tasks required of it but cannot access anything more.  This is important in the case of vulnerability in that a vulnerability affecting one application cannot be used to exploit the rest of the device.  

8. What does the OWASP top 10 refer to? Pick one and explain an experience you had mitigating or exploiting it. 

The OWASP top 10 refers to what is considered the top 10 most critical security issues to web applications.  As an amateur hack the box and CTF participant, I’ve used this injection in local file inclusions to expose sensitive data, like /etc/passwd and /etc/shadow and have further been able to use remote code execution to gain a foothold to the device.

9. Explain how firewall rules work.

Firewall rules examine packets and allow or deny the traffic based on specified parameters.  The rules listed at the top are applied first and a general deny is listed at the bottom to deny any traffic with the idea that the preceding rules are allow rules and anything that is not allowed should be blocked from the network.  These rules can be placed on one device or pushed to a network via something like GPO.

10. Explain SSL/TLS. Are they the same? Which one is better?

SSL and TLS are the cryptographic protocols that ensures HTTPS security.  TLS is the more secure successor to SSL and should be used instead.

11. What is a botnet? Explain how they work. 

A botnet is a network of compromised devices controlled by someone via command and control to perform malicious attacks, such as distributed denial of service by using the botnet to exhaust a server or system with a multitude of requests, resulting in that system go offline.  They have also been more prevalent in bitcoin mining.

12. What is the difference between public and private IP addresses? How do you identify either? 

A public IP address is the external IP address that the world sees when a request is sent to the internet whereas a private IP address is used internally in a network to identify which specific device it belongs to.  For example, multiple devices in a network can use the same external IP address, but when the information is returned to the external IP address and it is then translated via Network Address Translation to arrive at the correct destination.  The internal IP address ranges are 10.0.0.0-10.255.255.255, 172.16.0.0-172.31.255.255 and 192.168.0.0-192.168.255.255.

13. What is MFA? List the factors.

Multi-factor authentication refers to the usage of 2 or more ways to authenticate to ensure that the user is truly who they say they are.  The three factors are something you know, something you have, or something you are.  Something you know is a password or PIN.  Something you have is an ID or yubikey.  Something you are is a biometric factor, like your face. 

14. What is the difference between Symmetric and Asymmetric encryption? Below you will use gpg to encrypt a folder, what type of encryption is gpg an example of?

Symmetric encryption uses the same key for encryption and decryption whereas asymmetric encryption uses a public key for encryption and a private key for decryption.  GPG is an example of symmetric key encryption.

### The below is intended to test your comfort level with scripting and experience with different technologies, such as AWS, Terraform, Bash and/or Python. Please answer what you can to the best of your ability. If you are unfamiliar with something, skip it. 
### When you complete this tasks, create .txt or a .MD file called `results` with the output of the questions you completed (be sure to annotate the question number), make a directory named `submission_<your initials>` and copy all the code you wrote, the `results` file, and all related and necesary files to the directory - *Please include the answers to the questions above as well. 
### You will then encrypt the directory with our public gpg key and upload it to your fork and open a PR. (Our key is uploaded to `keys.openpgp.org` with the email `security@okcupid.com`. If you are unfamiliar with this process, please use this site as reference `https://yanhan.github.io/posts/2017-09-27-how-to-use-gpg-to-encrypt-stuff/`)

1. Suppose that you have an s3 bucket, `bucket`, which contains a file, `wordlist` that contains a comma-separated list of words. Write a lambda function which will  receive a json event payload containing a query string. The Lambda function should check whether the query word is in the wordlist and place the result on an SQS queue as well as return it.

   Sample wordlist:

   ``` 
   working,for,okcupid,is,really,fun,come,join,us
   ```

   Sample request:

   ``` json
   {
     "query":"for"
   }
   ```
2. Write Terraform code to deploy the above.
3. Using the [Harry Potter API](https://hp-api.herokuapp.com/), retrieve a list of students and their houses, print a list sorted by house then alphabetical order.
4. Write a bash script to find every file owned by a user `ex: joe` and output the number of lines in the file.
5. Create a file named `permissions.txt` and grant **all** permissions to the owner of the file, **read and execute** permissions for the group, and **execute** permissions for all other users. Take a screenshot of the file and the permissions after you are done.
