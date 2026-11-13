# Hospital Appointment System

A simple hospital appointment booking system built with a C++ backend and a frontend web interface. The application allows patients to book appointments, search for records, cancel bookings, and view appointment summaries.

## Features

- Book a new appointment
- Search appointment by ID
- View all appointments
- Cancel an existing appointment
- Export saved appointment records to a text file
- Lightweight REST API using C++ and Crow
- Responsive web UI using HTML, CSS, and JavaScript

## Tech Stack

- C++17
- Crow (C++ web framework)
- CMake
- vcpkg
- HTML, CSS, JavaScript
- Windows + VS Code development workflow

## Project Structure

```text
Hospital_Appointment_System_Full_Project/
├── CMakeLists.txt
├── README.md
├── vcpkg.json
├── backend/
│   └── main.cpp
├── frontend/
│   ├── index.html
│   ├── script.js
│   └── style.css
├── build/
└── appointments.txt   (generated at runtime)
```

## Prerequisites

Before running the project, make sure you have:

- Windows
- VS Code
- Git
- CMake
- C++17 compiler
- vcpkg

## Setup Instructions

### 1. Clone or download the project

```bash
git clone <your-repository-url>
cd Hospital_Appointment_System_Full_Project
```

### 2. Set up vcpkg

If your vcpkg installation is in `C:\vcpkg`, run:

```powershell
$env:VCPKG_ROOT = "C:\vcpkg"
```

If it is in another location, replace the path accordingly.

Verify that the toolchain file exists:

```powershell
Test-Path "$env:VCPKG_ROOT\scripts\buildsystems\vcpkg.cmake"
```

It should return `True`.

### 3. Install dependencies

From the project root:

```powershell
& "$env:VCPKG_ROOT\vcpkg.exe" install
```

### 4. Configure and build the backend

```powershell
cmake -S . -B build -DCMAKE_TOOLCHAIN_FILE="$env:VCPKG_ROOT\scripts\buildsystems\vcpkg.cmake"
cmake --build build --config Release
```

### 5. Run the backend

```powershell
.\build\Release\hospital_backend.exe
```

The backend will run on:

```text
http://localhost:18080
```

### 6. Run the frontend

Open the frontend file in VS Code:

```text
frontend/index.html
```

If you have Live Server installed, right-click the file and choose `Open with Live Server`.

## API Endpoints

| Method | Endpoint | Description |
|---|---|---|
| GET | `/api/health` | Checks if the backend is running |
| GET | `/api/appointments` | Returns all appointments |
| POST | `/api/appointments` | Creates a new appointment |
| GET | `/api/appointments/{id}` | Fetches a specific appointment |
| POST | `/api/appointments/{id}/cancel` | Cancels an appointment |

## Example Request

### Create an appointment

```http
POST /api/appointments
Content-Type: application/json

{
  "name": "John Doe",
  "age": 32,
  "doctor": "Dr. Smith",
  "date": "2026-11-12",
  "time": "10:30"
}
```

### Health check

```http
GET /api/health
```

## Notes

- Appointments are stored in memory while the server is running.
- Booking and cancellation actions are appended to `appointments.txt` in the backend working directory.
- CORS is intentionally open for local testing/demo use only.
- This project is intended for educational or local demonstration purposes and should not be deployed publicly without additional security and validation work.

## Troubleshooting

- If `cmake` is not recognized, install CMake and reopen VS Code.
- If Crow is not found, confirm that `VCPKG_ROOT` is set correctly and run `vcpkg install` again.
- If the browser cannot connect to the API, ensure the backend is running on port `18080`.

## License

This project is intended for educational and demonstration purposes. Add a license file if you want to publish it publicly.
