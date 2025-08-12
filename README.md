# NextStep-DevOps

Deployment on local machine & exposure via NGINX.

In this guide we use [Rocky Linux](https://rockylinux.org/) (similar as Red Hat Enterprise Linux).

## Prerequisites

- [npm and node.js](https://nodejs.org/).

- [NGINX](https://nginx.org/) server enabled:

  ```
  sudo dnf install -y nginx
  sudo systemctl enable --now nginx
  ```

## Installation

**Disclaimer:** In this guide, we assume that the current user name is `tal`.

1. Clone the NextStep Repository:

   ```
   git clone git@github.com:NextStepFinalProject/NextStep.git && cd NextStep
   ```

   **Edit the `nextstep-backend/.env`, and `nextstep-frontend/.env` files:**

   In the `nextstep-backend/.env`, setup:

   ```
   FRONTEND_URL=http://nextstep.theworkpc.com:1785
   ```

   In the `nextstep-frontend/.env`, setup:

   ```
   VITE_DOMAIN_NAME=0.0.0.0
   VITE_ALLOWED_HOSTS=nextstep.theworkpc.com
   ```

1. Setup build of frontend:

   ```
   cd nextstep-frontend
   npm i
   npm run build
   ```

   Done. Step out from the NextStep directory:

   ```
   cd ../..
   ```

1. Clone this repository:

   ```
   git clone git@github.com:NextStepFinalProject/NextStep-DevOps.git && NextStep-DevOps
   ```

1. Setup local deployment via systemd files:

   Edit the [linux backend service](/linux/nextstep-backend.service) to your environment (i.e. user name, npm path, working directory).

   Then, install the backend service:

   ```
   sudo cp linux/nextstep-backend.service /etc/systemd/system/
   
   sudo systemctl daemon-reload
   
   sudo systemctl enable --now nextstep-backend.service
   ```
   
1. Setup nginx configuration:

   Edit the [nginx.conf](/nginx/nginx.conf) file to your environment (i.e. user name, build files path).

   Then, add the `nginx` user to the `tal` group:

   ```
   sudo usermod -a -G tal nginx
   ```

   Give execute permissions to `tal` group:

   ```
   chmod g+x /home/tal
   chmod g+x /home/tal/Code
   chmod g+x /home/tal/Code/NextStep
   chmod g+x /home/tal/Code/NextStep/nextstep-frontend
   chmod -R g+rx /home/tal/Code/NextStep/nextstep-frontend/dist
   ```

   Confirm `nginx` is in the `tal` group:

   ```
   id nginx
   ```

   Test that the `index.html` file can be accesses by the `nginx` user:

   ```
   sudo -u nginx cat /home/tal/Code/NextStep/nextstep-frontend/dist/index.html
   ```

   Apply the configuration, and restart nginx:

   ```
   sudo cp nginx/nginx.conf /etc/nginx/nginx.conf
   sudo systemctl restart nginx
   ```

## Usage

- The nextstep frontend application will be exposed to the world in http://nextstep.theworkpc.com:1785

- The nextstep backend application will be exposed to the world in http://backend.nextstep.theworkpc.com:1785
