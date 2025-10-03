# Rustfs with Docker Compose

[![Docker](https://img.shields.io/badge/Docker-✔-2496ED?logo=docker&logoColor=white)](https://www.docker.com/) [![Rust](https://img.shields.io/badge/RustFS-Rust-888888?logo=rust&logoColor=white)](https://github.com/rustfs/rustfs)

RustFS is a high-performance distributed object storage software built in Rust.  
It claims to be fast, provides comprehensive S3 support, and includes a powerful console.  

This setup is intended for **development purposes only**, not for production.

---
## Purpose

I need an S3-compatible storage solution for development, but MinIO’s licensing is restrictive for my use case.  
After some research, I found RustFS. It is written in Rust, looks very promising, and provides the S3 compatibility I need.  

Although RustFS is still under rapid development and not recommended for production, this does not affect me since I only use it for development.  

---

## Prerequisites

- A VPS with Linux (tested on Ubuntu & Arch Linux)  
- Docker and Docker Compose installed  
- A reverse proxy already set up using a Docker network 
---

## Installation & Usage

1. Clone this repository:
   ```bash
   git clone https://github.com/wolewd/rustfs.git
   cd rustfs
   ```

2. Create an `.env` file:
   ```bash
   touch .env
   ```

3. Copy this inside `.env` and change `RUSTFS_PORT`, `RUSTFS_ACCESS_KEY` and `RUSTFS_SECRET_KEY` to you own values:
   ```env
   RUSTFS_PORT=9000
   RUSTFS_ACCESS_KEY=your-username
   RUSTFS_SECRET_KEY=your-password
   RUSTFS_ADDRESS=0.0.0.0:${RUSTFS_PORT}
   RUSTFS_API_BASE_URL=http://rustfs:${RUSTFS_PORT}
   ```
   Refer to the provided [.env.example](https://github.com/wolewd/rustfs/blob/main/.env.example).

4. Start the container:
   ```bash
   docker compose up -d
   ```

5. After the container is running, add the RustFS service into your reverse proxy.
   
   Example using Caddy:
   ```caddy
   rustfs.example.com {
      reverse_proxy rustfs:9000
   }
   ``` 
---
