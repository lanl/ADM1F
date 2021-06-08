.. ADM1F documentation master file, created by
   sphinx-quickstart on Sat Aug 15 22:50:15 2020.
   https://user-zwj.github.io/pagetest2/instruction.html
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

****************************************
Anaerobic Digester Model #1 Fast (ADM1F)
****************************************

Anaerobic digestion (AD) process converts organic wastes into biogas. Biogas can generate heat and electricity through a cascade of biochemical reactions and has been adapted by various facilities and industries to treat and recover energy from high-strength liquid or solid waste streams. Anaerobic Digestion Model 1 (ADM1) is a mathematical model that describes the stoichiometry and kinetics of the essential biochemical reactions in AD. This repository includes C++ version of the Matlab/Simulink [#rosen06]_ version of the ADM1 model and the solid retention time (SRT) version [#zhu]_. The C++ version of the model is computationally more efficient than its Matlab/Simulink predecessor. We called this version of the model Anaerobic Digestion Model 1 Fast (ADM1F). 

.. image:: _static/images/digester_m.png

.. toctree::
   :maxdepth: 2
   :caption: User Guide:

   compile
   inouts
#   examples
#   join

.. rubric:: References

.. [#rosen06] `Rosen C., Vrecko D., Gernaey K.V., Pons M.-N. and Jeppsson U. (2006). Implementing ADM1 for plant-wide benchmark simulations in Matlab/Simulink. Water Sci. Technol., 54(4), 11-19. <https://pdfs.semanticscholar.org/9f84/13e7bb8ec49b3d0eb321e9d54720f117a527.pdf>`_
.. [#zhu] `Zhu et al, in prep. A Novel Core-shell ADM1 model allows rapid optimization of membrane anaerobic digestion processes`

.. rubric:: Acknowledgements

The research was supported by the U.S. Department of Energy, Office of Energy Efficiency and Renewable Energy, Bioenergy Technologies Office, under contract DE-AC02-06CH11357.
