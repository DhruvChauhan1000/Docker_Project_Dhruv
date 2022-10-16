# Give Root level permissions inside EC2
```
sudo yum update -y
sudo yum install docker
sudo systemctl start docker
sudo usermod -a -G docker ec2-user
```
# Create Custom Network Bridge
```
docker network create -d bridge <name>
```

# Install the required MySQL package
```
sudo apt-get update -y
sudo apt-get install mysql-client -y
```

# Running application locally
```
pip3 install -r requirements.txt
sudo python3 app.py
```

# Running mysql
```
docker run -d -e MYSQL_ROOT_PASSWORD=123  my_db
```


# Get the IP of the database and export it as DBHOST variable
```docker inspect <container_id>```


# Example when running DB runs as a docker container and app is running locally
```
export DBHOST=127.0.0.1
export DBPORT=3307
```
# Example when running DB runs as a docker container and app is running locally
```
export DBHOST=172.18.0.2
export DBPORT=3306
```
```
export DBUSER=root
export DATABASE=employees
export DBPWD=123
export APP_COLOR=blue
```
# Run MySQL Container and Test its connectivity to the database (inside ec2)
```
docker images (to see the pulled images)(copy the image id of sql)
docker exec -it <id paste here> bash
mysql -p
Enter Password: <whichever you created>
use employees;
select * from employee;
```
# Run the application containers for blue, pink and lime
```
docker run -d -p 8081:8080 --network <name> --name blue -e APP_COLOR=blue -e DBHOST=172.18.0.2 -e DBPORT=3306 -e DBUSER=root -e DBPWD=123 <repo URI>
docker run -d -p 8082:8080 --network <name> --name pink -e APP_COLOR=pink -e DBHOST=172.18.0.2 -e DBPORT=3306 -e DBUSER=root -e DBPWD=123 <repo URI>
docker run -d -p 8083:8080 --network <name> --name lime -e APP_COLOR=lime -e DBHOST=172.18.0.2 -e DBPORT=3306 -e DBUSER=root -e DBPWD=123 <repo URI>
```
# Try curling from inside ec2
```
curl localhost:8081
curl localhost:8082
curl localhost:8083
```
# To make sure its accessible from the Internet
```
copy the Public IP of EC2 instance in the browser with :8081, :8082, :8083 and see the results
```
