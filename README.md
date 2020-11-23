# Real-time FFT Ocean Rendering

Render FFT Ocean using Tessendorf’s model [Tessendorf 2001] with CUDA/MPI

## Introduction

### Ocean Data

1. Displacement texture for vertex position
![image](https://github.com/CyxFTS/CSCI596/blob/main/displacement.jpg?raw=true)
2. Normal texture for vertex normal
3. Jacobian texture for foam calculation

## Number of executions of FFT

1. Displacement texture: 3
2. Normal texture: 2
3. Jacobian texture: 3

## Details

1. Generate 8 spectrums for inverse FFT
2. **(Parallel)** Calculate 8 FFT with cuFFT/MPI+fftw
3. Generate textures for rendering
4. Render

## Result

### Device

CPU: AMD Ryzen 2600X (6 cores 12 threads) 

GPU: Nvdia GeForce RTX 2060 SUPER (2176 CUDA cores)

### Data

Time spent in one frame (60fps min: 0.017 second per frame)

| Mesh Size | CUDA | MPI |Origin|
| ------------ | ------------- | ------------- | ------------- |
| 256 * 256 | 0.017  | 0.017  |0.022
| 512 * 512| 0.017  | 0.091 |0.139
| 1024 * 1024| 0.017  | 0.349  |0.573
| 2048 * 2048 | 0.058  | 1.58  |2.67

## Conclusion
MPI can calculate the scale of 256 in real time on the 60Hz display

CUDA can calculate the scale of 256, 512, 1024 in real time

The original serial calculation cannot meet real-time requirements


Therefore, if the device has a GPU, it is a better choice to use GPU for computing parallel computing-friendly rendering data

## License
[MIT](https://choosealicense.com/licenses/mit/)
