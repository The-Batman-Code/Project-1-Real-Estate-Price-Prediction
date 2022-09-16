![](Image.png)

# Introduction -
In this data science project I walked through the process of building a real estate price prediction website. I first built a model using sklearn and linear regression using banglore home prices dataset from kaggle.com. Second step was to create a python flask server that uses the saved model to serve http requests. Third component was the website built using html, css and javascript that allows user to enter home square ft area, bedrooms, etc and it calls the python flask server to retrieve the predicted price. During model building I covered many data science concepts such as data load and cleaning, outlier detection and removal, feature engineering, gridsearchcv for hyperparameter tunning, k fold cross validation, etc. I enjoyed creating this project and I hope you like it😊

# Tools used to create the project-
1. Python
2. Numpy and pandas for data cleaning
3. Matplotlib for data visualization
4. Sklearn for model building
5. Jupyter Notebook in Visual Studio Code as IDE
6. Python flask server for http server
7. HTML/CSS/Javascript for UI

# Deploy this app to cloud (AWS EC2)-

1. Create EC2 instance using amazon console and in secutity group allow HTTP/HTTPS incoming traffic.
2. Now connect to your instance using PuTTY windows application.
3. Become the root user to avoid permission errors with the command-
```
sudo su
```
4. Update the linux instance and install nginx using using the commands-
```
sudo apt-get update
sudo apt-get install nginx
```
5. We can check whether the nginx server is running by loading the url of the instance in the browser.
6. Now login to your instance and transfer the application folder (download this repo, extract it and rename the folder as BHP, this folder is now your application folder😊) into the EC2 instance using WinSCP application.
7. Navigate to the location using the command-
```
cd /etc/nginx/sites-enabled
```
8. Unlink the deafult file using the command-
```
sudo unlink default
```
9. Navigate to the location using the command-
```
cd /etc/nginx/sites-available
```
10. Now create the file named bhp.conf using the command-
```
sudo vim bhp.conf
```
11. Enter the following data in bhp.conf file-
```
server {
    listen 80;
        server_name bhp;
        root /home/ubuntu/BHP/client;
        index app.html;
        location /api/ {
             rewrite ^/api(.*) $1 break;
             proxy_pass http://127.0.0.1:5000;
        }
}
```
12. Now navigate to the following location using the command-
```
cd /etc/nginx/sites-enabled
```
13. Create the following symlink using the command-
```
sudo ln -v -s /etc/nginx/sites-available/bhp.conf
```
14. Now restart the nginx server using the command-
```
sudo service nginx restart
```
15. Reload the instance link in the browser, you should see your app.html load in the browser😊
16. For flask server to run install python using the command-
```
sudo apt-get install python3-pip
```
17. Now we need the necessary python libraries, so run the following commands one by one-
```
sudo pip3 install Flask
sudo pip3 install numpy
sudo pip3 install scikit-learn
```
18. Naviagte to the location - /home/ubuntu/BHP/server and run the following commmand-
```
python3 server.py
```
19. Restart the nginx server using the following command-
```
sudo service nginx restart
```
20. Reload the instance link in the browser and see the magic❤️. Congratulations😍😊.

# Error handling
Here we will troubleshoot the errors I faced during the making of this project😁

## Error 1 (403 forbidden error)-
1. Open the WinSCP application and navigate to /usr/share/nginx/html and copy the path.
2. Now check the permission of the copied path using the command-
```
namei -om /usr/share/nginx/html
```
3. Check the permissions carefully. We want the same permissions for our project(BHP) folder.
4. Change the permission of the ubuntu/user folder using the following command-
```
chmod 755 /home/ubuntu
```
5. To verify the change in permissions enter the following command and cross-check with the permissions in step 2-
```
namei -om /home/ubuntu/BHP
```
6. Now restart the nginx server using the command-
```
sudo service nginx restart
```
7. Refresh the browser and the app.html file should load. Congratulations😊

[Reference Video](https://www.youtube.com/watch?v=CtRSx3EvBIY&list=WL&index=26/)

## Error 2 (Could not find path)-
1. This error may be because we created util.py using windows path syntax not linux.
2. Navigate to the /home/ubuntu/ path and enter the following command to edit the util.py file-
```
sudo nano BHP/server/util.py
```
3. Now wherever you see mention of path replace all '\\\' with '/' and save the file.
4. Navigate to the /home/ubuntu path and enter the following command to start the flask server-
```
python3 BHP/server/server.py
```

You seem interested in machine learning😉. Thank you for reading till here. Cheers!!!🍻
