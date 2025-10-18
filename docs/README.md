# Nginx (Hello & Welcome Demo)
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://github.com/user-attachments/assets/9335b488-ffcc-4157-8364-2370a0b70ad0">
  <source media="(prefers-color-scheme: light)" srcset="https://github.com/user-attachments/assets/3a7eeb08-1133-47f5-859c-fad4f5a6a013">
  <img alt="NGINX Banner">
</picture>

## What is Nginx?

[Nginx](https://www.nginx.com/) (pronounced "Engine X") is a high-performance web server and reverse proxy server. It is widely used to serve static files, handle load balancing, and manage HTTP traffic efficiently. Nginx is lightweight, fast, and highly configurable, making it one of the most popular web servers in the world.

## Why this Project?

The goal of this project is to **learn and practice serving static web pages using Nginx on a Windows setup** without writing any backend API.  

By doing this project, we learned:

- How to install and run Nginx on Windows.  
- How to configure `nginx.conf` to serve custom HTML pages.  
- How to create simple endpoints (`/hello` and `/welcome`) using only Nginx configuration.  
- How to debug Nginx errors and fix configuration issues like duplicate `server_name`.  

This project is **purely educational**, focusing on understanding the basic Nginx workflow and static file serving.

---

## Project Structure

nginx-1.28.0/

├─ conf/ # Nginx configuration files

│ └─ nginx.conf # Main configuration with server block

├─ myapp/ # HTML pages

│ ├─ hello.html

│ └─ welcome.html

├─ logs/ # Nginx log files (ignored in git)

└─ nginx.exe # Nginx executable (ignored in git)


## Steps to Run the Project

### 1. Download Nginx
Download the **Windows version of Nginx** from [nginx.org](https://nginx.org/en/download.html) and place it in your project folder.
 ---
 
### 2. Add HTML Pages
Create a folder `myapp/` and add two simple HTML files:
- `hello.html`  

  ```
  Hello
  ```
- `welcome.html`

    ```
    Welcome
    ```
---

### 3. Configure Nginx
Update `conf/nginx.conf` with the following `server` block inside `http` block:
```
server {
    listen 80;
    server_name localhost;

    location = /hello {
        alias C:/path/to/myapp/hello.html;
        default_type text/plain;
    }

    location = /welcome {
        alias C:/path/to/myapp/welcome.html;
        default_type text/plain;
    }

    location = / {
        return 200 "Nginx is running. Use /hello or /welcome";
        default_type text/plain;
    }
}

```
**Note**: Replace `C:/path/to/myapp/` with your actual absolute path to the myapp folder.



### 4.Test Nginx Configuration
Open **VS Code terminal** in the Nginx folder and run:
```
.\nginx.exe -t

```
You should see:
```
syntax is ok
configuration test is successful

```

### 5. Start Nginx
```
.\nginx.exe

```
Check if the process started:
```
Get-Process -Name nginx

```

### 6. Access the Pages
Open your browser and visit:
```
http://localhost/
http://localhost/hello
http://localhost/welcome
```
You should see:

- `/hello` → Hello

- `/welcome` → Welcome

- `/` → Nginx is running. Use /hello or /welcome

### 7. Debugging Tips
- If you see errors like `conflicting server name "localhost"` → stop extra nginx processes.

- Use `.\nginx.exe -s` reload after config changes.

- Check logs: `logs/error.log` for detailed error messages. 

---

**Author**: Divyansh

**Date**: October 2025
