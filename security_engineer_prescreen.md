### The following questions are meant to serve as an assessment; answer as much as you are able to answer (even if you can't fully answer a specific question). Make sure to explain your answers
@. Explain the differences between a VM, container, chroot jail, and Kubernetes pod
@. Suppose that you have an s3 bucket, `bucket`, which contains a file, `wordlist`, which contains a comma-separated, list of words. Write a lambda function which will receive a json event payload containing a query string. The Lambda function should check whether the query word is in the wordlist and place the result on an SQS queue as well as return it

 Sample wordlist:
 ```
 working,for,okcupid,is,really,fun,come,join,us
 ```

 Sample request:
 ```
 {
   "query":"for"
 }
 ```

@. Write Terraform code to deploy the above
@. Explain the CIA triad and provide an example of each
@. Write a bash script to find every file owned by the user `joe` and output the number of lines in the file
@. How would you go about investigating a security incident in AWS?
@. How do you stay up to date on security news?
@. Describe the process, in as much detail as possible, that occurs when a user opens a web browser and types in https://okcupid.com/ until the site is displayed on their browser
@. Describe a security incident response process (either one you have been a part of or a public incident that you read about)
@. What is the principle of least privilege and why is it important? Provide an example
@. What is a 0 day?
@. What is a CVE?
@. Explain what XSS is
@. What is MFA? List the factors
@. Using the [Harry Potter API](https://hp-api.herokuapp.com/), retrieve a list of students and their houses, print a list sorted by house then alphabetical order.
