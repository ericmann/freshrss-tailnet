# FreshRSS on Tailscale

This project provides a Docker Compose setup for running [FreshRSS](https://freshrss.org/), a free, self-hostable RSS feed aggregator.

As the name indicnates, you can run your own FreshRSS instance and make it securely accessible over your [Tailscale](https://tailscale.com/) network. This allows you to access your feeds from anywhere without exposing the FreshRSS instance directly to the public internet.

## Overview

The `docker-compose.yml` file defines three services:

1.  `tailscale`: Runs the Tailscale daemon, connecting the container environment to your tailnet and handling HTTPS termination.
2.  `freshrss`: The main FreshRSS application container. It uses the `tailscale` service's network.
3.  `postgres`: A PostgreSQL database container used by FreshRSS for storing data. It also uses the `tailscale` service's network.

Persistent data for Tailscale state, FreshRSS, and PostgreSQL is stored in the `./data` directory on the host machine.

The `ts-serve.json` file configures the `tailscale` service to expose FreshRSS securely over HTTPS using your Tailscale domain name.

## Prerequisites

*   Docker and Docker Compose installed.
*   A Tailscale account and tailnet configured.
*   A Tailscale auth key (`TS_AUTHKEY`) - ideally an ephemeral, reusable, tagged key.
*   A registered domain name configured for Tailscale HTTPS certificates (`TS_CERT_DOMAIN`).

## Getting Started

1.  **Clone the repository:**
    ```bash
    git clone <repository-url>
    cd freshrss-tailnet
    ```
2.  **Configure environment variables:** Copy `.env.example` to `.env` and define the necessary variables. Pay close attention to:
    *   `TAILNET_NAME`: A hostname for the services within your tailnet.
    *   `TS_AUTHKEY`: Your Tailscale auth key.
    *   `TS_CERT_DOMAIN`: The domain Tailscale should use for HTTPS (e.g., `freshrss.your-domain.ts.net`).
    *   Database credentials, admin user details, and `BASE_URL` (which should likely match `https://${TS_CERT_DOMAIN}`).
3.  **Start the services:**
    ```bash
    docker-compose up -d
    ```
4.  **Access FreshRSS:**
    *   Once the Tailscale container authenticates and configures itself, you can access FreshRSS securely via `https://${TS_CERT_DOMAIN}` from any device connected to your tailnet.
    *   Check the Tailscale admin console to ensure the device (`TAILNET_NAME`) is connected and the service is recognized.

## Contributing

Contributions are welcome! Please feel free to open an issue or submit a pull request.

## License

This project is licensed under the [MIT License](LICENSE).