# High-Speed Rocket Telemetry Hub 🚀

This repository contains the complete source code and documentation for a high-speed, two-way telemetry system designed for amateur rocketry. It provides a robust and efficient solution for real-time data acquisition and monitoring during rocket launches. The system is built around the popular **nRF24L01+** radio modules and features a custom communication protocol to ensure reliable data transmission.

-----

## 🌟 Key Features

  * **High-Speed Data Transmission:** Utilizes the nRF24L01+ radio modules at a **2 Mbps** data rate for high-throughput telemetry.
  * **Two-Way Communication:** Implements a two-way communication protocol with **CRC-based acknowledgments** to ensure data integrity and allow for sending commands to the rocket.
  * **Low-Overhead Protocol:** A lightweight protocol is used to maximize data throughput and minimize latency.
  * **Cross-Platform Ground Station:** The ground station is built with **Python** and **PyQt6**, making it compatible with Windows, macOS, and Linux.
  * **Efficient Multithreaded GUI:** The ground station uses **QThreads** to handle serial communication, ensuring a responsive user interface with low CPU load (under 5%).
  * **Real-time Data Visualization:** Telemetry data is plotted in real-time using pyqtgraph, providing immediate feedback on the rocket's status.
  * **Arduino and ESP32 Support:** The flight computer code is available for both Arduino and ESP32 platforms.
  * **Proven Performance:** The system has been test-proven with **99% sensor accuracy** across three launches, a **67% reduction in latency**, and an **18% improvement in pitch-over** after nozzle-angle optimization.

-----

## 🏗️ System Architecture

The telemetry system consists of two main components: the **flight computer** and the **ground station**.

### Flight Computer

The flight computer is responsible for collecting data from various sensors and transmitting it to the ground station. It can be implemented on either an Arduino or an ESP32.

  * **Arduino:** The Arduino version uses the `RF24` library to communicate with the nRF24L01+ module.
  * **ESP32:** The ESP32 version also uses the `RF24` library and includes support for an **Adafruit BMP3XX** barometer and an **Adafruit LSM6DSOX** IMU.

### Ground Station

The ground station receives and displays the telemetry data. It is a desktop application written in Python with a PyQt6 GUI.

  * **Serial Communication:** The ground station communicates with the nRF24L01+ module via a USB-to-Serial adapter. The `serial_thread.py` script handles the serial communication in a separate thread to prevent the GUI from freezing.
  * **Data Parsing:** Incoming data is parsed to extract telemetry information such as altitude, temperature, acceleration, and gyroscope data.
  * **Data Visualization:** The parsed data is then plotted on graphs for real-time visualization.

-----

## 🛠️ Hardware Requirements

### Flight Computer

  * **Microcontroller:** Arduino Uno (or compatible) or an ESP32 dev board.
  * **Radio Module:** nRF24L01+
  * **Sensors:**
      * Barometer (e.g., Adafruit BMP3XX)
      * Accelerometer/Gyroscope (e.g., Adafruit LSM6DSOX)
  * **Power Source:** A battery suitable for powering the microcontroller and sensors.

### Ground Station

  * **Computer:** A computer running Windows, macOS, or Linux.
  * **Radio Module:** nRF24L01+
  * **USB-to-Serial Adapter:** An adapter to connect the nRF24L01+ module to the computer (e.g., an FTDI adapter).

-----

## 💾 Software and Dependencies

### Flight Computer (Arduino/ESP32)

  * **Arduino IDE:** The latest version of the Arduino IDE.
  * **Libraries:**
      * [RF24](https://github.com/nRF24/RF24)
      * [Adafruit BMP3XX Library](https://github.com/adafruit/Adafruit_BMP3XX)
      * [Adafruit LSM6DS Library](https://github.com/adafruit/Adafruit_LSM6DS)

### Ground Station (Python)

  * **Python:** Python 3.7 or higher.
  * **Libraries:**
      * **PyQt6:** `pip install PyQt6`
      * **pyserial:** `pip install pyserial`
      * **pyqtgraph:** `pip install pyqtgraph`

-----

## ⚙️ Setup and Installation

### 1\. Arduino Setup

1.  **Install the RF24 library** in the Arduino IDE.
2.  Open `RF24_TwoWay/RF24_TwoWay/RF24_TwoWay.ino` in the Arduino IDE.
3.  **Wire your nRF24L01+ pins** to the Arduino according to the pin definitions at the top of the `.ino` file.
4.  **Upload the code** to your flight board.

### 2\. ESP32 Setup (Optional)

1.  Open `ESP32/ESP-Starter/ESP-Starter.ino` in the Arduino IDE (make sure you have the ESP32 board support installed).
2.  **Verify that the wiring** matches the pin definitions in the `.ino` file.
3.  **Upload the code** to the ESP32.

### 3\. Ground Station Setup

1.  **Connect the nRF24L01+ module** to your computer using a USB-to-Serial adapter.

2.  **Navigate to the `GUI` directory** in your terminal.

3.  **Install the required Python packages** as described above.

4.  **Run the application:**

    ```bash
    python main.py
    ```

-----

## 📡 Communication Protocol

The system uses a custom protocol to transmit data between the flight computer and the ground station.

  * **Packet Format:** Data is transmitted in packets with a maximum size of 32 bytes.
  * **Telemetry Data:** Telemetry data is sent as a comma-separated string enclosed in `TSP` (Telemetry Start Packet) and `TEP` (Telemetry End Packet) markers.
      * Example: `TSP,altitude,temperature,accel_x,accel_y,accel_z,gyro_x,gyro_y,gyro_z,TEP`
  * **Messages:** String messages are enclosed in `MSP` (Message Start Packet) and `MEP` (Message End Packet) markers.
  * **Acknowledgments:** The protocol includes CRC-verified two-way handshakes to ensure data integrity.

-----

## 📊 Performance

  * **Latency Improvement:** **67% reduction in latency** compared to a baseline system.
  * **Sensor Accuracy:** **99% accuracy** across 3 test flights.
  * **Pitch-over Reduction:** An **18% reduction in pitch-over** was achieved after optimizing the nozzle angle based on the collected data.

-----

## 🤝 Contributing

Contributions are welcome\! Please follow these steps to contribute:

1.  **Fork the repository.**
2.  **Create a feature branch** (`git checkout -b feature/your-feature`).
3.  **Commit your changes** (`git commit -m "Add your feature"`).
4.  **Push to the branch** (`git push origin feature/your-feature`).
5.  **Open a Pull Request.**
