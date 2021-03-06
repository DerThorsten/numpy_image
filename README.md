# numpy_image

This is a module for displaying numpy matrices as widgets on a kivy canvas. 

Cython code is used for essential speedup. Run 

  > python setup.py build_ext --inplace

or
   > python3 setup.py build_ext --inplace
   
in the src directory to build c library

The module contains two classes. Additionally two colormaps are included 'PastelHeat' and 'Random'

1. ImDisplay:

   > ImDisplay.create_im(image, 'color_map',  scale=True)

  This takes a numpy 2D array scales it to the number of colors in an RGB colormap (len(cmap) divided by 3). After scaling the matrix is mapped to an RGB format and then displayed as the texture of a kivy rectangle. The option of not scaling the image is available though values in the image must not exceed the number of colours available. An example of this function and test image are provided.
  
     > ImDisplay.update_im(image)
     
  Updates the image on the canvas, much faster execution time than reloading.
  
  
2. IndexedDisplay

   > IndexedDisplay.create_im(image, 'color_map', mapping)

  This class requires an additional input that displays images where many values in the numpy matrix need to point to the same color
  
  The mapping numpy array must be the length of the greatest value in the image that requires indexing, each value must correspond to a color e.g. in the following example with a three color RGB colormap.
   
```python
  color_map = [[.1 .1 .9]
               [.1 .9 .1]
               [.9 .1 .1]]
  
  image = [ 1 2 3
            4 5 6
            7 8 9]
 
  mapping = [1 2 3 1 2 3 1 2 3]
  
  mapped_image = [ 1 2 3
                   1 2 3
                   1 2 3]

  displayed_image = [[.1 .1 .9] [.1 .9 .1] [.9 .1 .1]
                    [.1 .1 .9] [.1 .9 .1] [.9 .1 .1]
                    [.1 .1 .9] [.1 .9 .1] [.9 .1 .1]]

```

  > IndexedDisplay.update_im(image, mapping)
  
  Updates image on canvas either with new image or mapping.


