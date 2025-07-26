# NextStep-DevOps

Fast (and naive) deployment on local machine & exposure via kubernetes HTTPRoute.

## Prerequisites

- npm and node.js.

- Kubernetes With Gateway API.

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

1. Setup the kubernetes

   ```
   kubectl apply -k kubernetes
   ```

## Usage

- The nextstep frontend application will be exposed to the world in http://nextstep.theworkpc.com:1785

- The nextstep backend application will be exposed to the world in http://backend.nextstep.theworkpc.com:1785
