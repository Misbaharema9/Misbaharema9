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
'''Clone the repository
bash

Line Wrapping

Collapse

  git clone <repository-url>
  cd olt-monitor-system
  Start the application
  bash

Line Wrapping

Collapse
Copy
1
docker-compose up -d
Access the application
Frontend: http://localhost
API Documentation: http://localhost/api/docs
Default Login: admin / admin123
Configuration
Environment Variables
Create a .env file in the backend directory:

env

Line Wrapping

'''Collapse
DATABASE_URL=mysql+mysqlconnector://olt_user:olt_password_123@mysql:3306/olt_monitor
REDIS_URL=redis://redis:6379
SECRET_KEY=your-secret-key-here-change-in-production
ALGORITHM=HS256
ACCESS_TOKEN_EXPIRE_MINUTES=30
OLT Configuration
Add OLT devices through the web interface or API:

json

Line Wrapping

'''Collapse
{
  "name": "ZTE-C300-01",
  "ip_address": "192.168.1.100",
  "model": "C300",
  "version": "v2.1",
  "snmp_community": "public",
  "ssh_username": "admin",
  "ssh_password": "admin123"
}

Usage
Adding OLT Devices
Navigate to OLT Management
Click "Add OLT"
Enter device details and credentials
Test connection to verify connectivity
Save the configuration
Monitoring ONUs
Select an OLT from the list
View discovered ONUs in the ONU tab
Configure ONU parameters (VLAN, bandwidth, etc.)
Monitor signal quality and performance
Performance Graphs
Navigate to Performance section
Select time range and metrics
View real-time and historical data
Export graphs for reports
Configuration Backup
Select OLT device
Click "Backup Configuration"
Enter backup name and description
Download backup file
API Documentation
Authentication
bash

Line Wrapping

'''Collapse
POST /api/auth/login
{
  "username": "admin",
  "password": "admin123"
}
OLT Management
bash

Line Wrapping

Collapse
Copy
1
2
3
4
5
6
7
8
9
10
11
12
13
14
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
ONU Management
bash

Line Wrapping

Collapse
Copy
1
2
3
4
5
6
7
8
9
10
11
12
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
Development
Backend Development
bash

Line Wrapping

Collapse
Copy
1
2
3
cd backend
pip install -r requirements.txt
uvicorn main:app --reload
Frontend Development
bash

Line Wrapping

Collapse
Copy
1
2
3
cd frontend
npm install
npm run dev
Database Migrations
bash

Line Wrapping

Collapse
Copy
1
2
3
cd backend
alembic revision --autogenerate -m "Initial migration"
alembic upgrade head
Supported OLT Models
ZTE C300
Version: v2.1, v2.2, v3.0
PON Types: GPON, EPON
Max PON Ports: 16
Max ONUs per PON: 128
ZTE C320
Version: v3.0, v3.1, v3.2
PON Types: GPON, XG-PON
Max PON Ports: 24
Max ONUs per PON: 256
ZTE C600
Version: v1.5, v2.0
PON Types: GPON, XGS-PON
Max PON Ports: 32
Max ONUs per PON: 512
Monitoring Metrics
OLT Metrics
CPU Usage
Memory Usage
Temperature
Uptime
Interface Statistics
Error Rates
ONU Metrics
RX/TX Power
Signal Quality
Traffic Statistics
Error Rates
Distance/OLT
Alert Types
Signal Quality Alerts
Low RX Power (< -27 dBm)
High RX Power (> -6 dBm)
Signal Loss
Device Status Alerts
OLT Offline
ONU Offline
High CPU Usage (> 80%)
High Memory Usage (> 80%)
High Temperature (> 70°C)
Security Features
Authentication
JWT-based authentication
Role-based access control
Session management
Password hashing
Network Security
HTTPS support
CORS configuration
Rate limiting
Input validation
Troubleshooting
Common Issues
OLT Connection Failed
Verify IP address and network connectivity
Check SNMP community string
Verify SSH/Telnet credentials
Check firewall settings
ONU Not Discovered
Ensure OLT is online
Check PON port status
Verify ONU is powered and connected
Check optical signal levels
High Memory Usage
Restart monitoring services
Check database connections
Review monitoring intervals
Scale resources if needed
Logs
bash

Line Wrapping

Collapse
Copy
1
2
3
4
5
6
7
8
# Application logs
docker-compose logs -f backend

# Database logs
docker-compose logs -f mysql

# Nginx logs
docker-compose logs -f nginx
Contributing
Fork the repository
Create a feature branch
Make your changes
Add tests if applicable
Submit a pull request
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
