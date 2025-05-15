# Cyclist Power & Speed Tracker

A responsive web app to **track and analyze cycling power and speed in real-time**, using GPS (or simulation), elevation, and live wind data. The app supports automatic estimation of rider drag based on terrain, and generates full-session analytics and downloadable CSV files for further analysis.


## Features

* **Real-time Sampling:** Records location, elevation, and wind every 5 seconds (configurable for API limitations).
* **Flexible Data Input:** Use browser GPS (for outdoor rides) or simulation mode (for testing or demos).
* **Auto Pose Option:**

  * Automatically adjusts the drag area (CdA) based on the gradient: upright on climbs, hoods on flats, drops on descents.
  * Or, use a fixed user-specified CdA.
* **Physics-based Calculation:** Computes cyclist power and speed at each interval using standard cycling dynamics (accounts for gradient, rolling resistance, wind, and more).
* **Session Analytics:**

  * Live display of recent power, speed, wind, gradient, and current CdA.
  * End-of-session summary: average power, speed, calories burned, total elevation gain.
* **Export to CSV:** Download a file with all recorded sample points and computed values.
* **Polished, Responsive UI:** Looks great and works well on both desktop and mobile.

## How it Works

1. **Select your data mode:**

   * *Simulate:* The app generates a realistic virtual ride over hilly terrain.
   * *Use GPS:* Uses your device's location (requires browser permission).
2. **Input your parameters:**
   Rider mass, bike mass, drag area (CdA), and rolling resistance (CRR).
   Enable “Auto Pose” if you want the drag area to adjust automatically.
3. **Start your session:**
   The app samples your position and local wind every 5 seconds, computes power and speed, and updates the display.
4. **Stop your session:**
   View summary analytics and download your session data as CSV.

## Running the App

1. **Download the `cyclist_tracker.html` file** from this repository.
2. **Open the file in your browser** (desktop or mobile).
3. **Grant location access** if using GPS mode.

> **Note:**
>
> * Live elevation and wind are fetched from [Open-Meteo](https://open-meteo.com/).
> * In GPS mode, the app’s accuracy depends on your device and outdoor signal.

## Calculation Details

* **Power is computed as:**
  `Power = (Gravity Force + Rolling Resistance + Aerodynamic Drag) × Speed`
* **Drag area (CdA) varies** with rider position if “Auto Pose” is enabled:

  * Climbing (gradient > +3%): upright (CdA = 0.40 m²)
  * Descending (gradient < -3%): drops (CdA = 0.28 m²)
  * Flat: hoods (CdA = 0.32 m²)
* **Calories burned** use a typical gross mechanical efficiency (23%).

## API Limits and Privacy

* **Elevation and wind data:** Queried from Open-Meteo APIs (500 daily requests per IP is their free tier).
* **No data is uploaded or stored externally.** Everything runs in your browser and stays on your device.

## Example Output

The downloadable CSV includes:
`timestamp, latitude, longitude, altitude, power, speed, cda, gradient`

## Troubleshooting

* **GPS mode not working?**

  * Make sure you allow location access in your browser.
  * Try outdoors for best results.
* **API errors?**

  * Too many sessions in a day may exceed Open-Meteo’s free API quota.

## License

MIT License.

---

## Acknowledgments

* [Open-Meteo](https://open-meteo.com/) for free elevation and wind APIs.
* [OpenAI ChatGPT](https://openai.com/) for assistance in designing this project.
