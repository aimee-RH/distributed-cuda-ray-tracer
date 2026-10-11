# Distributed CUDA Ray Tracer

A C++17 and CUDA course project that renders image tiles on GPU workers and assembles them in an SFML coordinator over UDP.

## What this version implements

- One CUDA thread per pixel in a 16 x 16 thread block, with ray-sphere intersection, direct lighting, shadow rays, and a sky gradient.
- Per-tile device allocation, kernel execution, and device-to-host RGBA transfer.
- UDP worker registration, tile dispatch, timeout re-queuing, result collection, and progressive image display.

The project began from a Georgia Tech ECE 4122/6122 assignment scaffold. The packet types, scene setup, tile queue construction, and parts of the SFML and CUDA setup were supplied. The implementation fills in the rendering, worker communication, and coordinator scheduling sections.

## Build environment

The original CMake configuration targets CUDA 12, C++17, SFML 2.6, and NVIDIA compute capability 8.0 (A100). It refers to a local `../SFML` installation and may need path changes on another machine. A CUDA build and runtime benchmark have not yet been verified in this repository.

## Next improvements

The current worker allocates and frees a GPU pixel buffer for each tile. A useful next experiment is to reuse one buffer per worker, then measure allocation time, kernel time, transfer time, and end-to-end render time before claiming a speedup.
