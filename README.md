# grafana-monitoring

# Grafana Monitoring Stack

A comprehensive monitoring solution using Grafana, Prometheus, and Loki that provides system metrics, container monitoring, and log aggregation capabilities out of the box.

## Overview

This project sets up a complete monitoring stack with:
- **Grafana**: Visualization and dashboarding
- **Prometheus**: Metrics collection and storage
- **Loki**: Log aggregation
- **Promtail**: Log collection agent
- Pre-configured dashboards and data sources
- Automatic provisioning

## Prerequisites

- Docker
- Docker Compose
- At least 4GB of RAM available
- Port 3000, 9090, and 3100 available on your host

## Quick Start

1. Clone the repository:
```bash
git clone https://github.com/yourusername/grafana-monitoring.git
cd grafana-monitoring
```

2. Start the stack:
```bash
docker-compose up -d
```

3. Access Grafana:
   - URL: http://localhost:3000
   - Username: admin
   - Password: admin

## Project Structure

```
.
├── docker-compose.yml      # Docker services configuration
├── prometheus.yml         # Prometheus scraping configuration
├── promtail.yml          # Log collection configuration
├── datasources.yml       # Grafana datasources configuration
├── dashboards.yml        # Grafana dashboard provider configuration
└── dashboards/           # Pre-configured Grafana dashboards
    └── system_overview.json
```

## Available Metrics & Logs

### System Metrics
- CPU usage (overall and per core)
- Memory usage and allocation
- Disk I/O and usage
- Network traffic and errors

### Container Metrics
- Container CPU usage
- Container memory usage
- Container network stats

### Logs
- System logs
- Application logs
- Error rate monitoring

## Default Ports

| Service    | Port  | Purpose                    |
|------------|-------|----------------------------|
| Grafana    | 3000  | Web interface             |
| Prometheus | 9090  | Metrics database          |
| Loki       | 3100  | Log aggregation           |

## Configuration

### Adding New Dashboards

Place your dashboard JSON files in the `dashboards/` directory. They will be automatically loaded into Grafana on startup.

### Modifying Data Sources

Edit `datasources.yml` to add or modify data sources. The current setup includes:
- Prometheus (default)
- Loki

### Updating Prometheus Scrape Targets

Edit `prometheus.yml` to add new scrape targets or modify existing ones.

## Maintenance

### Backup

Volume data is stored in Docker volumes. Back them up regularly:
```bash
docker run --rm -v grafana-monitoring_grafana-storage:/source:ro -v $(pwd):/backup alpine tar czf /backup/grafana-backup.tar.gz -C /source ./
```

### Scaling

The stack can be scaled by:
1. Increasing Docker resource limits
2. Adjusting Prometheus retention settings
3. Configuring Loki retention policies

## Troubleshooting

Common issues and solutions:

1. **Grafana Not Loading**
   - Check if all containers are running: `docker-compose ps`
   - Verify port 3000 is not in use: `netstat -tulpn | grep 3000`

2. **No Metrics Data**
   - Verify Prometheus is running: `docker-compose logs prometheus`
   - Check Prometheus targets: http://localhost:9090/targets

3. **No Logs in Loki**
   - Check Promtail configuration
   - Verify log paths exist
   - Check Promtail logs: `docker-compose logs promtail`

## Contributing

1. Fork the repository
2. Create your feature branch
3. Commit your changes
4. Push to the branch
5. Create a new Pull Request

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Security

- Default credentials should be changed in production
- Exposed ports should be properly firewalled
- Regular security updates should be applied to all components

## Support

For issues and feature requests, please create an issue in the GitHub repository.
