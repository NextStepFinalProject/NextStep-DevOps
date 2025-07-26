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

1. Clone the NextStep Repository:

   ```
   git clone git@github.com:NextStepFinalProject/NextStep.git
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

1. Clone this repository:

   ```
   git clone git@github.com:NextStepFinalProject/NextStep-DevOps.git
   ```

1. Setup local deployment via sytemd files:

   Edit the [linux](/linux) services to your environment (i.e. user name, npm path, working directory).

   Then, install the services:

   ```
   sudo cp linux/nextstep-frontend.service /etc/systemd/system/
   sudo cp linux/nextstep-backend.service /etc/systemd/system/
   
   sudo systemctl daemon-reload
   
   sudo systemctl enable --now nextstep-frontend.service
   sudo systemctl enable --now nextstep-backend.service
   ```

1. Setup nginx configuration:

   ```
   sudo cp nginx/nginx.conf /etc/nginx/nginx.conf
   sudo systemctl restart nginx
   ```

## Usage

- The nextstep frontend application will be exposed to the world in http://nextstep.theworkpc.com:1785

- The nextstep backend application will be exposed to the world in http://backend.nextstep.theworkpc.com:1785
