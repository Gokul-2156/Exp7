from bokeh.io import show
from bokeh.models import ColumnDataSource, HoverTool
from bokeh.plotting import figure
from bokeh.layouts import column
import pandas as pd
import folium
# Load your data
data = pd.read_csv('D:\ARCHANA\dxv\LAB\DXV\geographic.csv')
# Create a Bokeh figure
p = figure(width=800, height=400, tools='pan,wheel_zoom,reset')
# Create a ColumnDataSource to hold data
source = ColumnDataSource(data)
# Add circle markers to the figure
p.circle(x='Longitude', y='Latitude', size=10, source=source, color='orange')
# Create a hover tool for mouse rollover effect
hover = HoverTool()
hover.tooltips = [("Info", "@Info"), ("Latitude", "@Latitude"), ("Longitude", "@Longitude")]
p.add_tools(hover)
# Display the Bokeh plot
layout = column(p)
show(layout)
# Create a map centered at a specific location
m = folium.Map(location=[latitude, longitude], zoom_start=10)
# Add markers for your data points
for index, row in data.iterrows():
    folium.Marker(
        location=[row['Latitude'], row['Longitude']],
        popup=row['Info'],  # Display additional info on mouse click
    ).add_to(m)
# Save the map to an HTML file
m.save('map.html')
![image](https://github.com/user-attachments/assets/991231a4-7bce-46af-a67e-d48eb7856ad2)
![image](https://github.com/user-attachments/assets/5a8eceb7-ebcb-4897-99c6-4e90b56cde29)
