//permission on nginx

sudo chown -R www-data:www-data /home/ubuntu/poridhi-assignment-first-phase/poridhi-assignment-non-optimized/poridhi-assign-non-optimized/public
sudo chmod -R 755 /home/ubuntu/poridhi-assignment-first-phase/poridhi-assignment-non-optimized/poridhi-assign-non-optimized/public


sudo chmod 755 /home/ubuntu
sudo chmod 755 /home/ubuntu/poridhi-assignment-first-phase
sudo chmod 755 /home/ubuntu/poridhi-assignment-first-phase/poridhi-assignment-non-optimized
sudo chmod 755 /home/ubuntu/poridhi-assignment-first-phase/poridhi-assignment-non-optimized/poridhi-assign-non-optimized
--------------------

nginx

------------------------

server {
    listen 80 default_server;
    listen [::]:80 default_server;

    server_name your_server_ip_or_domain;

    location / {
        root /home/ubuntu/poridhi-assignment-first-phase/poridhi-assignment-non-optimized/poridhi-assign-non-optimized/public;
        try_files $uri $uri/ =404;
    }

    location /video {
        proxy_pass http://localhost:3000/video;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}

--------------------------------------------------

index.html

-------------------------------------

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Video Streaming</title>
</head>
<body>
    <h1>Video Streaming Example</h1>
    <video controls width="900">
        <source src="http://your_server_ip_or_domain/video" type="video/mp4">
        Your browser does not support the video tag.
    </video>
</body>
</html>

---------------------------------------------------


sudo systemctl restart nginx
pm2 restart app
sudo npm install -g pm2
pm2 status
pm2 log
pm2 start app.js --name myapp
pm2 status
pm2 save
