# NextStep-DevOps

Deployment on local machine & exposure via NGINX.

## Prerequisites

- npm and node.js.

- Nginx server enabled

## Installation

Clone the repository.

1. Setup local deployment via sytemd files:

   Edit the [linux](/linux) services to your environment (i.e. user name, npm path).

   Install the services:

   ```
   sudo cp linux/nextstep-frontend.service /etc/systemd/system/
   sudo cp linux/nextstep-backend.service /etc/systemd/system/
   
   sudo systemctl daemon-reload
   
   sudo systemctl enable --now nextstep-frontend.service
   sudo systemctl enable --now nextstep-backend.service
   ```

1. Setup nginx configuration

   ```
   sudo cp nginx/nginx.conf /etc/nginx/nginx.conf
   sudo systemctl restart nginx
   ```

## Usage

- The nextstep frontend application will be exposed to the world in http://nextstep.theworkpc.com:1785

- The nextstep backend application will be exposed to the world in http://backend.nextstep.theworkpc.com:1785
