# 🦅 Bird-Migration-and-Climate-Change-A-Data-Science-Experimentation With Real Time Simulation: VERSION 2

Welcome to **Bird-Migration-and-Climate-Change-A-Data-Science-Experimentation With Real Time Simulation: VERSION 2**, a data science project that simulates bird migration patterns across India while exploring the impact of temperature changes due to climate change.

This interactive **Streamlit** application leverages historical bird observation and weather data to generate **real-time migration simulations**, visualized through **dynamic maps, charts, and animations**. With multi-select filters for regions, bird types, and species, users can explore migration trends and download simulation data for further analysis.

🔧 **Version 2 Highlights**:
- Vectorized simulations for performance
- Realistic temperature ranges (15–35°C)
- Non-zero bird counts
- Enhanced user interactivity

---

## 📚 Table of Contents
- [Project Overview](#project-overview)
- [Features of app.py](#features-of-apppy)
- [Other Files](#other-files)
- [Installation and Setup](#installation-and-setup)
- [Usage](#usage)
- [Tech Stack](#tech-stack)
- [Future Enhancements](#future-enhancements)
- [Contributing](#contributing)
- [License](#license)

---

## 📈 Project Overview

This project simulates **30 days** of bird migration across India, using historical data from `bird_weather_merged.csv` (3477 rows) to model how temperature influences bird populations.

### 🔍 Key Features:
- **Interactive Visualizations**: Folium maps, Plotly charts, and animated migration paths.
- **Multi-Select Filters**: Filter by states (e.g., Delhi, Gujarat), bird categories (e.g., Raptor, Waterfowl), and species (e.g., Indian Pond-Heron, Black Kite).
- **Optimized Simulation**: Vectorized Pandas/NumPy operations for fast processing.
- **Realistic Data**: Non-zero bird counts and temperature clipping (15–35°C).
- **Exportable Data**: Download simulation results as CSV.

> **Pipeline Scripts**:  
> `data_collection.py`, `data_preprocessing.py`, `data_merging.py`, `data_visualization.py`, and `app.py`.

---

## 🔍 Features of `app.py`

### `load_processed_data()`
- Loads and cleans `bird_weather_merged.csv`.
- Ensures non-negative `how_many` values; replaces zeros with random (1–5).
- Clips temperature values to 15–35°C.
- Converts `observation_date` to datetime.

---

### `generate_simulation_data(base_data, start_date, selected_states, selected_categories)`
- Filters data based on selections.
- Simulates temperature trends and anomalies.
- Adjusts bird counts using vectorized operations.
- Generates 30-day simulation data.

---

### `create_interactive_map(data, selected_date, selected_species)`
- Folium map with:
  - Circle markers sized by `bird_count`
  - Heatmap layer
  - Location/species/temperature popups

---

### `create_time_series(data, selected_species)`
- Plotly dual-axis line chart:
  - Blue: Bird count (sum)
  - Red (dashed): Temperature (mean)

---

### `create_species_distribution(data, selected_date)`
- Bar chart of **top 10 bird species** by count using Plotly (Viridis scale)

---

### `create_location_distribution(data, selected_date, selected_species)`
- Bar chart of **top 10 locations** for selected species

---

### `create_temperature_influence_chart(data, selected_species)`
- Scatter plot showing bird count vs. temperature
- Optional trendline (OLS)

---

### `create_migration_animation_data(data, selected_species)`
- Creates **Timestamped GeoJSON** for animated map
- Circle size = bird count | Color = temperature

---

### `main()`
- Builds the complete Streamlit interface:
  - Sidebar controls (multi-selects, date slider)
  - Tabs: Map View, Trends, Species Distribution, Animation
  - Summary stats + CSV download

---

## 📁 Other Files

### `data_collection.py`
- Fetches raw bird and weather data
- Exports: `bird_data.csv`, `weather_data.csv`

### `data_preprocessing.py`
- Cleans raw data (nulls, duplicates, outliers)
- Adds columns: `state`, `bird_category`
- Outputs: `cleaned_bird_data.csv`, `cleaned_weather_data.csv`

### `data_merging.py`
- Merges bird and weather datasets
- Outputs: `bird_weather_merged.csv`

### `data_visualization.py`
- Exploratory plots (static)
- Supports logic building for app.py

---

## ⚙️ Installation and Setup

### Clone the Repository:
```bash
git clone https://github.com/your-username/Bird-Migration-and-Climate-Change-A-Data-Science-Experimentation.git
cd Bird-Migration-and-Climate-Change-A-Data-Science-Experimentation
```


<img width="1276" alt="image" src="https://github.com/user-attachments/assets/1617fe79-d23a-4556-a98e-2a57c08dc077" />



<img width="1280" alt="image" src="https://github.com/user-attachments/assets/c39a0c14-ebe8-4adc-bbac-34688896d7b9" />



<img width="1275" alt="image" src="https://github.com/user-attachments/assets/9e199ea9-b17f-4258-b374-e304ac4db7be" />



<img width="1271" alt="image" src="https://github.com/user-attachments/assets/ca4ea9ba-7884-449c-8af2-b2e517cd0c1a" />



<img width="1274" alt="image" src="https://github.com/user-attachments/assets/b804ee33-af6e-457e-88aa-e9d3c09fc2d6" />



<img width="725" alt="image" src="https://github.com/user-attachments/assets/68ba4342-5843-4a0d-82e0-4e9dedf3093c" />



<img width="1280" alt="image" src="https://github.com/user-attachments/assets/eb3a85bd-d856-4bec-a683-5a1a15a22029" />

