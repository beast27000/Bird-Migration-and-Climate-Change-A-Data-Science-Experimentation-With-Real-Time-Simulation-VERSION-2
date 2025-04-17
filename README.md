# Bird-Migration-and-Climate-Change-A-Data-Science-Experimentation With Real Time Simulation: VERSION 2

Welcome to **Bird-Migration-and-Climate-Change-A-Data-Science-Experimentation With Real Time Simulation: VERSION 2**, a data science project that simulates bird migration patterns across India, exploring the impact of temperature changes due to climate change.

This interactive **Streamlit** application leverages historical bird observation and weather data to generate real-time migration simulations, visualized through dynamic maps, charts, and animations. With multi-select filters for regions, bird types, and species, users can explore migration trends and download simulation data for further analysis.

**Version 2** is optimized with vectorized simulations, realistic temperature ranges (15–35°C), non-zero bird counts, and enhanced user interactivity, making it a powerful tool for conservationists, researchers, and data enthusiasts.

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

## 📊 Project Overview

This project simulates **30 days** of bird migration across India, using historical data from `bird_weather_merged.csv` (3477 rows) to model how temperature influences bird populations.

### Key Features:
- **Interactive Visualizations**: Folium maps, Plotly charts, and animated migration paths.
- **Multi-Select Filters**: Filter by states (e.g., Delhi, Gujarat), bird categories (e.g., Raptor, Waterfowl), and species (e.g., Indian Pond-Heron, Black Kite).
- **Optimized Simulation**: Vectorized Pandas/NumPy operations for fast processing.
- **Realistic Data**: Non-zero bird counts and temperature clipping (15–35°C).
- **Exportable Data**: Download simulation results as CSV.

---

## 🧠 Features of `app.py`

The core script, `app.py`, is a Streamlit application that drives the simulation and visualization of bird migration.

### `load_processed_data()`
**Purpose**: Loads and cleans `bird_weather_merged.csv`.

- Reads columns like: `state`, `common_name`, `how_many`, `temperature`, `bird_category`, `latitude_x`, `longitude_x`, `location_name`.
- Converts `observation_date` to datetime.
- Ensures non-negative bird counts; replaces zero with random 1–5.
- Clips temperature to 15–35°C.
- Prints debug stats.

---

### `generate_simulation_data(base_data, start_date, selected_states, selected_categories)`
**Purpose**: Simulates 30 days of migration.

- Filters data by selections.
- Uses Pandas/NumPy to calculate:
  - Mean temperatures and bird counts per location.
  - Adds random noise to simulate seasonal variation.
- Ensures bird_count ≥ 1.
- Returns a DataFrame of simulated results.
- Shows progress via Streamlit bar and logs.

---

### `create_interactive_map(data, selected_date, selected_species)`
**Purpose**: Visual map rendering using Folium.

- Plots circle markers and heatmap.
- Includes popups with species, counts, and temperature.
- Centers map on India.

---

### `create_time_series(data, selected_species)`
**Purpose**: Time series using Plotly.

- Aggregates bird counts and temperature by date.
- Dual-axis chart: bird count vs. temperature.

---

### `create_species_distribution(data, selected_date)`
**Purpose**: Bar chart of top 10 bird species.

- Groups data and plots with Plotly.

---

### `create_location_distribution(data, selected_date, selected_species)`
**Purpose**: Bar chart of top 10 migration hotspots.

- Filters by species, groups by location.
- Displays migration-rich areas.

---

### `create_temperature_influence_chart(data, selected_species)`
**Purpose**: Scatter plot to analyze temperature impact.

- Shows trendline with OLS.
- Colored by species if “All Species” is selected.

---

### `create_migration_animation_data(data, selected_species)`
**Purpose**: Generates data for animated migration.

- Creates timestamped GeoJSON features.
- Maps bird count and temperature visually.

---

### `main()`
**Purpose**: Runs the entire Streamlit app.

- Sidebar controls: region, bird type, species, date.
- Tabs:
  - **Map View**
  - **Trends Analysis**
  - **Species Distribution**
  - **Animation**
- Summary stats and CSV export.

---

## 📁 Other Files

### `data_collection.py`
**Purpose**: Collects raw data.

- Gets bird sightings (from eBird or similar).
- Retrieves weather for same dates/locations.
- Outputs: `bird_data.csv`, `weather_data.csv`.

---

### `data_preprocessing.py`
**Purpose**: Cleans and formats raw data.

- Handles nulls, duplicates, and formats.
- Adds derived columns: `state`, `bird_category`.
- Outputs: `cleaned_bird_data.csv`, `cleaned_weather_data.csv`.

---

### `data_wrangling.py` 
**Purpose**: Merges bird and weather data.

- Combines cleaned datasets on location and date.
- Handles nearest-date matches if necessary.
- Outputs: `bird_weather_merged.csv`.

---

### `data_visualization.py`
**Purpose**: Explores data visually.

- Histograms, trends, species distributions.
- Outputs static plots (PNGs) to support simulation design.

---

## ⚙️ Installation and Setup

### 1. Clone the Repository:
```bash
git clone https://github.com/your-username/Bird-Migration-and-Climate-Change-A-Data-Science-Experimentation.git
cd Bird-Migration-and-Climate-Change-A-Data-Science-Experimentation


<img width="1276" alt="image" src="https://github.com/user-attachments/assets/1617fe79-d23a-4556-a98e-2a57c08dc077" />



<img width="1280" alt="image" src="https://github.com/user-attachments/assets/c39a0c14-ebe8-4adc-bbac-34688896d7b9" />



<img width="1275" alt="image" src="https://github.com/user-attachments/assets/9e199ea9-b17f-4258-b374-e304ac4db7be" />



<img width="1271" alt="image" src="https://github.com/user-attachments/assets/ca4ea9ba-7884-449c-8af2-b2e517cd0c1a" />



<img width="1274" alt="image" src="https://github.com/user-attachments/assets/b804ee33-af6e-457e-88aa-e9d3c09fc2d6" />



<img width="725" alt="image" src="https://github.com/user-attachments/assets/68ba4342-5843-4a0d-82e0-4e9dedf3093c" />



<img width="1280" alt="image" src="https://github.com/user-attachments/assets/eb3a85bd-d856-4bec-a683-5a1a15a22029" />

