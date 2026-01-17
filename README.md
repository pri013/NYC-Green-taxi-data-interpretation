<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NYC Green Taxi Tip Prediction - README</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, sans-serif;
            line-height: 1.6;
            color: #333;
            max-width: 1000px;
            margin: 0 auto;
            padding: 20px;
            background-color: #f6f8fa;
        }
        
        .container {
            background: white;
            padding: 40px;
            border-radius: 10px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
        }
        
        h1 {
            color: #1a1a2e;
            border-bottom: 3px solid #f9a825;
            padding-bottom: 15px;
            margin-bottom: 20px;
        }
        
        h2 {
            color: #16213e;
            margin-top: 40px;
            margin-bottom: 15px;
            padding-bottom: 10px;
            border-bottom: 2px solid #eee;
        }
        
        h3 {
            color: #0f3460;
            margin-top: 25px;
            margin-bottom: 10px;
        }
        
        .badge {
            display: inline-block;
            padding: 5px 10px;
            border-radius: 5px;
            font-size: 12px;
            font-weight: bold;
            margin-right: 5px;
            color: white;
        }
        
        .badge-r { background-color: #276DC3; }
        .badge-license { background-color: #97ca00; }
        
        table {
            width: 100%;
            border-collapse: collapse;
            margin: 15px 0;
            font-size: 14px;
        }
        
        th, td {
            border: 1px solid #ddd;
            padding: 12px;
            text-align: left;
        }
        
        th {
            background-color: #1a1a2e;
            color: white;
        }
        
        tr:nth-child(even) {
            background-color: #f9f9f9;
        }
        
        tr:hover {
            background-color: #f1f1f1;
        }
        
        code {
            background-color: #f4f4f4;
            padding: 2px 6px;
            border-radius: 4px;
            font-family: 'Courier New', monospace;
            font-size: 13px;
        }
        
        pre {
            background-color: #1a1a2e;
            color: #a8dadc;
            padding: 20px;
            border-radius: 8px;
            overflow-x: auto;
            margin: 15px 0;
            font-size: 13px;
        }
        
        .highlight {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 20px;
            border-radius: 10px;
            margin: 20px 0;
        }
        
        .highlight h3 {
            color: white;
            margin-top: 0;
        }
        
        .insight-box {
            background-color: #e8f5e9;
            border-left: 5px solid #4caf50;
            padding: 15px 20px;
            margin: 15px 0;
            border-radius: 0 8px 8px 0;
        }
        
        .warning-box {
            background-color: #fff3e0;
            border-left: 5px solid #ff9800;
            padding: 15px 20px;
            margin: 15px 0;
            border-radius: 0 8px 8px 0;
        }
        
        .metrics-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 20px;
            margin: 20px 0;
        }
        
        .metric-card {
            background: linear-gradient(135deg, #1a1a2e 0%, #16213e 100%);
            color: white;
            padding: 20px;
            border-radius: 10px;
            text-align: center;
        }
        
        .metric-card .value {
            font-size: 32px;
            font-weight: bold;
            color: #f9a825;
        }
        
        .metric-card .label {
            font-size: 14px;
            opacity: 0.8;
        }
        
        .toc {
            background-color: #f8f9fa;
            padding: 20px;
            border-radius: 8px;
            margin: 20px 0;
        }
        
        .toc ul {
            list-style: none;
            columns: 2;
        }
        
        .toc li {
            padding: 5px 0;
        }
        
        .toc a {
            color: #0066cc;
            text-decoration: none;
        }
        
        .toc a:hover {
            text-decoration: underline;
        }
        
        .folder-structure {
            background-color: #263238;
            color: #aed581;
            padding: 20px;
            border-radius: 8px;
            font-family: monospace;
        }
        
        .star-rating {
            color: #f9a825;
            font-size: 18px;
        }
        
        .plot-placeholder {
            background: linear-gradient(135deg, #e0e0e0 0%, #bdbdbd 100%);
            border: 2px dashed #999;
            border-radius: 10px;
            padding: 40px;
            text-align: center;
            margin: 15px 0;
            color: #666;
        }
        
        .plot-placeholder .icon {
            font-size: 48px;
            margin-bottom: 10px;
        }
        
        footer {
            text-align: center;
            margin-top: 40px;
            padding-top: 20px;
            border-top: 1px solid #eee;
            color: #666;
        }
        
        .btn {
            display: inline-block;
            padding: 10px 20px;
            background-color: #1a1a2e;
            color: white;
            text-decoration: none;
            border-radius: 5px;
            margin: 5px;
        }
        
        .btn:hover {
            background-color: #16213e;
        }
        
        .emoji {
            font-size: 1.2em;
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- Header -->
        <h1><span class="emoji">🚕</span> NYC Green Taxi Tip Prediction Using k-NN Regression</h1>
        
        <p>
            <span class="badge badge-r">R 4.0+</span>
            <span class="badge badge-license">MIT License</span>
        </p>
        
        <p style="font-size: 18px; margin-top: 15px;">
            A machine learning project that predicts tip amounts for NYC Green Taxi trips using the 
            <strong>CRISP-DM methodology</strong> and <strong>k-Nearest Neighbors (k-NN) regression</strong> modeling.
        </p>

        <!-- Table of Contents -->
        <h2><span class="emoji">📋</span> Table of Contents</h2>
        <div class="toc">
            <ul>
                <li><a href="#overview">Overview</a></li>
                <li><a href="#dataset">Dataset</a></li>
                <li><a href="#project-structure">Project Structure</a></li>
                <li><a href="#installation">Installation</a></li>
                <li><a href="#methodology">Methodology</a></li>
                <li><a href="#results">Results</a></li>
                <li><a href="#insights">Key Insights</a></li>
                <li><a href="#references">References</a></li>
            </ul>
        </div>

        <!-- Overview -->
        <h2 id="overview"><span class="emoji">🎯</span> Overview</h2>
        <p>This project analyzes NYC Green Taxi trip data from 2018 to:</p>
        <ol>
            <li><strong>Predict tip amounts</strong> using k-NN regression</li>
            <li><strong>Understand tipping patterns</strong> based on trip characteristics</li>
            <li><strong>Analyze operational efficiency</strong> across different times and days</li>
        </ol>
        
        <div class="insight-box">
            <h4>Why Green Taxis?</h4>
            <p>Green taxis (Boro Taxis) serve areas outside Manhattan's core, providing valuable insights into outer-borough transportation patterns.</p>
        </div>

        <!-- Dataset -->
        <h2 id="dataset"><span class="emoji">📊</span> Dataset</h2>
        
        <table>
            <tr>
                <th>Attribute</th>
                <th>Description</th>
            </tr>
            <tr>
                <td><strong>Source</strong></td>
                <td><a href="https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page">NYC Taxi & Limousine Commission</a></td>
            </tr>
            <tr>
                <td><strong>Period</strong></td>
                <td>January - February 2018</td>
            </tr>
            <tr>
                <td><strong>Original Size</strong></td>
                <td>1,048,575 rows × 19 columns</td>
            </tr>
            <tr>
                <td><strong>Cleaned Size</strong></td>
                <td>531,855 rows × 26 columns</td>
            </tr>
        </table>

        <h3>Key Variables</h3>
        <table>
            <tr>
                <th>Variable</th>
                <th>Type</th>
                <th>Description</th>
            </tr>
            <tr>
                <td><code>tip_amount</code></td>
                <td>Target</td>
                <td>Tip amount in USD (credit card only)</td>
            </tr>
            <tr>
                <td><code>trip_distance</code></td>
                <td>Numeric</td>
                <td>Distance traveled in miles</td>
            </tr>
            <tr>
                <td><code>fare_amount</code></td>
                <td>Numeric</td>
                <td>Base fare in USD</td>
            </tr>
            <tr>
                <td><code>passenger_count</code></td>
                <td>Numeric</td>
                <td>Number of passengers</td>
            </tr>
            <tr>
                <td><code>overnight_surcharge</code></td>
                <td>Binary</td>
                <td>1 if pickup between 8PM-6AM</td>
            </tr>
            <tr>
                <td><code>rush_hour_surcharge</code></td>
                <td>Binary</td>
                <td>1 if pickup during rush hour (4PM-8PM weekdays)</td>
            </tr>
            <tr>
                <td><code>efficiency_ratio</code></td>
                <td>Engineered</td>
                <td>Ratio of actual fare to expected fare by distance</td>
            </tr>
        </table>

        <!-- Project Structure -->
        <h2 id="project-structure"><span class="emoji">📁</span> Project Structure</h2>
        <div class="folder-structure">
<pre>nyc-green-taxi-tip-prediction/
│
├── 📂 data/
│   ├── 2018_Green_Taxi_Trip_Data.csv
│   └── taxi_zone_lookup.csv
│
├── 📂 plots/
│   ├── 01_tip_distribution.png
│   ├── 02_fare_amount_histogram.png
│   ├── 03_trip_distance_histogram.png
│   ├── 04_mse_vs_k.png
│   ├── 05_actual_vs_predicted.png
│   ├── 06_efficiency_heatmap.png
│   ├── 07_efficiency_weekday_weekend.png
│   ├── 08_airport_trips_by_hour.png
│   └── 09_short_rides_by_hour.png
│
├── 📄 taxi_tip_prediction.Rmd
├── 📄 taxi_tip_prediction.html
├── 📄 README.md
└── 📄 LICENSE</pre>
        </div>

        <!-- Installation -->
        <h2 id="installation"><span class="emoji">🛠️</span> Installation</h2>
        
        <h3>Prerequisites</h3>
        <ul>
            <li>R (version 4.0 or higher)</li>
            <li>RStudio (recommended)</li>
        </ul>

        <h3>Required Packages</h3>
        <pre>
# Install required packages
install.packages(c(
  "tidyverse",
  "lubridate",
  "psych",
  "correlation",
  "caret",
  "FNN"
))</pre>

        <h3>Clone Repository</h3>
        <pre>
git clone https://github.com/yourusername/nyc-green-taxi-tip-prediction.git
cd nyc-green-taxi-tip-prediction</pre>

        <!-- Methodology -->
        <h2 id="methodology"><span class="emoji">🔬</span> Methodology</h2>
        <p>This project follows the <strong>CRISP-DM</strong> (Cross-Industry Standard Process for Data Mining) framework:</p>

        <h3>1. Business Understanding</h3>
        <ul>
            <li>Predict tip amounts to help drivers optimize earnings</li>
            <li>Identify factors that influence tipping behavior</li>
        </ul>

        <h3>2. Data Understanding & Exploration</h3>
        
        <div class="plot-placeholder">
            <div class="icon">📊</div>
            <p><strong>Plot: Tip Amount Distribution</strong></p>
            <p><em>plots/01_tip_distribution.png</em></p>
            <p>Right-skewed distribution with many $0 tips</p>
        </div>

        <table>
            <tr>
                <th colspan="2">Tip Amount Summary Statistics</th>
            </tr>
            <tr><td>Minimum</td><td>$0.00</td></tr>
            <tr><td>Median</td><td>$1.58</td></tr>
            <tr><td>Mean</td><td>$1.88</td></tr>
            <tr><td>Maximum</td><td>$50.00</td></tr>
        </table>

        <h3>3. Data Preparation</h3>
        
        <h4>Cleaning Steps</h4>
        <table>
            <tr>
                <th>Step</th>
                <th>Action</th>
                <th>Impact</th>
            </tr>
            <tr>
                <td>1</td>
                <td>Remove missing values</td>
                <td>~8 rows removed</td>
            </tr>
            <tr>
                <td>2</td>
                <td>Keep credit card payments only</td>
                <td>~462,566 rows removed</td>
            </tr>
            <tr>
                <td>3</td>
                <td>Filter trip duration (1-180 min)</td>
                <td>~27,000 rows removed</td>
            </tr>
            <tr>
                <td>4</td>
                <td>Remove invalid passenger counts (>6)</td>
                <td>3 rows removed</td>
            </tr>
            <tr>
                <td>5</td>
                <td>Remove incorrect dates (2009)</td>
                <td>9 rows removed</td>
            </tr>
            <tr>
                <td>6</td>
                <td>Remove zero-distance anomalies</td>
                <td>~415 rows removed</td>
            </tr>
            <tr>
                <td>7</td>
                <td>Remove tips >35% of fare</td>
                <td>~21,000 rows removed</td>
            </tr>
            <tr>
                <td>8</td>
                <td>Remove tolls >$25</td>
                <td>17 rows removed</td>
            </tr>
        </table>

        <h4>Feature Engineering</h4>
        <pre>
# Created new features
trip_duration_minutes  <- difftime(dropoff, pickup, units="mins")
speed_of_taxi          <- trip_distance / (trip_duration_minutes / 60)
efficiency_ratio       <- (fare_amount - 2.5) / (trip_distance * 2.5)
overnight_surcharge    <- ifelse(hour >= 20 | hour < 6, 1, 0)
rush_hour_surcharge    <- ifelse(hour >= 16 & hour < 20 & weekday, 1, 0)</pre>

        <h4>Normalization Pipeline</h4>
        <ol>
            <li><strong>Log transformation</strong> → For skewed variables (distance, fare, speed)</li>
            <li><strong>Min-Max scaling</strong> → Scale all features to [0, 1] range</li>
        </ol>

        <h3>4. Modeling</h3>
        
        <div class="highlight">
            <h3>Algorithm: k-Nearest Neighbors (k-NN) Regression</h3>
            <p><strong>Why k-NN?</strong></p>
            <ul>
                <li>Non-parametric (no assumptions about data distribution)</li>
                <li>Intuitive interpretation</li>
                <li>Works well with normalized numerical features</li>
            </ul>
        </div>

        <h4>Selected Features</h4>
        <table>
            <tr>
                <th>Included ✓</th>
                <th>Excluded ✗ (Low Correlation)</th>
            </tr>
            <tr>
                <td>passenger_count</td>
                <td>VendorID (-0.03)</td>
            </tr>
            <tr>
                <td>log_trip_distance</td>
                <td>PULocationID (0.01)</td>
            </tr>
            <tr>
                <td>log_fare_amount</td>
                <td>extra (0.03)</td>
            </tr>
            <tr>
                <td>log_total_amount</td>
                <td>mta_tax (-0.07)</td>
            </tr>
            <tr>
                <td>efficiency_ratio</td>
                <td>pickup_day (0.01)</td>
            </tr>
            <tr>
                <td>log_speed_of_taxi</td>
                <td>pickup_hour (0.02)</td>
            </tr>
            <tr>
                <td>overnight_surcharge</td>
                <td>-</td>
            </tr>
            <tr>
                <td>rush_hour_surcharge</td>
                <td>-</td>
            </tr>
        </table>

        <p><strong>Train/Test Split:</strong> 70% / 30%</p>

        <h3>5. Evaluation</h3>
        
        <div class="plot-placeholder">
            <div class="icon">📈</div>
            <p><strong>Plot: MSE vs Number of Neighbors (k)</strong></p>
            <p><em>plots/04_mse_vs_k.png</em></p>
            <p>Optimal k = 5 with lowest MSE</p>
        </div>

        <!-- Results -->
        <h2 id="results"><span class="emoji">📈</span> Results</h2>
        
        <div class="metrics-grid">
            <div class="metric-card">
                <div class="value">5</div>
                <div class="label">Optimal k</div>
            </div>
            <div class="metric-card">
                <div class="value">0.000163</div>
                <div class="label">MSE (normalized)</div>
            </div>
            <div class="metric-card">
                <div class="value">372,298</div>
                <div class="label">Training Samples</div>
            </div>
            <div class="metric-card">
                <div class="value">159,557</div>
                <div class="label">Test Samples</div>
            </div>
        </div>

        <h3>Prediction Quality by Tip Range</h3>
        <table>
            <tr>
                <th>Tip Range</th>
                <th>Performance</th>
                <th>Rating</th>
            </tr>
            <tr>
                <td>$0 - $5</td>
                <td>Good</td>
                <td class="star-rating">⭐⭐⭐⭐</td>
            </tr>
            <tr>
                <td>$5 - $15</td>
                <td>Excellent</td>
                <td class="star-rating">⭐⭐⭐⭐⭐</td>
            </tr>
            <tr>
                <td>$15 - $25</td>
                <td>Moderate</td>
                <td class="star-rating">⭐⭐⭐</td>
            </tr>
            <tr>
                <td>> $25</td>
                <td>Underestimates</td>
                <td class="star-rating">⭐⭐</td>
            </tr>
        </table>

        <div class="plot-placeholder">
            <div class="icon">🎯</div>
            <p><strong>Plot: Actual vs Predicted Tip Amounts</strong></p>
            <p><em>plots/05_actual_vs_predicted.png</em></p>
            <p>Points near diagonal line indicate accurate predictions</p>
        </div>

        <h3>Example Prediction</h3>
        <div class="insight-box">
            <pre style="background: transparent; color: #333; padding: 0;">
Test Example #5:
├── Predicted tip: $4.94
├── Actual tip:    $4.96
└── Error:         $0.02 (0.4%)</pre>
        </div>

        <!-- Key Insights -->
        <h2 id="insights"><span class="emoji">💡</span> Key Insights</h2>

        <h3>1. 🕐 Optimal Operating Hours</h3>
        <div class="insight-box">
            <strong>Finding:</strong> Best operational efficiency occurs <strong>7AM-6PM, Monday-Friday</strong>
        </div>

        <div class="plot-placeholder">
            <div class="icon">🗓️</div>
            <p><strong>Plot: Efficiency Heatmap by Hour and Day</strong></p>
            <p><em>plots/06_efficiency_heatmap.png</em></p>
        </div>

        <table>
            <tr>
                <th>Time Period</th>
                <th>Weekday Efficiency</th>
                <th>Weekend Efficiency</th>
                <th>Difference</th>
            </tr>
            <tr>
                <td>6-9 AM</td>
                <td>1.42</td>
                <td>1.38</td>
                <td>+2.9%</td>
            </tr>
            <tr>
                <td>9-12 PM</td>
                <td>1.45</td>
                <td>1.40</td>
                <td>+3.6%</td>
            </tr>
            <tr>
                <td>12-3 PM</td>
                <td>1.44</td>
                <td>1.41</td>
                <td>+2.1%</td>
            </tr>
            <tr>
                <td>3-6 PM</td>
                <td>1.43</td>
                <td>1.39</td>
                <td>+2.9%</td>
            </tr>
            <tr>
                <td>6-9 PM</td>
                <td>1.38</td>
                <td>1.37</td>
                <td>+0.7%</td>
            </tr>
        </table>

        <h3>2. ✈️ Early Morning Airport Rush</h3>
        <div class="insight-box">
            <strong>Finding:</strong> 5AM efficiency dip caused by long airport trips
        </div>

        <div class="plot-placeholder">
            <div class="icon">✈️</div>
            <p><strong>Plot: Airport Trips by Hour</strong></p>
            <p><em>plots/08_airport_trips_by_hour.png</em></p>
        </div>

        <table>
            <tr>
                <th>Rank</th>
                <th>5AM Drop-off Location</th>
                <th>Trip Count</th>
            </tr>
            <tr>
                <td>1</td>
                <td>LaGuardia Airport</td>
                <td>223</td>
            </tr>
            <tr>
                <td>2</td>
                <td>JFK Airport</td>
                <td>120</td>
            </tr>
            <tr>
                <td>3</td>
                <td>Upper East Side North</td>
                <td>79</td>
            </tr>
            <tr>
                <td>4</td>
                <td>Midtown Center</td>
                <td>72</td>
            </tr>
            <tr>
                <td>5</td>
                <td>Times Square</td>
                <td>63</td>
            </tr>
        </table>

        <p><strong>5AM Passenger Profile:</strong> 84% solo travelers (likely commuters), Average distance: 5.2 miles</p>

        <h3>3. 🚗 Evening Traffic Impact</h3>
        <div class="warning-box">
            <strong>Finding:</strong> Post-6PM efficiency drop due to short/aborted rides caused by traffic congestion
        </div>

        <div class="plot-placeholder">
            <div class="icon">🚗</div>
            <p><strong>Plot: Short Rides (&lt;1 mile) by Hour</strong></p>
            <p><em>plots/09_short_rides_by_hour.png</em></p>
        </div>

        <table>
            <tr>
                <th>Hour</th>
                <th>Short Rides Count</th>
                <th>% of Daily</th>
            </tr>
            <tr>
                <td>6 PM</td>
                <td>4,521</td>
                <td>8.2%</td>
            </tr>
            <tr style="background-color: #fff3e0;">
                <td><strong>7 PM</strong></td>
                <td><strong>4,892</strong></td>
                <td><strong>8.9% ← Peak</strong></td>
            </tr>
            <tr>
                <td>8 PM</td>
                <td>4,234</td>
                <td>7.7%</td>
            </tr>
            <tr>
                <td>9 PM</td>
                <td>3,876</td>
                <td>7.0%</td>
            </tr>
        </table>

        <h3>4. 💰 Tipping Patterns</h3>
        <table>
            <tr>
                <th>Tip Percentage</th>
                <th>% of Credit Card Trips</th>
            </tr>
            <tr>
                <td>0% (No tip)</td>
                <td>~40%</td>
            </tr>
            <tr>
                <td>1-15%</td>
                <td>~25%</td>
            </tr>
            <tr>
                <td>15-20% (Standard)</td>
                <td>~20%</td>
            </tr>
            <tr>
                <td>20-30% (Generous)</td>
                <td>~12%</td>
            </tr>
            <tr>
                <td>>30% (Outliers)</td>
                <td>~3%</td>
            </tr>
        </table>

        <div class="warning-box">
            <strong>Note:</strong> Cash tips are NOT recorded in the dataset. Only credit card payments have tip data.
        </div>

        <!-- Future Improvements -->
        <h2><span class="emoji">🔮</span> Future Improvements</h2>
        <table>
            <tr>
                <th>Improvement</th>
                <th>Description</th>
                <th>Priority</th>
            </tr>
            <tr>
                <td>🌲 Random Forest</td>
                <td>Try ensemble methods for better accuracy</td>
                <td>High</td>
            </tr>
            <tr>
                <td>📍 Location Encoding</td>
                <td>Include pickup/dropoff zone features</td>
                <td>High</td>
            </tr>
            <tr>
                <td>🌧️ Weather Data</td>
                <td>Add external weather conditions</td>
                <td>Medium</td>
            </tr>
            <tr>
                <td>📈 Time Series</td>
                <td>Capture seasonal/monthly patterns</td>
                <td>Medium</td>
            </tr>
            <tr>
                <td>🌐 API Deployment</td>
                <td>Create REST API for real-time predictions</td>
                <td>Low</td>
            </tr>
        </table>

        <!-- References -->
        <h2 id="references"><span class="emoji">📚</span> References</h2>
        <ol>
            <li>
                <strong>NYC TLC Trip Data</strong><br>
                NYC Taxi & Limousine Commission (2018)<br>
                <a href="https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page">https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page</a>
            </li>
            <li>
                <strong>NYC Taxi Regulations</strong><br>
                NYC311 - Taxis<br>
                <a href="https://portal.311.nyc.gov/article/?kanumber=KA-01245">https://portal.311.nyc.gov/article/?kanumber=KA-01245</a>
            </li>
            <li>
                <strong>NYC Taxi Fare Structure</strong><br>
                NYC TLC (2019) - Archived<br>
                <a href="https://web.archive.org/web/20190722151033/https://www.nyc.gov/site/tlc/passengers/taxi-fare.page">Archive Link</a>
            </li>
            <li>
                <strong>NYC Traffic Study</strong><br>
                Corrado, K. (2021). PIX11 News<br>
                <a href="https://pix11.com/news/local-news/nyc-worst-traffic-in-country-study-finds/">https://pix11.com/news/local-news/nyc-worst-traffic-in-country-study-finds/</a>
            </li>
        </ol>

        <!-- Author -->
        <h2><span class="emoji">👤</span> Author</h2>
        <p>
            <strong>Your Name</strong><br>
            <a href="https://github.com/yourusername" class="btn">GitHub</a>
            <a href="https://linkedin.com/in/yourprofile" class="btn">LinkedIn</a>
        </p>

        <!-- License -->
        <h2><span class="emoji">📄</span> License</h2>
        <p>This project is licensed under the MIT License - see the LICENSE file for details.</p>

        <!-- Footer -->
        <footer>
            <p><strong>⭐ Star this repo if you found it helpful! ⭐</strong></p>
            <p style="margin-top: 10px; font-size: 14px;">
                NYC Taxi & Limousine Commission for open data | R community for excellent packages | CRISP-DM framework
            </p>
        </footer>
    </div>
</body>
</html>
