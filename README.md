Bird-Migration-and-Climate-Change-A-Data-Science-Experimentation With Real Time Simulation: VERSION 2
Welcome to Bird-Migration-and-Climate-Change-A-Data-Science-Experimentation With Real Time Simulation: VERSION 2, a data science project that simulates bird migration patterns across India, exploring the impact of temperature changes due to climate change. This interactive Streamlit application leverages historical bird observation and weather data to generate real-time migration simulations, visualized through dynamic maps, charts, and animations. With multi-select filters for regions, bird types, and species, users can explore migration trends and download simulation data for further analysis.
This is Version 2, optimized with vectorized simulations, realistic temperature ranges (15–35°C), non-zero bird counts, and enhanced user interactivity, making it a powerful tool for conservationists, researchers, and data enthusiasts.

<img width="283" alt="image" src="https://github.com/user-attachments/assets/4b53c994-8e0a-4888-ab61-8130fe9e2c6d" />

<img width="1276" alt="image" src="https://github.com/user-attachments/assets/1617fe79-d23a-4556-a98e-2a57c08dc077" />

<img width="1280" alt="image" src="https://github.com/user-attachments/assets/c39a0c14-ebe8-4adc-bbac-34688896d7b9" />

<img width="1275" alt="image" src="https://github.com/user-attachments/assets/9e199ea9-b17f-4258-b374-e304ac4db7be" />

<img width="1271" alt="image" src="https://github.com/user-attachments/assets/ca4ea9ba-7884-449c-8af2-b2e517cd0c1a" />

<img width="1274" alt="image" src="https://github.com/user-attachments/assets/b804ee33-af6e-457e-88aa-e9d3c09fc2d6" />

<img width="725" alt="image" src="https://github.com/user-attachments/assets/68ba4342-5843-4a0d-82e0-4e9dedf3093c" />

<img width="1280" alt="image" src="https://github.com/user-attachments/assets/eb3a85bd-d856-4bec-a683-5a1a15a22029" />


Project Overview
The project simulates 30 days of bird migration across India, using historical data from bird_weather_merged.csv (3477 rows) to model how temperature influences bird populations. Key features include:

Interactive Visualizations: Folium maps, Plotly charts, and animated migration paths.
Multi-Select Filters: Filter by states (e.g., Delhi, Gujarat), bird categories (e.g., Raptor, Waterfowl), and species (e.g., Indian Pond-Heron, Black Kite).
Optimized Simulation: Vectorized Pandas/NumPy operations ensure fast processing of large datasets.
Realistic Data: Non-zero bird counts and temperature clipping (15–35°C) for accurate modeling.
Exportable Data: Download simulation results as CSV for further analysis.

The project consists of five Python scripts: data_collection.py, data_preprocessing.py, data_merging.py, data_visualization.py, and app.py, each handling a specific stage of the data pipeline.
Features of app.py
The core of the project, app.py, is a Streamlit application that orchestrates the simulation and visualization of bird migration. Below are its key functions and their roles:
1. load_processed_data()

Purpose: Loads and cleans bird_weather_merged.csv.
Functionality:
Reads the CSV (3477 rows) with columns like state, common_name, how_many, temperature, bird_category, latitude_x, longitude_x, location_name.
Converts date columns (e.g., observation_date) to datetime.
Cleans how_many: Ensures non-negative values, replacing zeros with random counts (1–5).
Normalizes temperature: Clips to 15–35°C for realistic Indian climate.
Prints debug stats (unique species, states, categories, how_many, temperature).



2. generate_simulation_data(base_data, start_date, selected_states, selected_categories)

Purpose: Simulates 30 days of bird migration based on historical patterns and temperature trends.
Functionality:
Filters data by selected_states (e.g., Delhi) and selected_categories (e.g., Raptor).
Uses vectorized Pandas/NumPy to compute:
Mean temperatures per location (loc_temps).
Mean bird counts per location/species (base_counts).
Current temperatures with seasonal trends (sin function) and random noise, clipped to 15–35°C.


Adjusts counts based on temperature anomalies and species sensitivity, ensuring bird_count >= 1.
Outputs a DataFrame with columns: date, location_name, latitude, longitude, species_name, bird_count, temperature.
Shows progress via Streamlit bar and terminal logs.



3. create_interactive_map(data, selected_date, selected_species)

Purpose: Generates a Folium map showing bird migration for a selected date and species.
Functionality:
Plots circles (size ~ bird_count) and a heatmap for bird density.
Includes popups with location, species, count, and temperature.
Centers on India (20.5937°N, 78.9629°E).



4. create_time_series(data, selected_species)

Purpose: Creates a Plotly time series chart of bird counts and temperatures over 30 days.
Functionality:
Aggregates bird_count (sum) and temperature (mean) by date.
Plots dual-axis chart: blue line for counts, red dashed line for temperature.



5. create_species_distribution(data, selected_date)

Purpose: Displays a bar chart of the top 10 bird species by count on a selected date.
Functionality:
Groups by species_name, sums bird_count.
Uses Plotly with Viridis color scale for visual appeal.



6. create_location_distribution(data, selected_date, selected_species)

Purpose: Shows a bar chart of the top 10 migration hotspots by bird count.
Functionality:
Filters by selected_species, groups by location_name, sums bird_count.
Plotly bar chart with Viridis colors.



7. create_temperature_influence_chart(data, selected_species)

Purpose: Visualizes the relationship between temperature and bird count.
Functionality:
Creates a Plotly scatter plot with optional trendline (OLS) for specific species.
Colors by species_name if “All Species” is selected.



8. create_migration_animation_data(data, selected_species)

Purpose: Generates data for an animated migration map over 30 days.
Functionality:
Creates Timestamped GeoJSON features with circle sizes (bird count) and colors (temperature).
Includes popups with location, date, count, and temperature.



9. main()

Purpose: Orchestrates the Streamlit app’s UI and logic.
Functionality:
Sets up sidebar controls: multi-select for states, bird categories, species; date slider; custom start date option.
Renders four tabs: Map View, Trends Analysis, Species Distribution, Animation.
Displays summary stats (total birds, average temperature, number of species).
Provides insights/recommendations and a CSV download button.



Other Files
The project includes four supporting scripts that prepare the data for app.py:
1. data_collection.py

Purpose: Collects raw bird observation and weather data.
Functionality:
Fetches bird sightings from eBird API (or similar) with columns like common_name, how_many, latitude, longitude, observation_date.
Retrieves weather data (e.g., temperature) for corresponding locations and dates.
Outputs raw CSVs: bird_data.csv and weather_data.csv.


Role: Provides the foundational datasets for analysis.

2. data_preprocessing.py

Purpose: Cleans and formats raw data for consistency.
Functionality:
Handles missing values, duplicates, and outliers in bird_data.csv and weather_data.csv.
Standardizes columns (e.g., converts dates to datetime, ensures numeric how_many).
Adds derived columns like state and bird_category (e.g., Raptor, Waterfowl).
Outputs cleaned CSVs: cleaned_bird_data.csv and cleaned_weather_data.csv.


Role: Ensures data quality for merging and analysis.

3. data_merging.py

Purpose: Combines cleaned bird and weather data.
Functionality:
Merges cleaned_bird_data.csv and cleaned_weather_data.csv on latitude, longitude, and observation_date.
Resolves mismatches (e.g., nearest date matching for weather).
Outputs bird_weather_merged.csv with unified columns (e.g., state, common_name, how_many, temperature, bird_category).


Role: Creates the master dataset used by app.py and data_visualization.py.

4. data_visualization.py

Purpose: Generates exploratory visualizations to understand data patterns.
Functionality:
Creates static plots (e.g., histograms of how_many, temperature vs. bird count scatter).
Analyzes species distribution (e.g., Indian Pond-Heron prevalence) and regional trends.
Outputs plots to files (e.g., PNGs) for reference.


Role: Provides insights that inform the simulation logic in app.py.

Installation and Setup

Clone the Repository:
git clone https://github.com/your-username/Bird-Migration-and-Climate-Change-A-Data-Science-Experimentation.git
cd Bird-Migration-and-Climate-Change-A-Data-Science-Experimentation


Create a Conda Environment:
conda create -n bird-migration python=3.9
conda activate bird-migration


Install Dependencies:
pip install streamlit pandas numpy matplotlib folium streamlit-folium plotly scipy


Ensure Data:

Place bird_weather_merged.csv in the project root (generated by data_merging.py).
Run data_collection.py, data_preprocessing.py, and data_merging.py if starting from scratch.


Run the App:
streamlit run app.py


Open http://localhost:8501 in your browser.



Usage

Filters: Use sidebar multi-selects to choose states (e.g., Delhi, Gujarat), bird categories (e.g., Raptor, Waterfowl), and species (e.g., Indian Pond-Heron).
Date Slider: Select a specific day within the 30-day simulation.
Tabs:
Map View: Interactive map with migration hotspots.
Trends Analysis: Time series and temperature influence charts.
Species Distribution: Bar chart of top species.
Animation: Animated migration over 30 days.


Download: Export simulation data as bird_migration_simulation.csv.

Tech Stack

Python 3.9: Core programming language.
Pandas: Data manipulation and vectorized simulation.
NumPy: Efficient array operations for temperature and count calculations.
Streamlit: Interactive web app framework.
Folium: Interactive maps with heatmaps and GeoJSON animations.
Plotly: Dynamic charts (time series, scatter, bar).
Matplotlib: Static plot support (used in data_visualization.py).
SciPy: Interpolation for smooth simulation trends.
Conda: Environment management.

Future Enhancements

Predictive Modeling: Integrate XGBoost with GPU support for data-driven bird count predictions.
Real-Time Weather: Fetch live temperature data via OpenWeatherMap API.
Migration Paths: Visualize animated migration routes between locations.
Species Info Panel: Display scientific names, migratory status, and images.
PDF Reports: Export summary stats and visuals as PDFs.
GPU Optimization: Use CuPy for faster array operations.

Contributing
Feel free to fork, submit issues, or send pull requests! Contact [your-email] for collaboration.
License
MIT License. See LICENSE for details.

Bird Migration Simulator: VERSION 2 - Exploring the nexus of bird migration and climate change through data science. Built with 💻 and 🦅!
