# Steps for Deploying the Entire Flow

I started off by creating a directory in my Linux EC2 instance and initialised it as a Git repository. Then I downloaded a eCommerce website template from the "themewagon.com" website to the Linux EC2 instance. I then staged the website directory to the Git repository and set the Git global configuration to my GitHub username and email and commited the initial basic website.

I then had to create a repository on GitHub with the name "MarketPeak_Ecommerce" and link the my local repositroy from Linux EC2 with my GitHub and push the commit to the from local repository to the remote repository on GitHub.

After that I had to created an Amazon Linux AMI EC2 instance from AWS Management Console and clone the website from the GitHub remote repository using HTTPS link onto the Linux AMI EC2 instance.

Next I had to install the Apache HTTP Server (httpd) onto the Linux AMI EC2 instance, which would be used to host the website. "sudo yum update -y" command was used to update the Linux server. "sudo yum install httpd -y" command installs the httpd server. "sudo systemctl start httpd" starts the web server and "sudo systemctl enable httpd" ensure the web server starts on server boot.

Then I had to configure httpd so that it would host my website rather than using the default webpage. "sudo rm -rf /var/www/html/*" was used to delete anything that was in the html directory and "sudo cp -r ~/MarketPeak_Ecommerce/* /var/www/html/" command copied everything that was in "MarketPeak_Ecommerce" folder into the "html" folder. After that I have to use the "sudo systemctl reload httpd" command to reload the server so it can put the changes into effect.

Next step would be to use the Linux AMI EC2's public ip address to access the website, which is hosted by Apache HTTP Server (httpd).

Then comes Continuos Intergration and Deployment. This is done on the EC2 instance and by making a branch using "git checkout -b Development" and make changes away from the master branch, which is visible to everyone. After making any chances, they need to staged, commited with a meaningful message and then pushed to the Development branch on GitHub.

The changes pushed to the Development branch are not live yet. The Development branch needs to be merged with Master branch using the "git checkout main" to go to the Master branch and then using the "git merger Development" to merge the change with Master branch.

Once the changes have been merged, the changes need to be pushed to the master branch, which then can be pulled onto the Linux AMI EC2 instance, where the web server is running. The last step would be to restart the web server so the changes become live and go the Linux AMI EC2's public IP address to check if everything is working perfectly.

# 