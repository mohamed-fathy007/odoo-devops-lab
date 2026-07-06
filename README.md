# Odoo Custom Deployment Pipeline 🚀

This repository contains a fully automated CI/CD pipeline for building, testing, and deploying a customized Odoo 17 instance via Docker.

## 🌟 Features
- **Automated CI/CD:** Powered by GitHub Actions to build and push the production-ready Docker image.
- **Automated Smoke Testing:** GitHub Actions automatically tests the built image using Docker Compose to ensure application stability before push.
- **Custom Addons:** All custom modules are built directly into the immutable Docker image.

## 🛠️ Infrastructure Architecture
- **App Layer:** Custom Odoo 17 Image (`01013576608/odoo-custom:latest`)
- **Database Layer:** PostgreSQL 15

---

## 🚀 How to Run the Production Image (Fast Track)

You **don't need** the source code or the Dockerfile to run this project. Anyone can pull and spin up the complete environment using our production compose file.

### Prerequisites
- Docker and Docker Compose installed.

### Step 1: Download the production compose file
Create a file named `docker-compose.prod.yml` and paste the configuration below:

```yaml
services:
  web:
    image: 01013576608/odoo-custom:latest
    depends_on:
      - db
    ports:
      - "8069:8069"
    volumes:
      - odoo-web-data:/var/lib/odoo
    environment:
      - HOST=db
      - USER=odoo
      - PASSWORD=odoo_password

  db:
    image: postgres:15
    environment:
      - POSTGRES_DB=postgres
      - POSTGRES_PASSWORD=odoo_password
      - POSTGRES_USER=odoo
    volumes:
      - odoo-db-data:/var/lib/postgresql/data

volumes:
  odoo-web-data:
  odoo-db-data:

networks:
  default:
    name: odoo-network
