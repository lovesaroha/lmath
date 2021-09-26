# lmath
This is a generalized math package with clean and transparent API for the Go language.
Also available for javascript [github/lovesaroha/lmath.js](https://github.com/lovesaroha/lmath.js) 

## Features
- Lightweight and Fast.
- Native Go implementation.

## Requirements
- Go 1.9 or higher. We aim to support the 3 latest versions of Go.

## Installation
Simple install the package to your [$GOPATH](https://github.com/golang/go/wiki/GOPATH "GOPATH") with the [go tool](https://golang.org/cmd/go/ "go command") from shell:
```bash
go get -u github.com/lovesaroha/lmath
```
Make sure [Git is installed](https://git-scm.com/downloads) on your machine and in your system's `PATH`.

## Usage

### Random

```Golang
  // Random float64 between given range.
  random := lmath.Random(-1, 1)
```

### Map Given Value Between Given Range
```Golang
  // Return float64 between given range of (200, 1000).
  result := lmath.Map(20 , 0, 100, 200, 1000)
```

## Apply Math Functions
```Golang
  // Sigmoid.
  result := lmath.Sigmoid(1.5)
  // Diff of sigmoid.
  dresult := lmath.Dsigmoid(result)
  // Relu.
  result := lmath.Relu(2)
  // Diff of relu.
  dresult := lmath.Drelu(result)
```

### Create Matrix 

```Golang
  // Create a matrix (rows, cols).
  matrix := lmath.Matrix(4, 3)

  // Print matrix shape.
  matrix.Shape()
  // Print matrix values.
  matrix.Print()

```
![image](https://raw.githubusercontent.com/lovesaroha/gimages/main/38.png)

### Create Random Matrix 

```Golang
  // Create a matrix (rows, cols, minimum , maximum).
  matrix := lmath.Matrix(3, 4, -1 , 1)

  // Print matrix shape.
  matrix.Shape()
  // Print matrix values.
  matrix.Print()
```
![image](https://raw.githubusercontent.com/lovesaroha/gimages/main/39.png)

### Convert Slice Into Matrix 

```Golang
    // Slice of int to matrix and print values.
    lmath.ToMatrix([]int{1, 2, 3}).Print()
    // 2d slice of int to matrix and print values.
    lmath.ToMatrix([][]int{[]int{1, 2},[]int{3, 4}}).Print()
    // Slice of float64 to matrix and print values.
     lmath.ToMatrix([]float64{4, 5, 6}).Print()
    // 2d slice of float64 to matrix and print values.
    lmath.ToMatrix([][]float64{[]float64{7, 8},[]float64{9, 0}}).Print()
```
![image](https://raw.githubusercontent.com/lovesaroha/gimages/main/45.png)

### Matrix Element Wise Operations (Add, Subtract, Multiply, Divide) 

```Golang
  // Create a matrix (rows, cols, minimum , maximum).
  matrix := lmath.Matrix(3, 4, 10, 20)
  matrixB := lmath.Matrix(3, 4, 0, 10)

  // Add and print values.
  matrix.Add(matrixB).Print()
  // Subtract and print values.
  matrix.Sub(matrixB).Print()
  // Multiply and print values.
  matrix.Mul(matrixB).Print()
  // Divide and print values.
  matrix.Sub(matrixB).Print()
```
![image](https://raw.githubusercontent.com/lovesaroha/gimages/main/40.png)

### Matrix Element Wise Operations With Scalar Value (Add, Subtract, Multiply, Divide) 

```Golang
  // Create a matrix (rows, cols, minimum , maximum).
  matrix := lmath.Matrix(3, 4, 10, 20)

  // Add and print values.
  matrix.Add(2).Print()
  // Subtract and print values.
  matrix.Sub(2).Print()
  // Multiply and print values.
  matrix.Mul(2).Print()
  // Divide and print values.
  matrix.Sub(2).Print()
```
![image](https://raw.githubusercontent.com/lovesaroha/gimages/main/47.png)

### Matrix Dot Product 

```Golang
  // Create a matrix (rows, cols, minimum , maximum).
  matrix := lmath.Matrix(3, 4, 10, 20)
  matrixB := lmath.Matrix(4, 3, 0, 10)

  // Dot product and print values.
  matrix.Dot(matrixB).Print()
```
![image](https://raw.githubusercontent.com/lovesaroha/gimages/main/41.png)

### Matrix Transpose
```Golang
  // Create a matrix (rows, cols, minimum , maximum).
  matrix := lmath.Matrix(3, 4, 10, 20)

  // Print values.
  matrix.Print()
  // Transpose and print values.
  matrix.Transpose().Print()
```
![image](https://raw.githubusercontent.com/lovesaroha/gimages/main/42.png)

### Add All Column Values
```Golang
  // Create a matrix (rows, cols, minimum , maximum).
  matrix := lmath.Matrix(3, 4, 10, 20)

  // Print values.
  matrix.Print()
  // Add columns and print values.
  matrix.AddCols().Print()
```
![image](https://raw.githubusercontent.com/lovesaroha/gimages/main/46.png)

### Change Matrix Values (Map)
```Golang
  // Create a matrix (rows, cols, minimum , maximum).
  matrix := lmath.Matrix(3, 4, 10, 20)

  // Print values.
  matrix.Print()
  // Square and print values.
  matrix.Map(func (value float64) float64 {
    return value * value
  }).Print()
```
![image](https://raw.githubusercontent.com/lovesaroha/gimages/main/43.png)

### Apply Function In Matrix
```Golang
  // Create a matrix (rows, cols, minimum , maximum).
  matrix := lmath.Matrix(3, 4, -1, 1)

  // Print values.
  matrix.Print()
  // Apply sigmoid and print values.
  matrix.Map(lmath.Sigmoid).Print()
```
![image](https://raw.githubusercontent.com/lovesaroha/gimages/main/44.png)

## Examples

### Logistic Regression (OR Gate)
```Golang 
    // Learning rate.
    var learningRate = 0.2

    // Inputs and outputs.
    inputs := lmath.ToMatrix([][]float64{[]float64{1, 1, 0, 0},[]float64{0, 1, 0, 1}})
    outputs := lmath.ToMatrix([][]float64{[]float64{1, 1, 0, 1}})

    // Weights and bias.
    weights := lmath.Matrix(2, 1, -1, 1)
    bias := lmath.Random(-1, 1)

    // Train weights and bias (epochs 1000).
    for i := 0; i < 1000; i++ {
      // Sigmoid(wx + b).
      prediction := weights.Transpose().Dot(inputs).Add(bias).Map(lmath.Sigmoid)
      dZ := prediction.Sub(outputs)
      weights = weights.Sub(inputs.Dot(dZ.Transpose()).Divide(4).Mul(learningRate))
      bias -= dZ.Sum() / 4
    }

    // Show prediction.
    weights.Transpose().Dot(inputs).Add(bias).Map(lmath.Sigmoid).Print()

```
![image](https://raw.githubusercontent.com/lovesaroha/gimages/main/48.png)