Recipes for Initial Conditions
==============================

General use of initial conditions
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Initial conditions can be included in the model by passing it directly
to the Model object.  For example, for a uniform distribution centered
at 0, do::

  from ddm import Model
  from ddm.models import ICRange
  model = Model(IC=ICRange(sz=.2))

.. _ic-biased:

Biased Initial Conditions
~~~~~~~~~~~~~~~~~~~~~~~~~

When rewards or stimulus probabilities are asymmetric, a common
paradigm is to start the trial with a bias towards one side.  Suppose
we have a sample which has the ``highreward`` condition set to either
0 or 1, describing whether the correct answer is the high or low
reward side.  We must define the :meth:`~.InitialCondition.get_IC`
method in an :class:`.InitialCondition` object which generates a
discredited probability distribution on the model's position grid
domain.  We can model this with:

.. literalinclude:: ../downloads/cookbook.py
   :language: python
   :start-after: # Start ICPointRew
   :end-before: # End ICPointRew

Then we can compare the high reward distribution to the low reward
distribution::

  from ddm import Model
  from ddm.plot import plot_compare_solutions
  import matplotlib.pyplot as plt
  model = Model(IC=ICPoint(x0=.3))
  s1 = model.solve(conditions={"highreward": 1})
  s2 = model.solve(conditions={"highreward": 0})
  plot_compare_solutions(s1, s2)
  plt.show()

To more accurately represent the initial condition, we can 
linearly approximate the probability density function at the two 
neighboring grids of the initial position:

.. literalinclude:: ../downloads/cookbook.py
   :language: python
   :start-after: # Start ICPointRewInterp
   :end-before: # End ICPointRewInterp


.. _ic-biased-range:

Biased Initial Condition Range
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. literalinclude:: ../downloads/cookbook.py
   :language: python
   :start-after: # Start ICPointRange
   :end-before: # End ICPointRange


.. _ic-cauchy:

Cauchy-distributed Initial Conditions
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. literalinclude:: ../downloads/cookbook.py
   :language: python
   :start-after: # Start ICCauchy
   :end-before: # End ICCauchy
