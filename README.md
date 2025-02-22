# UniFi Network Application Controller

This repository contains the Docker configuration for running a UniFi Network Application controller, which allows you to manage UniFi network devices.

## Quick Start

1. Clone this repository:
```bash
git clone https://github.com/banderson12/ubiquiti-local.git
cd ubiquiti-local
```

2. Start the controller:
```bash
docker-compose up -d
```

3. Access the controller:
   - URL: https://localhost:8443
   - Default credentials:
     - Username: `ubnt`
     - Password: `ubnt`

## SSL Certificate Warning

When accessing the controller for the first time, you'll see a certificate warning in your browser. This is normal as the controller uses a self-signed certificate.

To proceed:
1. Click "Advanced"
2. Click "Proceed to localhost (unsafe)"

## Ports Used

The controller uses the following ports:
- TCP 8443 - Main web interface
- TCP 8080 - Device communication
- TCP 8880 - HTTP portal redirect
- TCP 8843 - HTTPS portal redirect
- TCP 6789 - Speed test
- UDP 3478 - STUN
- UDP 10001 - Device discovery

## Connecting Devices

1. Access the controller at https://localhost:8443
2. Log in with the default credentials
3. Follow the setup wizard to:
   - Create a new admin account
   - Set up your site
   - Adopt UniFi devices

## Volume Mounts

The configuration persists in the `./unifi` directory, which contains:
- `data/` - UniFi configuration and database
- `log/` - Log files
- `cert/` - SSL certificates
- `run/` - Runtime data

## Environment Variables

The following environment variables are configured:
- `TZ`: Timezone (default: America/Denver)
- `RUNAS_UID0`: Run as root (required for host networking)
- `UNIFI_UID/GID`: User/Group IDs for UniFi processes

## Troubleshooting

1. If devices can't be discovered:
   - Ensure the controller is running
   - Check that all required ports are accessible
   - Verify network connectivity between devices and controller

2. If the web interface is inaccessible:
   - Wait a few minutes for initial startup
   - Check docker logs: `docker logs unifi-controller`
   - Ensure no other services are using port 8443

## Maintenance

- View logs: `docker logs unifi-controller`
- Restart controller: `docker-compose restart`
- Update image: 
  ```bash
  docker-compose pull
  docker-compose up -d
  ```

## License

This project is licensed under the MIT License - see the LICENSE file for details.
