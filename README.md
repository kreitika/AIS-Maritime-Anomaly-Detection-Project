#  AIS Maritime Anomaly Detection
*A simple machine learning pipeline to detect unusual vessel behaviour using AIS (Automatic Identification System) data.*

---

##  Overview

This project builds a small but complete anomaly-detection system using AIS signals.  
The goal is to identify vessel movements that look **unusual**, such as:

- sudden speed jumps  
- abrupt slowdowns  
- sharp course changes  
- inconsistent movement patterns  

Using basic AIS fields (lat, lon, speed, course), the notebook extracts motion features and uses an **unsupervised Isolation Forest model** to flag anomalies.  
The output also includes an **interactive map** showing the most suspicious points.

---


##  What the Notebook Does

### 1️⃣ Load & Clean AIS Data
The notebook performs basic preprocessing:

- removes missing/invalid values  
- filters bad lat/lon ranges  
- removes impossible speeds (> 60 knots)  
- sorts messages by vessel (MMSI) and timestamp  

This ensures clean vessel movement sequences.

---

### 2️⃣ Extract Motion Features
For each AIS point, the notebook computes:

- **dt** → time gap (hours)  
- **dist_km** → distance travelled (haversine)  
- **spd_est** → estimated speed from distance/time  
- **accel** → change in speed  
- **turn_rate** → change in course angle  

These features represent how the ship is actually moving.

---

### 3️⃣ Unsupervised Anomaly Detection

Model used: **Isolation Forest**

- no labels required  
- works well on small datasets  
- outputs anomaly scores  
- marks each row as “normal” or “anomaly”  

Higher score = more unusual behaviour.

---

### 4️⃣ Visualise Anomalies on a Map

The notebook uses **Folium** to display the top-k anomalies on an interactive map.  
You can zoom, explore, and inspect suspicious positions with popups showing:

- MMSI  
- coordinates  
- anomaly score  

---

##  Example Outputs

- anomaly rate ~0.16 (normal for a 10-row dataset)  
- anomalies occur where speed or course changes abruptly  
- histogram shows anomaly score distribution  
- Folium map highlights unusual movements in red  

---

##  Technologies Used

- Python  
- pandas  
- numpy  
- scikit-learn (Isolation Forest)  
- folium (map visualisation)  
- Google Colab  

---

##  How to Run

1. Open `AIS_Anomaly_Detection.ipynb` in Google Colab  
2. Upload `ais_sample.csv` when asked  
3. Run all cells top to bottom  
4. Scroll to the map section to inspect anomalies  

---

##  Why This Project Matters

AIS data is critical for:

- maritime safety  
- vessel tracking  
- illegal fishing detection  
- port surveillance  
- identifying suspicious behaviour  

Even a simple ML approach can detect:

- abnormal speed patterns  
- strange course changes  
- route deviations  
- potential AIS spoofing  

---

##  Future Improvements

Possible upgrades:

- use LSTM/Transformer models for full trajectory modelling  
- cluster typical vessel routes and detect off-route behaviour  
- detect AIS spoofing or silent periods  
- add vessel-type classification  
- use a larger AIS dataset (1k–50k rows)  

---
