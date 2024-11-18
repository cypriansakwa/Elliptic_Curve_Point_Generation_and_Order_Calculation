# Elliptic Curve Point Generation and Order Calculation

This Rust program generates all the points on an elliptic curve defined over a finite field and determines the order of each point. The elliptic curve is defined by the equation:

$y^2 = x^3 + ax + b \pmod{p}$

## Table of Contents
- [Overview](#overview)
- [How It Works](#how-it-works)
- [Getting Started](#getting-started)
- [Usage](#usage)
- [Example Output](#example-output)

## Overview
The program performs the following tasks:
1. Generates all points on the elliptic curve modulo a prime $p$.
2. Computes the order of each point by repeatedly adding the point to itself until reaching the point at infinity.

## How It Works
1. **Point Generation**: The function `generate_points_on_curve` finds all the points $(x, y)$ that satisfy the elliptic curve equation modulo $p$.
2. **Point Addition**: The function `add_points` handles both point addition and point doubling on the curve.
3. **Order Calculation**: The function `find_order` determines the order of a point by adding it repeatedly until it reaches the point at infinity.

### Elliptic Curve Equation
The elliptic curve is defined as:

$y^2 \equiv x^3 + ax + b \pmod{p}$

### Point Addition and Doubling
For two points $P_1 = (x_1, y_1)$ and $P_2 = (x_2, y_2)$ on the curve:
- **Point Doubling** (if $P_1 = P_2$):

  $\lambda = \frac{3x_1^2 + a}{2y_1} \pmod{p}$
- **Point Addition** (if $P_1 \neq P_2$):

  $\lambda = \frac{y_2 - y_1}{x_2 - x_1} \pmod{p}$
  
The new point $(x_3, y_3)$ is computed as:

$x_3 = \lambda^2 - x_1 - x_2 \pmod{p}$

$y_3 = \lambda(x_1 - x_3) - y_1 \pmod{p}$

### Modular Inverse
The function `mod_inverse` uses the extended Euclidean algorithm to find the inverse:

$a^{-1} \equiv x \pmod{p}$

## Getting Started
### Prerequisites
- Rust installed on your system. You can download it from [rust-lang.org](https://www.rust-lang.org/).

### Installation
Clone the repository and navigate to the project directory:
```bash
git clone https://github.com/cypriansakwa/Elliptic_Curve_Point_Generation_and_Order_Calculation.git
cd Elliptic_Curve_Point_Generation_and_Order_Calculation
```
## Usage
Compile and run the program using Cargo:
```
cargo run
```
## Example Code
Below is a snippet of the main function:
```
fn main() {
    let a = 4; // coefficient a
    let b = 5; // coefficient b
    let p = 7; // prime modulus

    let points = generate_points_on_curve(a, b, p);
    for point in points {
        let order = find_order(point, a, p);
        println!("Point {:?} modulo {} is of order {}", point, p, order);
    }
}
```
## Example Output
```
Point (2, 0) modulo 7 is of order 2
Point (3, 3) modulo 7 is of order 3
Point (3, 4) modulo 7 is of order 3
Point (4, 1) modulo 7 is of order 6
Point (4, 6) modulo 7 is of order 6
Point (6, 0) modulo 7 is of order 2
