# SwiftRoute Logistics: Urban Fleet Routing & Delivery Performance Analysis

An executive-level operational analysis evaluating food delivery bottlenecks, route inefficiencies, and fleet dispatch allocation for SwiftRoute Logistics.

---

## 1. Executive Summary & Problem Statement
SwiftRoute Logistics experienced severe service-level agreement (SLA) breaches, with 45.5% of total deliveries exceeding 50 minutes. Operational leadership initially attributed these delays to adverse weather conditions and peak urban traffic congestion. 

This analysis interrogates route topology, vehicle dispatching rules, and external environmental factors across 200 delivery runs to isolate the true operational bottlenecks and deliver data-driven corrective strategies.

---

## 2. Key Metrics & Dataset Exploration
The dataset was processed and modeled in Power BI using Power Query and custom DAX measures:
* Total Volume Analyzed: 200 orders across 5 geographic zones (Central, East, North, South, West).
* Average Delivery Duration: 44.7 minutes (Target SLA: $\le 35$ minutes).
* Average Fleet Transit Speed: 11.3 km/h across all vehicle classes.
* Average Detour Overhead: +23.1% excess transit distance compared to direct straight-line distance.
* SLA Performance Breakdown:
  * On-Time ($\le 35$ mins): 40.5%
  * Moderate Delay (36–50 mins): 14.0%
  * Severe Breach (> 50 mins): 45.5%

---

## 3. Key Findings & Diagnostic Insights

### Finding 1: The "Distance Cliff" and Detour Compounding
* Delivery durations scale non-linearly once trips exceed 6 km. 
* While trips under 3 km maintain strong SLA adherence, long trips suffer an average of +23.1% detour overhead due to circuitous urban routing. 
* On high-friction inter-zone corridors (such as North $\rightarrow$ South), deliveries stretched up to 67 minutes, demonstrating that spatial friction is the primary driver of extended delays.

### Finding 2: Fleet Velocity Parity (Debunking the Weather Myth)
* Fleet transit speeds remain virtually flat at ~11.3 km/h across Clear, Cloudy, Rainy, and Windy conditions.
* Courier velocity also showed minimal variance between Low, Medium, and High traffic tiers, proving that weather and traffic density are secondary symptoms rather than the root causes of systemic delays.

### Finding 3: Dispatch Misallocation on Long Corridors
* Low-speed delivery modes (primarily bicycles) were consistently assigned to delivery routes exceeding 9 km.
* Given an average velocity of ~11.3 km/h, assigning a bicycle to a 9 km trip requires over 47 minutes in transit time alone—mathematically guaranteeing an SLA failure before order preparation and handoff are even accounted for.

---

## 4. Strategic Recommendations

1. Implement Vehicle-to-Distance Dispatch Geofencing:
   * Restrict Bicycles strictly to micro-deliveries under 3 km.
   * Assign Scooters and Motorbikes to mid-range trips (3–6 km).
   * Reserve Motorbikes and Cars exclusively for long-distance trips (> 6 km).
2. Re-route High-Friction Corridors:
   * Recalibrate waypoint routing logic on the top detour corridors to reduce the +23.1% excess mileage penalty.
3. Establish Tiered SLA Windows:
   * Transition from a flat 35-minute promise to distance-calibrated SLAs (<3 km: 30 mins; 3–6 km: 40 mins; >6 km: 55–60 mins) to protect customer trust and reduce cancellation costs.

---

## 5. Dashboard Architecture
The accompanying Power BI report is structured as an interactive 2-page executive suite:
* Page 1: Route Efficiency: Focuses on spatial corridor friction, distance tiers, detour overhead %, and hourly order flows.
* Page 2: Fleet Operations: Evaluates vehicle transit velocity, traffic parity, weather impacts, and mode-to-distance dispatch distribution.

Tools Used: Power BI Desktop | DAX | Power Query ETL
