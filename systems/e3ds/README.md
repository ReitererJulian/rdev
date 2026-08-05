# Blender 5 – STL File Reduction Workflow

## 1. Import the STL File

- Import the STL model into **Blender 5**.
    
- Set the import **Scale** to **0.001** (meters → millimeters).
    
    - Alternatively, you can set the scale directly when dragging the STL file into Blender.
        

## 2. Orient the Model

- Align the model with the coordinate system.
    
- Rotate the model:
    
    - **Z-axis:** **+180°** (so the handle-like structures point upwards)
        
- Verify the orientation along the **X, Y, and Z axes**.
    

---

## 3. First Decimation

1. Open the **Modifiers** tab (wrench icon).
    
2. Add a modifier:
    
    - **Add Modifier → Generate → Decimate**
        
3. Set the **Ratio** to **0.1**.
    
4. Aim for approximately **100,000 vertices/faces**.
    
5. If the mesh becomes too coarse, increase the ratio slightly.
    

---

## 4. Remove the Outer Rim

Before selecting vertices:

- Press **Alt + Z** to enable **X-Ray Mode**.
    
    - Otherwise, only visible vertices will be selected.
        

Next:

1. Switch to **Edit Mode**.
    
2. Select the vertices as shown in the reference screenshot.
    
3. Press **Ctrl + I** to invert the selection.
    
4. Delete the outer rim:
    
    - Press **Delete (X)** → **Vertices**.
        

---

## 5. Second Decimation

1. Open the **Modifiers** tab again.
    
2. Add another **Decimate** modifier.
    
3. Set the **Ratio** to **0.25**.
    
4. Target approximately **80,000 vertices/faces**.
    

### For Larger Models

If the file is still very large:

- Reduce the ratio further to **0.1**.
    
- A final mesh between **80,000 and 150,000 vertices/faces** is typically sufficient.
    

---

## 6. Export

- Save the project.
    
- Export the model as **STL**.
    

Example:

- `decimated_6.stl` → approximately **4 MB**
    

### Notes

- **Model 3** has already been reduced and does not require additional processing.
    
- **Model 2** should be reviewed again.
    

---

# Sensor Validation

- Mount all **three sensors** together.
    
- Perform measurements while **shaking them in free air**.
    
- Compare the sensor outputs and analyze how the deviations change over time.
    

---

# Script

Integrate the existing script into a **multiprocessing** implementation.

---

## Notes for ChatGPT

If you ask ChatGPT for Blender-related help, mention that you are using **Blender 5**, as some instructions differ from previous versions.


### TODO

Powerpoint about Testing Sensors
Based upon the Docu PDF

- Process documentation
	- What could be automated
- 

Powerpoint about finishing Weather Station
- Requierments
- Planning
	- Time...
- 