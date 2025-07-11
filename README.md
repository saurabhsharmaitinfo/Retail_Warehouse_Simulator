# Retail Warehouse Simulation

## Overview
This project simulates a retail company warehouse using **SimPy**, a Python library for discrete-event simulation. The warehouse receives orders randomly (~every 5 minutes), processed by 3 workers, with each order consuming 1–5 items from an inventory of 1000 items. If inventory drops below 100 items, a restock of 500 items occurs after a 10-minute delay. The simulation runs for 480 minutes (8 hours) and tracks order processing times (time from arrival to processing start), queue lengths (orders waiting), and inventory levels.

Designed for **Google Colab**, the code uses `simpy`, `numpy`, and `matplotlib` to produce console logs, statistics, and visualizations. It includes robust error handling, synchronized data collection, and safeguards to prevent issues like array mismatches or syntax errors (e.g., `SyntaxError` for global declarations).

## Features
- Simulates order arrivals, processing, and inventory management with 3 workers.
- Tracks processing times, queue lengths, and inventory levels.
- Computes statistics (average/max processing time, average queue length, average inventory).
- Visualizes results with two `matplotlib` plots:
  - Processing times vs. arrival times.
  - Queue lengths and inventory levels vs. arrival times.
- Outputs data for Chart.js visualization.
- Robust error handling, parameter validation, and reproducible results (random seed).

## Prerequisites
- **Google Colab**: Run in a Colab notebook.
- **Python Libraries**:
  - `simpy`: For simulation.
  - `numpy`: For statistical analysis.
  - `matplotlib`: For plotting.
- No local setup required (libraries installed in Colab).

## Setup Instructions
1. Open [Google Colab](https://colab.research.google.com/) and create a new notebook (`File > New Notebook`).
2. Copy the simulation code into a single code cell.
3. Run the cell (`Shift + Enter`) to install `simpy` and execute the simulation.
4. Save to Google Drive (`File > Save`) or download as `.ipynb` (`File > Download > Download .ipynb`).

## Usage
1. **Run the Simulation**:
   - Execute the code cell in Colab.
   - Check console output for order events (e.g., arrivals, processing, restocks), statistics, and array lengths.
2. **View Plots**:
   - Two `matplotlib` plots:
     - Top: Processing times vs. arrival times (blue line with markers).
     - Bottom: Queue lengths (red) and inventory levels (green) vs. arrival times.
3. **Chart.js Visualization**:
   - Copy `Timestamps` and `Processing Times` from the console output for a custom Chart.js chart.
4. **Modify Parameters**:
   - Adjust `NUM_WORKERS`, `ARRIVAL_RATE`, `RESTOCK_THRESHOLD`, or `INITIAL_INVENTORY` to test scenarios (e.g., high demand, low inventory).
   - Rerun the cell for updated results.

## Example Output
- **Console**:
  ```
  Order0 arrived at 3.45, waited 0.00 minutes
  Order0 processed in 5.12 minutes, left at 8.57, inventory: 998
  Inventory low at 150.23: 99. Initiating restock.
  Restocked 500 items at 160.23, new inventory: 599
  ...
  Generated 95 orders
  Average processing time: 2.34 minutes
  Maximum processing time: 6.78 minutes
  Average queue length: 0.67 orders
  Average inventory level: 623.45 items
  Length of timestamps: 95, processing_times: 95, queue_lengths: 95, inventory_levels: 95
  Timestamps: [3.45, 7.89, 12.34, 15.67, 20.12, ...]
  Processing Times: [0.0, 1.2, 2.5, 0.0, 3.1, ...]
  ```
- **Plots**:
  - Top: Processing times vs. arrival times (blue line with markers).
  - Bottom: Queue lengths (red markers) and inventory levels (green markers) vs. arrival times.
- **Chart.js Example** (for external use):
  ```json
  {
    "type": "line",
    "data": {
      "labels": [3.45, 7.89, 12.34, 15.67, 20.12],
      "datasets": [{
        "label": "Processing Times (minutes)",
        "data": [0.0, 1.2, 2.5, 0.0, 3.1],
        "borderColor": "#2196F3",
        "backgroundColor": "rgba(33, 150, 243, 0.2)",
        "fill": true,
        "pointRadius": 5
      }]
    },
    "options": {
      "scales": {
        "y": { "beginAtZero": true, "title": { "display": true, "text": "Processing Time (minutes)" } },
        "x": { "title": { "display": true, "text": "Time (minutes)" } }
      },
      "plugins": { "legend": { "display": true } }
    }
  }
  ```

## Troubleshooting
- **No Output/Plots**: Ensure `!pip install simpy` ran successfully and `MAX_ORDERS` (100) and `SIM_TIME` (480) are reasonable.
- **SyntaxError**: The code fixes global declaration issues by placing `global` statements at the start of `order` and `analyze_and_visualize`.
- **Array Length Mismatch**: Unlikely, but the code trims arrays if needed and prints a warning.
- **Insufficient Inventory**: Adjust `RESTOCK_THRESHOLD` (100) or `RESTOCK_AMOUNT` (500) if orders are skipped frequently.
- **Errors**: Check console for error messages (e.g., invalid parameters).

## Extending the Project
- **Priority Orders**: Use `simpy.PriorityResource` for urgent orders.
- **Multiple Item Types**: Use `simpy.Store` for different product types.
- **Export Data**: Save to CSV with:
  ```python
  import pandas as pd
  pd.DataFrame({"Time": timestamps, "Processing": processing_times}).to_csv("results.csv")
  ```
- **Test Scenarios**: Vary `NUM_WORKERS` (e.g., 5) or `ARRIVAL_RATE` (e.g., 1/2 for busier periods).

## License
For educational use only. Modify and share for learning purposes.

## Contact
Share `Timestamps` and `Processing Times` from the console output for a customized Chart.js visualization.
