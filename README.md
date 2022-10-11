# Mandelbrot-On-FPGA
A Mandelbrot Set Explorer implemented entirely in Hardware in SystemVerilog. Made to run on a DE 10 Lite FPGA. This was my final project for ECE 385: Digital Systems Laboratory at the University of Illinois.

The Mandelbrot Set Explorer supports multiple color palettes, horizontal and vertical panning, and zooming into and out of the set. Additionally, the user can change the resolution of the set.

The set is calculated using a simple escape time algorithm, and the resolution is changed by altering the number of maximum iterations of calculation for each pixel on the screen.

One of the core features of this project is its use of multithreading. Multiple threads are used to calculate portions of the screen in parallel, offering a massive speedup.

Each color palette used by the project only supports 16 different colors. This limitation was due to the limited on-chip-memory available on the DE10 Lite FPGA. The palettes are indexed using a portion of the binary string for the number of iterations before convergence for each pixel.

This project does have some key flaws. Although somewhat rare, it is possible to find timing artifacts in the Mandelbrot set. Additionally, some glitches can occur where the user accidentally pans much further than intended, or where certain threads (sometimes all threads) will fail. These glitches are due to timing issues in the project. Timing is not properly constrained, and I did not have time to flesh out timing when I did the project for ECE 385. Overflow is also visible on the outside of the Mandelbrot set for certain color palettes.

If I were to do this project again, I might use a better escape time algorithm that supports resolution gain at higher-detail areas without resolution loss in already-rendered areas. One example of away todo this. is by using a cyclic color palette and using a modulus to calculate the color of each pixel rather than using the raw binary string of the number of iterations.
