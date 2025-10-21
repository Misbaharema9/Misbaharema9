ZTE OLT Monitor System
A comprehensive web-based monitoring and management system for ZTE OLT devices (C300, C320, C600) built with modern web technologies.

Features
Core Functionality
OLT Management: Add, configure, and monitor ZTE OLT devices
ONU Management: Configure and manage ONUs with real-time monitoring
Real-time Monitoring: SNMP-based monitoring with live dashboard
Configuration Management: Backup and restore OLT configurations
Alert System: Intelligent alerting for signal quality and device status
Performance Analytics: Graphs and reports for system performance
User Management: Role-based access control (Admin, Operator, Viewer)
Technical Features
Multi-protocol Support: SNMP, SSH, and Telnet connectivity
Signal Quality Monitoring: Automatic classification (Good/Warning/Critical)
Device Auto-discovery: Automatic ONU detection and provisioning
Historical Data: Performance tracking and trend analysis
Responsive Design: Mobile-friendly interface
Dark/Light Theme: Modern UI with theme switching
Real-time Updates: WebSocket-based live updates
Architecture
Backend (FastAPI)
Framework: FastAPI with Python 3.11
Database: MySQL 8.0 with SQLAlchemy ORM
Caching: Redis for session management
Authentication: JWT-based authentication
Protocols: SNMP (pysnmp), SSH (paramiko), Telnet (telnetlib3)
Frontend (Vue.js)
Framework: Vue 3 with TypeScript
UI Library: Element Plus
Charts: ECharts for performance visualization
State Management: Pinia
Build Tool: Vite
Infrastructure
Containerization: Docker and Docker Compose
Reverse Proxy: Nginx
Database: MySQL 8.0
Cache: Redis
Quick Start
Prerequisites
Docker and Docker Compose
Git
Installation
1. Clone the repository
<pre>
git clone <repository-url>
cd olt-monitor-system
</pre>

2. Start the application
<pre>
docker-compose up -d
</pre>
3. Access the application
   Frontend: http://localhost
   API Documentation: http://localhost/api/docs
   Default Login: admin / admin123
   
Configuration
  Environment Variables
  Create a .env file in the backend directory:
<pre>
DATABASE_URL=mysql+mysqlconnector://olt_user:olt_password_123@mysql:3306/olt_monitor
REDIS_URL=redis://redis:6379
SECRET_KEY=your-secret-key-here-change-in-production
ALGORITHM=HS256
ACCESS_TOKEN_EXPIRE_MINUTES=30
</pre>

OLT Configuration

Add OLT devices through the web interface or API:
<pre>
{
  "name": "ZTE-C300-01",
  "ip_address": "192.168.1.100",
  "model": "C300",
  "version": "v2.1",
  "snmp_community": "public",
  "ssh_username": "admin",
  "ssh_password": "admin123"
}
</pre>

Usage

Adding OLT Devices

1. Navigate to OLT Management
2. Click "Add OLT"
3. Enter device details and credentials
4. Test connection to verify connectivity
5. Save the configuration

Monitoring ONUs

1. Select an OLT from the list
2. View discovered ONUs in the ONU tab
3. Configure ONU parameters (VLAN, bandwidth, etc.)
4. Monitor signal quality and performance

Performance Graphs

1. Navigate to Performance section
2. Select time range and metrics
3. View real-time and historical data
4. Export graphs for reports

Configuration Backup

1. Select OLT device
2. Click "Backup Configuration"
3. Enter backup name and description
4. Download backup file

API Documentation

Authentication
<pre>
# Login
POST /api/auth/login
{
  "username": "admin",
  "password": "admin123"
}
</pre>
OLT Management
<pre>
# Get all OLTs
GET /api/olt

# Add OLT
POST /api/olt
{
  "name": "ZTE-C300-01",
  "ip_address": "192.168.1.100",
  "model": "C300",
  "version": "v2.1"
}

# Monitor OLT
POST /api/olt/{id}/monitor
</pre>

ONU Management
<pre>
# Get ONUs
GET /api/onu?olt_id=1

# Configure ONU
POST /api/onu/{id}/configure
{
  "config": {
    "vlan_id": 100,
    "bandwidth_up": 100000,
    "bandwidth_down": 100000
  }
}
</pre>


Development

Backend Development
<pre>
cd backend
pip install -r requirements.txt
uvicorn main:app --reload
</pre>

Frontend Development
<pre>
cd frontend
npm install
npm run dev
</pre>
Database Migrations
<pre>
cd backend
alembic revision --autogenerate -m "Initial migration"
alembic upgrade head
</pre>

Supported OLT Models

ZTE C300

1. Version: v2.1, v2.2, v3.0
2. PON Types: GPON, EPON
3. Max PON Ports: 16
4. Max ONUs per PON: 128

ZTE C320

1. Version: v3.0, v3.1, v3.2
2. PON Types: GPON, XG-PON
3. Max PON Ports: 24
4. Max ONUs per PON: 256

ZTE C600

1. Version: v1.5, v2.0
2. PON Types: GPON, XGS-PON
3. Max PON Ports: 32
4. Max ONUs per PON: 512

Monitoring Metrics

OLT Metrics

1. CPU Usage
2. Memory Usage
3. Temperature
4. Uptime
5. Interface Statistics
6. Error Rates


ONU Metrics

1. RX/TX Power
2. Signal Quality
3. Traffic Statistics
4. Error Rates
5. Distance/OLT

Alert Types

Signal Quality Alerts

1. Low RX Power (< -27 dBm)
2. High RX Power (> -6 dBm)
3. Signal Loss

Device Status Alerts

1. OLT Offline
2. ONU Offline
3. High CPU Usage (> 80%)
4. High Memory Usage (> 80%)
5. High Temperature (> 70°C)

Security Features

Authentication

1. JWT-based authentication
2. Role-based access control
3. Session management
4. Password hashing

Network Security

1. HTTPS support
2. CORS configuration
3. Rate limiting
4. Input validation

Troubleshooting

Common Issues

OLT Connection Failed

1. Verify IP address and network connectivity
2. Check SNMP community string
3. Verify SSH/Telnet credentials
4. Check firewall settings

ONU Not Discovered

1. Ensure OLT is online
2. Check PON port status
3. Verify ONU is powered and connected
4. Check optical signal levels

High Memory Usage

1. Restart monitoring services
2. Check database connections
3. Review monitoring intervals
4. Scale resources if needed

Logs
<pre>
# Application logs
docker-compose logs -f backend

# Database logs
docker-compose logs -f mysql

# Nginx logs
docker-compose logs -f nginx
</pre>


Contributing
1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests if applicable
5. Submit a pull request

License
This project is licensed under the MIT License - see the LICENSE file for details.

Support
For support and questions:

Create an issue in the repository
Check the documentation
Review the troubleshooting section

Changelog
v1.0.0
Initial release
Basic OLT/ONU management
SNMP monitoring
Web interface
Configuration backup
Alert system
Performance graphs
