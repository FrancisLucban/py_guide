# 📈 Matplotlib – More Comprehensive Reference

```py
import matplotlib.pyplot as plt
import numpy as np

# Sample data
x = np.linspace(0, 10, 100)
y = np.sin(x)
z = np.cos(x)
```

## 🔹 Line Plot

```py
plt.plot(x, y, label="sin(x)")
plt.plot(x, z, label="cos(x)", linestyle="--")
plt.title("Line Plot")
plt.xlabel("X-axis")
plt.ylabel("Y-axis")
plt.legend()
plt.show()
```

## 🔹 Scatter Plot

```py
plt.scatter(x, y, c='red', marker='o')
plt.title("Scatter Plot")
plt.show()
```

## 🔹 Bar Chart

```py
categories = ["A","B","C","D"]
values = [3,7,5,2]

plt.bar(categories, values, color="skyblue")
plt.title("Bar Chart")
plt.show()
```

## 🔹 Horizontal Bar Chart

```py
plt.barh(categories, values, color="orange")
plt.title("Horizontal Bar Chart")
plt.show()
```

## 🔹 Histogram
data = np.random.randn(1000)

```py
plt.hist(data, bins=30, color="purple", alpha=0.7)
plt.title("Histogram")
plt.show()
```

## 🔹 Boxplot

```py
data = [np.random.normal(0, std, 100) for std in range(1, 4)]

plt.boxplot(data, vert=True, patch_artist=True)
plt.title("Boxplot")
plt.show()
```

## 🔹 Violin Plot

```py
plt.violinplot(data, showmeans=True)
plt.title("Violin Plot")
plt.show()
```
## 🔹 Pie Chart

```py
sizes = [30, 20, 25, 25]
labels = ["A","B","C","D"]

plt.pie(sizes, labels=labels, autopct="%1.1f%%", startangle=90)
plt.title("Pie Chart")
plt.show()
```

## 🔹 Area Plot (Filled Line Plot)

```py
plt.fill_between(x, y, color="skyblue", alpha=0.4)
plt.title("Area Plot")
plt.show()
```

## 🔹 Step Plot

```py
plt.step(x, y, where="mid")
plt.title("Step Plot")
plt.show()
```

## 🔹 Stack Plot

```py
y1 = np.sin(x)
y2 = np.cos(x)
y3 = np.sin(x/2)

plt.stackplot(x, y1, y2, y3, labels=["sin","cos","sin/2"], alpha=0.6)
plt.legend()
plt.title("Stack Plot")
plt.show()
```

## 🔹 Heatmap (using imshow)

```py
matrix = np.random.rand(5,5)

plt.imshow(matrix, cmap="viridis", interpolation="nearest")
plt.colorbar()
plt.title("Heatmap")
plt.show()
```

## 🔹 Contour Plot

```py
X, Y = np.meshgrid(np.linspace(-3,3,100), np.linspace(-3,3,100))
Z = np.sin(np.sqrt(X**2 + Y**2))

plt.contour(X, Y, Z, cmap="plasma")
plt.title("Contour Plot")
plt.show()
```

## 🔹 Filled Contour Plot

```py
plt.contourf(X, Y, Z, cmap="plasma")
plt.colorbar()
plt.title("Filled Contour Plot")
plt.show()
```

## 🔹 Quiver Plot (vector fields)

```py
X, Y = np.meshgrid(np.arange(-2, 2, 0.2), np.arange(-2, 2, 0.2))
U = -X
V = Y

plt.quiver(X, Y, U, V)
plt.title("Quiver Plot")
plt.show()
```

## 🔹 Streamplot

```py
plt.streamplot(X, Y, U, V, color=np.sqrt(U**2 + V**2), cmap="cool")
plt.title("Stream Plot")
plt.show()
```

## 🔹 Polar Plot

```py
theta = np.linspace(0, 2*np.pi, 100)
r = 1 + np.sin(6*theta)

plt.polar(theta, r)
plt.title("Polar Plot")
plt.show()
```

## 🔹 Error Bar Plot

```py
y = np.sin(x)
error = 0.1 + 0.1 * np.sqrt(x)

plt.errorbar(x, y, yerr=error, fmt="o", ecolor="red", capsize=3)
plt.title("Error Bar Plot")
plt.show()
```

## 🔹 Multiple Subplots

```py
fig, axs = plt.subplots(2,2, figsize=(8,6))

axs[0,0].plot(x,y)
axs[0,0].set_title("Line")

axs[0,1].bar(categories, values)
axs[0,1].set_title("Bar")

axs[1,0].scatter(x,y)
axs[1,0].set_title("Scatter")

axs[1,1].hist(data, bins=20)
axs[1,1].set_title("Histogram")

plt.tight_layout()
plt.show()
```

---

## 📌 Summary of Figure Types

- **Line & Area** → plot(), fill_between(), step(), stackplot().
- **Scatter** → scatter().
- **Categorical** → bar(), barh(), boxplot(), violinplot(), pie().
- **Distribution** → hist().
- **Matrix/Fields** → imshow(), contour(), contourf(), quiver(), streamplot().
- **Special** → polar(), errorbar().
- **Layout** → subplots() for grids of plots.