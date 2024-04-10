- Commands that were used in order to Host the website | Start and Enabeling Server.
- sudo su -
- yum update -y
- yum install -y httpd
- systemctl status httpd
- mkdir temp
- cd temp
- wget https://www.free-css.com/assets/files/free-css-templates/download/page294/rent4u.zip
- unzip complex.zip
cd complex
ls -lrt
mv * /var/www/html
systemctl enable httpd
systemctl start httpd
