Bird-Migration-and-Climate-Change-A-Data-Science-Experimentation With Real Time Simulation: VERSION 2
 
Welcome to Bird-Migration-and-Climate-Change-A-Data-Science-Experimentation With Real Time Simulation: VERSION 2, a data science project that simulates bird migration patterns across India, exploring the impact of temperature changes due to climate change. This interactive Streamlit application leverages historical bird observation and weather data to generate real-time migration simulations, visualized through dynamic maps, charts, and animations. With multi-select filters for regions, bird types, and species, users can explore migration trends and download simulation data for further analysis.
Version 2 is optimized with vectorized simulations, realistic temperature ranges (15–35°C), non-zero bird counts, and enhanced user interactivity, making it a powerful tool for conservationists, researchers, and data enthusiasts.
Table of Contents

Project Overview
Features of app.py
Other Files
Installation and Setup
Usage
Tech Stack
Future Enhancements
Contributing
License

Project Overview
This project simulates 30 days of bird migration across India, using historical data from bird_weather_merged.csv (3477 rows) to model how temperature influences bird populations. Key features include:

Interactive Visualizations: Folium maps, Plotly charts, and animated migration paths.
Multi-Select Filters: Filter by states (e.g., Delhi, Gujarat), bird categories (e.g., Raptor, Waterfowl), and species (e.g., Indian Pond-Heron, Black Kite).
Optimized Simulation: Vectorized Pandas/NumPy operations for fast processing.
Realistic Data: Non-zero bird counts and temperature clipping (15–35°C).
Exportable Data: Download simulation results as CSV.

The project comprises five Python scripts: data_collection.py, data_preprocessing.py, data_merging.py, data_visualization.py, and app.py, each handling a stage of the data pipeline.
Features of app.py
The core script, app.py, is a Streamlit application that drives the simulation and visualization of bird migration. Below are its key functions:
load_processed_data()

Purpose: Loads and cleans bird_weather_merged.csv.
Functionality:
Reads the CSV with columns like state, common_name, how_many, temperature, bird_category, latitude_x, longitude_x, location_name.
Converts date columns (e.g., observation_date) to datetime.
Cleans how_many: Ensures non-negative values, replacing zeros with random counts (1–5).
Normalizes temperature: Clips to 15–35°C for realistic Indian climate.
Prints debug stats (unique species, states, categories, how_many, temperature).



generate_simulation_data(base_data, start_date, selected_states, selected_categories)

Purpose: Simulates 30 days of bird migration based on historical patterns and temperature trends.
Functionality:
Filters data by selected_states and selected_categories.
Uses vectorized Pandas/NumPy to compute:
Mean temperatures per location.
Mean bird counts per location/species.
Current temperatures with seasonal trends and random noise, clipped to 15–35°C.


Adjusts counts based on temperature anomalies, ensuring bird_count >= 1.
Outputs a DataFrame with date, location_name, latitude, longitude, species_name, bird_count, temperature.
Shows progress via Streamlit bar and terminal logs.



create_interactive_map(data, selected_date, selected_species)

Purpose: Generates a Folium map for a selected date and species.
Functionality:
Plots circles (size ~ bird_count) and a heatmap for bird density.
Includes popups with location, species, count, and temperature.
Centers on India (20.5937°N, 78.9629°E).



create_time_series(data, selected_species)

Purpose: Creates a Plotly time series chart of bird counts and temperatures.
Functionality:
Aggregates bird_count (sum) and temperature (mean) by date.
Plots dual-axis chart: blue line for counts, red dashed line for temperature.



create_species_distribution(data, selected_date)

Purpose: Displays a bar chart of top 10 bird species by count.
Functionality:
Groups by species_name, sums bird_count.
Uses Plotly with Viridis color scale.



create_location_distribution(data, selected_date, selected_species)

Purpose: Shows a bar chart of top 10 migration hotspots.
Functionality:
Filters by selected_species, groups by location_name, sums bird_count.
Plotly bar chart with Viridis colors.



create_temperature_influence_chart(data, selected_species)

Purpose: Visualizes temperature vs. bird count relationship.
Functionality:
Creates a Plotly scatter plot with optional trendline (OLS) for specific species.
Colors by species_name if “All Species” is selected.



create_migration_animation_data(data, selected_species)

Purpose: Generates data for an animated migration map.
Functionality:
Creates Timestamped GeoJSON features with circle sizes (bird count) and colors (temperature).
Includes popups with location, date, count, and temperature.



main()

Purpose: Orchestrates the Streamlit app’s UI and logic.
Functionality:
Sets up sidebar controls: multi-select for states, bird categories, species; date slider; custom start date.
Renders tabs: Map View, Trends Analysis, Species Distribution, Animation.
Displays summary stats (total birds, average temperature, number of species).
Provides insights/recommendations and CSV download.



Other Files
data_collection.py

Purpose: Collects raw bird observation and weather data.
Functionality:
Fetches bird sightings (e.g., from eBird API) with common_name, how_many, latitude, longitude, observation_date.
Retrieves weather data (e.g., temperature) for matching locations/dates.
Outputs bird_data.csv and weather_data.csv.


Role: Provides raw datasets for the pipeline.

data_preprocessing.py

Purpose: Cleans and formats raw data.
Functionality:
Handles missing values, duplicates, and outliers in bird_data.csv and weather_data.csv.
Standardizes columns (e.g., datetime dates, numeric how_many).
Adds derived columns like state and bird_category.
Outputs cleaned_bird_data.csv and cleaned_weather_data.csv.


Role: Ensures data quality for merging.

data_merging.py

Purpose: Combines cleaned bird and weather data.
Functionality:
Merges cleaned_bird_data.csv and cleaned_weather_data.csv on latitude, longitude, observation_date.
Resolves mismatches (e.g., nearest date matching).
Outputs bird_weather_merged.csv with state, common_name, how_many, temperature, bird_category.


Role: Creates the master dataset for app.py and data_visualization.py.

data_visualization.py

Purpose: Generates exploratory visualizations.
Functionality:
Creates plots (e.g., histograms of how_many, temperature vs. bird count).
Analyzes species distribution (e.g., Indian Pond-Heron) and regional trends.
Outputs PNGs for reference.


Role: Informs simulation logic in app.py.

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

Place bird_weather_merged.csv in the project root.
Run data_collection.py, data_preprocessing.py, and data_merging.py if starting from scratch.


Run the App:
streamlit run app.py


Open http://localhost:8501 in your browser.



Usage

Filters: Use sidebar multi-selects for states, bird categories, and species.
Date Slider: Select a day within the 30-day simulation.
Tabs:
Map View: Interactive map with hotspots.
Trends Analysis: Time series and temperature influence charts.
Species Distribution: Top species bar chart.
Animation: Animated migration over 30 days.


Download: Export data as bird_migration_simulation.csv.

Tech Stack

Python 3.9: Core programming language.
Pandas: Data manipulation and simulation.
NumPy: Array operations for temperature/counts.
Streamlit: Web app framework.
Folium: Interactive maps with heatmaps/GeoJSON.
Plotly: Dynamic charts (time series, scatter, bar).
Matplotlib: Static plots in data_visualization.py.
SciPy: Interpolation for simulation trends.
Conda: Environment management.

Future Enhancements

Predictive Modeling: XGBoost with GPU support for bird count predictions.
Real-Time Weather: OpenWeatherMap API integration.
Migration Paths: Animated routes between locations.
Species Info Panel: Display scientific names, migratory status, images.
PDF Reports: Export stats and visuals as PDFs.
GPU Optimization: CuPy for faster array operations.

Contributing
Fork, submit issues, or send pull requests! Contact [your-email] for collaboration.
License
MIT License. See LICENSE for details.

Bird Migration Simulator: VERSION 2 - Exploring bird migration and climate change through data science. Built with 💻 and 🦅!



<img width="1276" alt="image" src="https://github.com/user-attachments/assets/1617fe79-d23a-4556-a98e-2a57c08dc077" />



<img width="1280" alt="image" src="https://github.com/user-attachments/assets/c39a0c14-ebe8-4adc-bbac-34688896d7b9" />



<img width="1275" alt="image" src="https://github.com/user-attachments/assets/9e199ea9-b17f-4258-b374-e304ac4db7be" />



<img width="1271" alt="image" src="https://github.com/user-attachments/assets/ca4ea9ba-7884-449c-8af2-b2e517cd0c1a" />



<img width="1274" alt="image" src="https://github.com/user-attachments/assets/b804ee33-af6e-457e-88aa-e9d3c09fc2d6" />



<img width="725" alt="image" src="https://github.com/user-attachments/assets/68ba4342-5843-4a0d-82e0-4e9dedf3093c" />



<img width="1280" alt="image" src="https://github.com/user-attachments/assets/eb3a85bd-d856-4bec-a683-5a1a15a22029" />

