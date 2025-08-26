### Step 1: Launch EC2 for Docker
- Launch an Ubuntu 22.04 EC2 instance (t2.micro free tier is fine).
- Security Group: allow 22 (SSH), 8080 (Custom TCP) and 80 (HTTP) from your IP.

### Step 2: Install Docker
- SSH into your new EC2:
```bash
ssh -i /path/to/your.pem ubuntu@<ec2-public-ip>
```
- Install Docker:
```bash
sudo apt update
sudo apt install -y docker.io
sudo systemctl enable --now docker
sudo usermod -aG docker ubuntu
```
- Log out and log back in so ubuntu can run Docker without sudo.

- Check:
```bash
docker --version
```
### Step 3: Run a Web Server Container
- Simplest way: run nginx container (web server).
```bash
docker run -d --name myweb -p 80:80 nginx
```
- Check container:
```bash
docker ps
```
- Open in browser:
```bash
http://<ec2-public-ip>
```
- You should see the Nginx welcome page 🎉
<img width="900" height="265" alt="this" src="https://github.com/user-attachments/assets/bd1e94de-c37e-4709-b451-3de1af0804f1" />

### Step 4: Monitor & Logs
- View logs:
```bash
docker logs myweb
```
- Check container stats:
```bash
docker stats
```

### Step 5: Custom Webpage (optional)

- Create index.html
```bash
echo "<h1>Hello, I'm Vishesh ghule a DevOps engineer</h1>" > index.html
```
- Run with custom page:
```bash
docker run -d --name myweb2 -p 8080:80 -v $(pwd)/index.html:/usr/share/nginx/html/index.html nginx
```
- Visit:
```bash
http://<ec2-public-ip>:8080

OR

curl http://localhost:8080
```
<img width="900" height="123" alt="Screenshot from 2025-08-26 13-31-48" src="https://github.com/user-attachments/assets/733d1652-1b6c-41af-a211-b9d2e34e27db" />




