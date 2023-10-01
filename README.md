# Stallprofi borjúnevelő konfigurátor üzemeltetési dokumentáció


A `helm` mappában találhatóak az általam használt helm chart-ok a telepítéshez.

## Frontend

Docker image link

```
https://hub.docker.com/r/kosbalint/fe-calfraiser
```

#### Environment variables

```
REACT_APP_BACKEND_URL #The url where the backend is hosted
```


---


## Backend

Docker image link

```
https://hub.docker.com/r/kosbalint/be-calfraiser
```


#### Environment variables

```
  NODE_ENV = "production"
  EMAIL_SENDER_NAME = "Borjú nevelő konfigurátor"
  EMAIL_HOST = "[host of the email server]"
  EMAIL_PORT = "[port of the email server]"
  EMAIL_SECURE = "true"
  EMAIL_AUTH_USER = "[email address of the sender]"
  EMAIL_AUTH_PASS = "[password of the sender]"
  ADMIN_EMAIL = "[email address of the admin, this is where the admin notifications will be sent]"
  FTP_HOST = "[host of the ftp server]"
  FTP_PORT = "21"
  FTP_USER = "[username on the ftp server]"
  FTP_PASSWORD = "[password on the ftp server]"
  FTP_SECURE = "true"
  FTP_REJECT_UNAUTHORIZED = "false" #Needed for self signed certificates
  FTP_EXCEL_PATH = "export.xlsx" #The path where the excel file will be located on the ftp server
```
