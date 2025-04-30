# FreshRSS on Tailscale

This project provides a Docker Compose setup for running [FreshRSS](https://freshrss.org/), a free, self-hostable RSS feed aggregator.

As the name indicnates, you can run your own FreshRSS instance and make it securely accessible over your [Tailscale](https://tailscale.com/) network. This allows you to access your feeds from anywhere without exposing the FreshRSS instance directly to the public internet.

## Overview

The `docker-compose.yml` file defines two services:

1.  `freshrss`: The main FreshRSS application container.
2.  `postgres`: A PostgreSQL database container used by FreshRSS for storing data.

Persistent data for both FreshRSS and PostgreSQL is stored in the `./data` directory on the host machine.

## Prerequisites

*   Docker and Docker Compose installed.
*   A Tailscale account and tailnet configured (if you intend to use it for access).

## Getting Started

1.  **Clone the repository:**
    ```bash
    git clone <repository-url>
    cd freshrss-tailnet
    ```
2.  **Configure environment variables:** Copy `.env.example` to `.env` and define the necessary variables (see `docker-compose.yml` for required variables like database credentials, admin user details, and `BASE_URL`).
3.  **Start the services:**
    ```bash
    docker-compose up -d
    ```
4.  **Access FreshRSS:**
    *   Initially, you can access FreshRSS locally via `http://localhost:8040` (or the port you configure).

## Contributing

Contributions are welcome! Please feel free to open an issue or submit a pull request.

## License

This project is licensed under the [MIT License](LICENSE).