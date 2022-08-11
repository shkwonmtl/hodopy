# hodopy
Python package for Hodograph Control Curve

<a href="https://shkwonmtl.github.io/hello-world/hodopoly/hodopoly.html"> Demo </a>

### Basic usage

Install hodopy from [PyPi](https://pypi.org/project/hodopy) via

```
pip install hodopy
```



```python
import hodopy as hp
import numpy as np
import matplotlib.pyplot as plt

xylist = np.array([68,343,96,100,214,317,334,200,365,333])
ctlptlist = np.reshape(xylist, (-1,2))

ndiv = 200
t = np.linspace(-1,1,ndiv+1)

ptlist = hp.getHCCPt(ctlptlist, t, 'all')    

print(ptlist.shape)
```

```python
(201, 3, 2)
```

```python
polygonlen = hp.computePolygonLength(ctlptlist)
curvelen = hp.getHCCLength(ctlptlist, ndiv=200, curve="all")
labs = ['Gauss-Legendre','Gauss-Lobatto', 'Bézier', 'Control Polygon']
lengths = np.hstack((curvelen, [polygonlen]) )
lab2 = [labs[i] + f"({lengths[i]:0.3f})" for i in range(4)]
print(lab2)
```

```python
['Gauss-Legendre(697.953)', 'Gauss-Lobatto(651.357)', 'Bézier(418.043)', 'Control Polygon(795.779)']
```

```python
px, py = ptlist[:,:,0], ptlist[:,:,1]
res = plt.plot(px, py)
[res[i].set_color(c) for i, c in enumerate(['b','r','k'])]

cx, cy = ctlptlist[:,0], ctlptlist[:,1]
plt.plot(cx, cy, '--k')
plt.plot(cx, cy, 'ro', markersize=10)
plt.gca().invert_yaxis()

plt.legend(lab2)
plt.show()
```
.. image:: https://github.com/shkwonmtl/hodopy/blob/main/docs/images/example01.png
   :align: center
   
   https://github.com/shkwonmtl/hodopy/blob/main/docs/images/example01.png?raw=true
