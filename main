
#include <iostream>
#include <vector>
#include <cmath>
#include <iomanip>

using namespace std;

struct Particle {
    double x, y;      // position
    double vx, vy;    // velocity
    bool alive;
};

const double G = 1.0;          // gravitational constant (scaled)
const double M = 500.0;        // black hole mass
const double dt = 0.01;        // time step
const double eventHorizon = 2.0; // radius where particle is absorbed
const int steps = 2000;

void updateParticle(Particle& p) {
    if (!p.alive) return;

    double r = sqrt(p.x * p.x + p.y * p.y);

    // Check if particle falls into the black hole
    if (r <= eventHorizon) {
        p.alive = false;
        return;
    }

    // Gravitational acceleration toward center
    double a = G * M / (r * r);
    double ax = -a * (p.x / r);
    double ay = -a * (p.y / r);

    // Update velocity
    p.vx += ax * dt;
    p.vy += ay * dt;

    // Update position
    p.x += p.vx * dt;
    p.y += p.vy * dt;
}

int main() {
    vector<Particle> particles;

    // Create some particles with different starting positions
    for (int i = 0; i < 5; i++) {
        Particle p;
        p.x = 10.0 + i * 2.0;
        p.y = 0.0;
        p.vx = 0.0;
        p.vy = sqrt(G * M / p.x) * 0.85; // slightly less than orbital speed
        p.alive = true;
        particles.push_back(p);
    }

    for (int step = 0; step < steps; step++) {
        cout << "Step " << step << "\n";

        for (size_t i = 0; i < particles.size(); i++) {
            updateParticle(particles[i]);

            if (particles[i].alive) {
                cout << "Particle " << i
                     << " | x = " << fixed << setprecision(3) << particles[i].x
                     << ", y = " << particles[i].y
                     << ", vx = " << particles[i].vx
                     << ", vy = " << particles[i].vy << "\n";
            } else {
                cout << "Particle " << i << " has fallen into the black hole.\n";
            }
        }

        cout << "---------------------------------\n";
    }

    return 0;
}