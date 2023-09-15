1. Connect to Bigquery and select your dataset
2. Top row are "Add a Control" from the upper ribbon
    -- Add a Control and select a column
3. Second row - "Scorecards" from "Add a Chart"
-- Add a Control and select a column
4. Bubble Map
    -- From the "Add a Chart" section, select "Bubble Map"
    -- In the dataset we have latitude and longitude values in seperate columns
    -- Use looker's built-in functions to create location coordinates that can be represented with a point on the map
            -- Concat(latitude, ",", longitude)  --> Add this in the "Add a field" section and a new column with the location coordinates will be added
    -- Select columns of your choice for colour dimension


Link to the Analytics dashboard on LOOker - https://lookerstudio.google.com/reporting/2d778c90-ce19-4a74-9a71-160a4c0932bc