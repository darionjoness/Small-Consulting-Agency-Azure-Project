# Architecture

This folder contains architecture diagrams and design documentation for the Azure AZ-104 Capstone Project.

## Diagrams to Include

- [ ] High-level architecture diagram
- [ ] Network topology diagram
- [ ] Data flow diagram
- [ ] Security architecture diagram

## Tools for Creating Diagrams

- [Draw.io](https://draw.io)
- [Azure Architecture Icons](https://docs.microsoft.com/en-us/azure/architecture/icons/)
- [Lucidchart](https://www.lucidchart.com)

## Architecture Overview

```
┌─────────────────────────────────────────────────────────────┐
│                      Azure Subscription                      │
├─────────────────────────────────────────────────────────────┤
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐          │
│  │   Web Tier  │  │  App Tier   │  │  Data Tier  │          │
│  │ App Service │  │ Function App│  │  Storage    │          │
│  │ + App GW    │  │             │  │ (Private EP)│          │
│  └─────────────┘  └─────────────┘  └─────────────┘          │
│                                                              │
│  ┌─────────────────────────────────────────────────────┐    │
│  │              Virtual Network (Hub-Spoke)             │    │
│  │   - Web Subnet    - App Subnet    - Data Subnet     │    │
│  │   - NSGs          - Route Tables  - Private DNS     │    │
│  └─────────────────────────────────────────────────────┘    │
│                                                              │
│  ┌─────────────────────────────────────────────────────┐    │
│  │                    Monitoring                        │    │
│  │   Log Analytics  -  Alerts  -  Dashboard            │    │
│  └─────────────────────────────────────────────────────┘    │
└─────────────────────────────────────────────────────────────┘
```

## Skills Demonstrated

- Solution Architecture Design
- Azure Well-Architected Framework
- Documentation Best Practices