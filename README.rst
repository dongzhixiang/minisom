MiniSom
=======

.. figure:: http://3.bp.blogspot.com/-TjLGnec3uko/Ud8LbHTpO1I/AAAAAAAAAqk/nfJneFOZrK8/s1600/logo.png
   :alt: MiniSom

   MiniSom

Self Organizing Maps
--------------------

MiniSom is a minimalistic and Numpy based implementation of the Self
Organizing Maps (SOM). SOM is a type of Artificial Neural Networks able
to convert complex, nonlinear statistical relationships between
high-dimensional data items into simple geometric relationships on a
low-dimensional display.

Installation
------------

Download MiniSom to the directory of your choice, enter it and run (may
require root privileges):

::

    python setup.py install

How to use it
-------------

In order to use MiniSom you need your data organized as a Numpy matrix
where each row corresponds to an observation or an as list of lists like
the following:

::

    data = [[ 5.1  3.5  1.4  0.2],
            [ 4.9  3.   1.4  0.2],
            [ 4.7  3.2  1.3  0.2], # <-- single observation
            [ 4.6  3.1  1.5  0.2],
            [ 5.   3.6  1.4  0.2],
            [ 4.1  3.3  1.4  0.2],
            [ 4.2  3.2  1.2  0.2]]         

Then you can run MiniSom just as follows:

::

    from minisom import MiniSom    
    som = MiniSom(6,6,4,sigma=0.3,learning_rate=0.5) # initialization of 6x6 SOM
    print "Training..."
    som.train_random(data,100) # trains the SOM with 100 iterations
    print "...ready!"

MiniSom implements two types of trainings. The random training
(implemented by the method ``train_random``), where the model is trained
picking random samples from your data, and the batch training
(implemented by the method ``train_batch``), where the samples are used
in the order they are stored.

A data driven initialization of the weights is also provided by the
method ``random_weights_init`` which initializes the weights picking
random samples from the data.

Using the trained SOM
~~~~~~~~~~~~~~~~~~~~~

After the training you will be able to

-  Compute the coordinate assigned to an observation ``x`` on the map
   with the method ``winner(x)``.
-  Compute the average distance map of the weights on the map with the
   method ``distance_map()``.
-  Compute the number of times that each neuron have been considered
   winner for the observations of a new data set with the method
   ``activation_response(data)``.
-  Compute the quantization error with the method
   ``quantization_error(data)``.

Vector quantization
^^^^^^^^^^^^^^^^^^^

The data can be quantized by assigning a code book (weights vector of
the winning neuron) to each sample in data. This kind of vector
quantization is implemented by the method ``quantization`` that can be
called as follows:

::

    qnt = som.quantization(data)

In this example we have that ``qnt[i]`` is the quantized version of
``data[i]``.

Examples
--------

In examples/example\_iris.py you can find an example that shows how to
train MiniSom and visualize the result using the Iris flower dataset.
Here is the result of the script:

For each observation we have a marker placed on the position of the
winning neuron on the map. Each type of marker represents a class of the
iris data. The average distance map of the weights is used as background
(see the color bar on the right to associate the value).

In examples/example\_digits.py there is an example of how to use MiniSom
for images clustering. The example uses the scitkits-learn wrapper to
the handwritten digits dataset. Here is one of the result that MiniSom
can achieve in digits recognition:

The graph above represent each image with the handwritten digit it
contains. The position corresponds to the position of the winning neuron
for the image. Here we also have a version of this graphs that shows the
original images:

In examples/example\_color.py you can find an example of how to use
MiniSom for color quantization. Here is one of the possible results:

(the examples require matplotlib for the visualization of the results).

Who uses Minisom?
-----------------

.. raw:: html

   <ul>

.. raw:: html

   <li>

Makiyama, Vitor Hirota, M. Jordan Raddick, and Rafael DC Santos. Text
Mining Applied to SQL Queries: A Case Study for the SDSS SkyServer. 2nd
Annual International Symposium on Information Management and Big Data.
2015.

.. raw:: html

   </li>

.. raw:: html

   <li>

Ivana Kajić, Guido Schillaci, Saša Bodiroža, Verena V. Hafner, Learning
hand-eye coordination for a humanoid robot using SOMs. Proceedings of
the 2014 ACM/IEEE international conference on Human-robot interaction
Pages 192-193.

.. raw:: html

   </li>

.. raw:: html

   </ul>

Compatibility notes
-------------------

Minisom has been tested under python 2.7.3 and 3.2.3.

License
-------

MiniSom by Giuseppe Vettigli is licensed under the Creative Commons
Attribution 3.0 Unported License. To view a copy of this license, visit
http://creativecommons.org/licenses/by/3.0/.

.. figure:: http://i.creativecommons.org/l/by/3.0/88x31.png
   :alt: Creative Commons Attribution 3.0 Unported License

   License
