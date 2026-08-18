# Smart Transit Tracker

> A real-time public transit tracking system featuring live GPS monitoring, geospatial analytics, and comprehensive fleet management capabilities.

[![Node.js](https://img.shields.io/badge/Node.js-339933?style=for-the-badge&logo=nodedotjs&logoColor=white)](https://nodejs.org/)
[![React](https://img.shields.io/badge/React-61DAFB?style=for-the-badge&logo=react&logoColor=black)](https://reactjs.org/)
[![MongoDB](https://img.shields.io/badge/MongoDB-4EA94B?style=for-the-badge&logo=mongodb&logoColor=white)](https://www.mongodb.com/atlas)
[![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=for-the-badge&logo=typescript&logoColor=white)](https://www.typescriptlang.org/)

## Overview

The Smart Transit Tracker is a full-stack application engineered to provide real-time tracking of Boston's public bus network utilizing the Massachusetts Bay Transportation Authority (MBTA) live API. The system continuously processes and visualizes data for over 100 buses, featuring live position updates, comprehensive analytics, and an interactive geospatial interface.

![Project Screenshot](client/src/assets/image-1.png)
![Project Screenshot](client/src/assets/image.png)
![Project Screenshot](client/src/assets/image2.png)
![Project Screenshot](client/src/assets/image3.png)

### Core Capabilities

*   **Real-Time Tracking:** Simultaneous monitoring of 100+ MBTA buses with 5-second interval updates.
*   **Time-Series Analytics:** MongoDB time-series collections for historical data aggregation and reporting.
*   **Geospatial Queries:** Advanced proximity searches supporting radius-based vehicle discovery.
*   **Live GTFS Integration:** Direct synchronization with the Boston MBTA public API.
*   **Interactive Visualization:** Mapbox-powered interface displaying route polylines and detailed stop information.

---

## Features

### Real-Time Tracking
*   Live GPS positions updated iteratively every 5 seconds.
*   Smooth, interpolated vehicle movement rendering on the map interface.
*   Current status indicators (On Time, Delayed, At Stop, Breakdown).
*   Live passenger occupancy levels.

### Fleet Analytics Dashboard
*   **Fleet Overview:** Real-time operational status breakdown and utilization metrics.
*   **Route Performance:** Analytics on speed trends, daily statistics, and stop efficiency.
*   **Geospatial Queries:** Radius-based location services for fleet discovery.
*   **Vehicle Heatmaps:** Visual representations of traffic density and congestion.
*   **Occupancy Analytics:** Passenger load distribution across active routes.
*   **Historical Reporting:** 30-day trend analysis for performance auditing.

### Interactive Map
*   Mapbox GL JS integration for high-performance geospatial rendering.
*   Route polylines displaying accurate turn-by-turn geometry.
*   Stop markers equipped with estimated arrival time calculations.
*   Click-to-track functionality for isolating individual vehicles.

---

## Technology Stack

### Frontend Application
| Technology | Purpose |
|------------|---------|
| **React 18** | UI architecture and state management |
| **TypeScript** | Static typing and enhanced developer tooling |
| **Vite** | Build tool and development server |
| **Tailwind CSS** | Utility-first styling framework |
| **shadcn/ui** | Accessible, customizable component library |
| **Mapbox GL JS** | High-performance interactive mapping |
| **Turf.js** | Client-side geospatial calculations |

### Backend Services
| Technology | Purpose |
|------------|---------|
| **Node.js** | Asynchronous runtime environment |
| **Express.js** | REST API framework and routing |
| **MongoDB Atlas** | Cloud database with native geo-indexing |
| **Mongoose** | Object Data Modeling (ODM) and schema validation |
| **Axios** | HTTP client for external GTFS feed ingestion |

---

## Getting Started

### Prerequisites
*   Node.js 18.x or higher
*   MongoDB Atlas account (Free tier supported)
*   Mapbox Access Token

### Installation

1.  **Clone the repository**
    ```bash
    git clone https://github.com/yourusername/smart-transit-tracker.git
    cd smart-transit-tracker
    ```

2.  **Backend Configuration**
    ```bash
    cd server
    npm install
    
    # Generate environment variables
    cat > .env << EOF
    PORT=5000
    ATLAS_URI=mongodb+srv://username:password@cluster.mongodb.net/bustrack
    MAPBOX_ACCESS_TOKEN=pk.your_mapbox_token
    SYNC_INTERVAL_MS=5000
    EOF
    
    # Initialize database schemas and indexes
    npm run seed
    
    # Initialize the development server
    npm run dev
    ```

3.  **Frontend Configuration**
    ```bash
    cd client
    npm install
    
    # Generate client environment variables
    echo "VITE_MAPBOX_TOKEN=pk.your_mapbox_token" > .env.local
    echo "VITE_API_URL=http://localhost:5000" >> .env.local
    
    # Initialize the development server
    npm run dev
    ```

4.  **Access the Application**
    Navigate to `http://localhost:5173` in your browser.

---

## Data Source Architecture

### Boston MBTA Live API
This application establishes a direct connection to the Massachusetts Bay Transportation Authority (MBTA) real-time transit feed to supply live telemetry data:

*   Simultaneous tracking of 100+ active vehicles.
*   Coordinates and metadata updated in 5-second intervals.
*   Comprehensive route data including vehicle identifiers, sequential stops, and directional vectors.
*   Live passenger occupancy metrics (where supported by MBTA hardware).
*   Public access infrastructure requiring no dedicated API key.

#### MBTA API Endpoints
*   Vehicle Positions: `https://api-v3.mbta.com/vehicles`
*   Routes: `https://api-v3.mbta.com/routes`
*   Stops: `https://api-v3.mbta.com/stops`

---

## System Architecture

### Real-Time Data Pipeline
```text
MBTA API ──5s poll──▶ Transit Service ──▶ Data Sync ──▶ MongoDB
                            │                               │
                            ▼                               ▼
                     Live Vehicles Cache             Vehicle History
                            │                      (7-day retention)
                            ▼
                     REST API ──▶ React Frontend ──▶ Mapbox GL
```

---

## Development Guidelines

### Testing Procedures
```bash
# Execute frontend test suite
cd client && npm test

# Execute backend test suite
cd server && npm test
```

### Production Build
```bash
# Compile frontend assets
cd client && npm run build

# Initialize production backend
cd server && npm start
```

### Code Quality Standards
```bash
# Execute ESLint
npm run lint

# Validate TypeScript compilation
npm run type-check
```

---

## Deployment Strategy

### Frontend Deployment (Vercel/Netlify)
Execute the build script and deploy the `dist` directory:
```bash
npm run build
```

### Backend Deployment (Railway/Render)
Configure the required environment variables in your hosting provider and initialize via:
```bash
npm start
```

### Database Administration (MongoDB Atlas)
Ensure your production `MONGODB_URI` environment variable is securely configured in your backend deployment environment.

---

## Contributing

1.  Fork the repository.
2.  Create a dedicated feature branch: `git checkout -b feature/issue-description`
3.  Commit your modifications: `git commit -m 'Implement specific feature'`
4.  Push to the branch: `git push origin feature/issue-description`
5.  Submit a Pull Request for review.

---

## License

This project is distributed under the MIT License. Reference the `LICENSE` file for full documentation and permissions.

---

## Project Highlights

### Technical Achievements
*   Implemented seamless real-time integration with the Boston MBTA GTFS-RT feed.
*   Engineered a data pipeline capable of tracking 100+ concurrent vehicles with sub-100ms API response times.
*   Designed complex MongoDB aggregation pipelines to process and deliver fleet analytics.
*   Integrated geospatial querying to facilitate advanced location-based services.
*   Developed a responsive React UI optimized for complex interactive Mapbox visualizations.

### Solution Impact
*   **For Passengers:** Provides accurate arrival telemetry to optimize journey planning.
*   **For Operators:** Delivers a centralized dashboard for real-time fleet performance monitoring.
*   **For Developers:** Establishes a clean, extensible architectural pattern adaptable to any GTFS-compliant transit system.
