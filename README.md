# IIT
Brief Overview of the Project
This project implements and simulates dynamic pricing models for parking lots based on real-world features such as occupancy, queue length, traffic conditions, special days, vehicle types, and competition.

The objective is to adjust parking prices over time to better match demand, improve revenue, and manage congestion.

It compares three pricing models:

Model 1: Simple occupancy-based price adjustment

Model 2: Demand-model-based dynamic pricing

Model 3: Competition-aware pricing that considers nearby lots

Tech Stacks Used
Language: Python

Data Science Libraries:

pandas

numpy

matplotlib

geopy

Environment: Google Colab / Jupyter Notebook

Data Source: CSV file with parking lot data


Architecture Diagram (Mermaid)
Below is a Mermaid diagram you can copy into Mermaid Live Editor to visualize:

mermaid
Copy
Edit
flowchart TD
    A[Dataset (CSV)] --> B[Data Loading & Preprocessing]
    B --> C[Feature Engineering]
    C --> D[Distance Matrix Computation]
    D --> E[Demand Calculation]
    E --> F[Price Update Loop Over Time Steps]
    F --> G[Model 1: Occupancy-Based Pricing]
    F --> H[Model 2: Demand-Based Pricing]
    F --> I[Model 3: Competitive Pricing]
    G --> J[Price History Storage]
    H --> J
    I --> J
    J --> K[Visualization: Matplotlib Plot]
    Detailed Explanation of Project Architecture and Workflow
Here’s a detailed breakdown of how your code works, structured into stages:

1️⃣ Data Loading and Preprocessing
CSV is loaded using pandas.

The 'LastUpdatedDate' and 'LastUpdatedTime' columns are combined into a single datetime column (Time).

Categorical features like TrafficConditionNearby and VehicleType are mapped to numerical weights.

2️⃣ Feature Engineering
Adds features like VehicleTypeWeight for modeling demand.

Special day flag (IsSpecialDay) is included as an influence on demand.

3️⃣ Distance Matrix Computation
Uses geopy to calculate pairwise distances between parking lots.

Builds a matrix of distances to identify "competitors" (other lots within 500m).

4️⃣ Demand Calculation
Computes demand using a custom formula:

Occupancy ratio

Queue length

Traffic conditions

Special day flag

Vehicle type weight

Demand is normalized across lots at each time step to ensure consistent scaling.

5️⃣ Pricing Models
For every time step, and for every parking lot:

✅ Model 1
Simple linear adjustment based on occupancy:

ini
Copy
Edit
new_price = prev_price + alpha * (occupancy / capacity)
✅ Model 2
Demand-based dynamic pricing:

ini
Copy
Edit
new_price = base_price * (1 + λ * normalized_demand)
λ controls sensitivity to demand.

✅ Model 3
Competition-aware pricing:

Starts with Model 2 price.

Adjusts up or down based on nearby competitor prices:

Reduces price if occupancy is full and competition is cheaper.

Increases price if there's spare capacity and competition is expensive.

6️⃣ Price History Storage
Prices for each model are tracked over time steps for every lot.

Three separate dictionaries maintain the price history:

price_history_model1

price_history_model2

price_history_model3

7️⃣ Visualization
Uses matplotlib to plot time series of price evolution for all parking lots across all models.

Different linestyles for easy comparison:

Model 1: dashed

Model 2: solid

Model 3: dotted
