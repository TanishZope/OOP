HOSPITAL APPOINTMENT SYSTEM — FRONTEND + C++ BACKEND

CONTENTS
frontend/index.html, style.css, script.js
backend/main.cpp
CMakeLists.txt
vcpkg.json

REQUIREMENTS
Windows, VS Code, working C++17 compiler, CMake, Git, vcpkg.
Crow is installed through the vcpkg manifest.

1. EXTRACT AND OPEN
Extract this ZIP. In VS Code choose File > Open Folder and select the extracted project folder.

2. SET VCPKG LOCATION IN THE VS CODE POWERSHELL TERMINAL
If vcpkg is in C:\vcpkg:
  $env:VCPKG_ROOT="C:\vcpkg"
If vcpkg is in D:\vcpkg:
  $env:VCPKG_ROOT="D:\vcpkg"

Check the location:
  Test-Path "$env:VCPKG_ROOT\scripts\buildsystems\vcpkg.cmake"
It should return True.

3. INSTALL CROW
Run from the project root (the folder containing vcpkg.json):
  & "$env:VCPKG_ROOT\vcpkg.exe" install

4. BUILD THE BACKEND
  cmake -S . -B build -DCMAKE_TOOLCHAIN_FILE="$env:VCPKG_ROOT/scripts/buildsystems/vcpkg.cmake"
  cmake --build build --config Release

5. RUN THE BACKEND
  .\build\Release\hospital_backend.exe
Keep this terminal open. The server listens at http://localhost:18080.

6. TEST THE BACKEND
Open http://localhost:18080/api/health in Chrome. You should see JSON saying the C++ backend is running.

7. RUN THE FRONTEND
In VS Code, open frontend/index.html. If you have the Live Server extension, right-click it and select Open with Live Server. Keep both the C++ server and Live Server running. Use the website to book, search, view and cancel appointments.

API ROUTES
GET  /api/health
GET  /api/appointments
POST /api/appointments
GET  /api/appointments/{id}
POST /api/appointments/{id}/cancel

IMPORTANT PROJECT NOTES
This is a web-ready C++ backend starter implementing the appointment operations and fields from your supplied console project. It is not a direct automatic conversion of your original console-menu source file; the console cin/cout menu is replaced by HTTP routes.
Appointments are held in memory while the server runs. New booking and cancellation events are appended to appointments.txt in the backend process working directory. This starter does not reload old appointments from the text file after restarting the server.
CORS is open for local classroom demonstration only. Do not deploy this configuration publicly. Do not enter real patient/private medical data.

TROUBLESHOOTING
- If CMake is not recognized, install CMake and reopen VS Code.
- If Crow is not found, check VCPKG_ROOT and run the vcpkg install command from the project root.
- If the webpage cannot connect, ensure hospital_backend.exe is running on port 18080 and launch the page with Live Server.
