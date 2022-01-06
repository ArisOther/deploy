## AWS
- [AWS - Dicoding Academy](https://github.com/ArisOther/aws-dicoding)
- [AWS - Coursera, Build modern python App](https://github.com/ArisOther/deploy/blob/main/aws_coursera_pythonApp.md)

## Best practice
- buat ec2 instance,\
- simpan pemfile
- cd home/pemfile
- chmod 400 arisdocker.pem
- ssh -i "arisdocker.pem" ec2-user@ec2-18-141-182-137.ap-southeast-1.compute.amazonaws.com

- kasus - 
  - Copy dari local ke ec2 = `scp -i /home/aris/aws_key/arisdocker.pem file_aris.zip ec2-user@ec2-18-141-182-137.ap-southeast-1.compute.amazonaws.com:/home/ubuntu/hortonworks`
  - Amazon Linux --> masuk root = sudo sh --> sudo su
 
## AWS Architect
- [Hosting website statis menggunakan S3 Bucket](https://www.dicoding.com/academies/266/tutorials/13472)
- Deploy Aplikasi Web di AWS
  - [architecture diagram](https://www.dicoding.com/academies/266/tutorials/13537)
  - [Membuat VPC](https://www.dicoding.com/academies/266/tutorials/13542)
  - [Membuat DB instance](https://www.dicoding.com/academies/266/tutorials/13547)
  - [Membuat EC2 instance](https://www.dicoding.com/academies/266/tutorials/13552)
- Membuat Virtual Private Cloud
  - [architecture diagram](https://www.dicoding.com/academies/266/tutorials/13592)
  - [Membuat VPC A](https://www.dicoding.com/academies/266/tutorials/16428)
  - [Meluncurkan EC2 Instance di VPC A](https://www.dicoding.com/academies/266/tutorials/16430)
  - [Membuat VPC B, Meluncurkan EC2 Instance, dan Membangun VPC Peering](https://www.dicoding.com/academies/266/tutorials/16455)
- Membangun Arsitektur yang Highly Available (Sangat Tersedia)
  - [architecture diagram](https://www.dicoding.com/academies/266/tutorials/13668)
  - [Membuat Load Balancer](https://www.dicoding.com/academies/266/tutorials/16435)
  - [Meluncurkan Auto Scaling](https://www.dicoding.com/academies/266/tutorials/16440)
  - [Pengujian](https://www.dicoding.com/academies/266/tutorials/16445)
