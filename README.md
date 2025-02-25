#include <iostream>
#include <vector>
#include <string>
#include <thread>
#include <chrono>

class ThermalCamera {
public:
    void initialize() {
        std::cout << "Thermal Camera Initialized." << std::endl;
    }

    std::vector<std::string> detectHeatSources() {
        // Simulated heat source detection
        return {"Fire", "Human", "Animal"};
    }
};

class Drone {
private:
    ThermalCamera camera;
    bool isFlying;

public:
    Drone() : isFlying(false) {}

    void takeOff() {
        isFlying = true;
        std::cout << "Drone is taking off." << std::endl;
    }

    void land() {
        isFlying = false;
        std::cout << "Drone is landing." << std::endl;
    }

    void flyToLocation(double latitude, double longitude) {
        if (isFlying) {
            std::cout << "Flying to location: (" << latitude << ", " << longitude << ")" << std::endl;
        } else {
            std::cout << "Drone must be in the air to fly to a location." << std::endl;
        }
    }

    void scanForFires() {
        if (isFlying) {
            camera.initialize();
            std::vector<std::string> heatSources = camera.detectHeatSources();
            for (const auto& source : heatSources) {
                if (source == "Fire") {
                    std::cout << "Fire detected! Activating firefighting protocol." << std::endl;
                    extinguishFire();
                }
            }
        } else {
            std::cout << "Drone must be in the air to scan for fires." << std::endl;
        }
    }

    void extinguishFire() {
        std::cout << "Extinguishing fire..." << std::endl;
        std::this_thread::sleep_for(std::chrono::seconds(2));
        std::cout << "Fire extinguished." << std::endl;
    }
};

int main() {
    Drone firefightingDrone;
    firefightingDrone.takeOff();
    firefightingDrone.flyToLocation(34.0522, -118.2437);
    firefightingDrone.scanForFires();
    firefightingDrone.land();
    return 0;
}
