Compile ADM1F
=====================================

1.  ADM1F uses external numerical library package PETSc. First download PETSc::

    $ cd build; git clone -b release https://gitlab.com/petsc/petsc.git petsc
    
    ::
    
    $ cd petsc; git checkout v3.14

2.  Set **PETSC_DIR** and **PETSC_ARCH** in your environmental variables. We suggest to put these lines in your `~/.bashrc` or similar files (`~/.bash_profile` on Mac OS X). Once you add it into the bash file, run `source  ~/.bash_profile`::

    $ export PETSC_DIR=/path-to-my-ADM1F-folder/build/petsc

    and::

    $ export PETSC_ARCH=macx-debug
    
    **Make sure** that ‘adolc-utils’ folder is in the ‘build' folder. 

3.  Configure PETSC::

    $ ./configure --download-mpich --with-cc=clang --with-fc=gfortran --with-debugging=0 --download-adolc PETSC_ARCH=macx-debug --with-cxx-dialect=C++11 --download-colpack

**NOTE**: that these are for Mac OSX. If you are installing on a linux machine, then replace **clang** with **gcc**. Also, sometimes turning off `--with-fc=0` could help with compilation. This step will take awhile.

4.  If configuration goes well, you can then compile. This step will take awhile too.::

    $ make PETSC_DIR=/path-to-my-ADM1F-folder/build/petsc PETSC_ARCH=macx-debug all

5.  After compilation, PETSc will show you how to test your installation (testing is optional).

6.  Navigate back to the `build` folder (`cd ../`) and compile adm1f::

    $ make adm1f
    
    or::
    
    $ make

7.  Set **ADM1F_EXE** in your environmental variable. Add this line in your `~/.bashrc` or similar files (`~/.bash_profile` on Mac OS X).  Once you add it into the bash file, do not forget to `source  ~/.bash_profile`:: 
     
    $ export ADM1F_EXE=path-to-my-ADM1F-folder/build/adm1f

8.  **NOTE**: There are two versions of the ADMF1: the original version  (adm1f.cxx), and the modified version of the model (adm1f_srt.cxx, see :ref:`ADM1F_SRT`). 
    

Running ADM1F
=====================================

1. Make sure that **ADM1F_EXE:** is not empty (see step 7 from the previous section).::

    $ echo $ADM1F_EXE

2. Navigate to the `simulations` folder and run the model::

    $ $ADM1F_EXE
    
    or using command-line options (see 4 and 5):
    
    $ $ADM1F_EXE -ts_monitor -steady

3. Note that adm1f will look for three files `ic.dat`, `params.dat`, and `influent.dat`, which contain the initial conditions (45 values), parameters (100 values), and influent values (28 values), see :ref:`inouts-label`.

4. The command-line options are:

    *  -Cat [val] - mass of Cat+ added [kmol/m3]
    *  -Vliq [val] - volume of liquid [m3]
    *  -Vgas [val] - volume of liquid [m3]
    *  -t_resx [val] -SRT adjustment: t_resx = SRT-HRT, [d] (works only for adm1f_srt.cxx)
    *  -params_file [filename] - specify params filename (default is params.dat)
    *  -ic_file [filename] - specify initial conditions filename (default is ic.dat)
    *  -influent_file [filename] - specify influent filename (default is influent.dat)
    *  -ts_monitor - shows the timestep and time information on screen
    *  -steady - run as steady state else runs as transient
    *  -debug - gives out more details on the screen

5. More command-line options can be found `here <https://www.mcs.anl.gov/petsc/petsc-current/docs/manualpages/TS/TSSetFromOptions.html>`_.


.. _ADM1F_SRT:

ADM1F SRT
=====================================

The adm1f_srt.cxx version includes solid retention time (SRT) and other modifications described below. To switch to the SRT version of the model change 'EXAMPLESC  = adm1f_srt.cxx' , 'OBJECTS_PF = adm1f_srt.o', and 'adm1f: adm1f_srt.o' in the `build/makefile`. Then recompile the model (Compile ADM1F, step 6).  

	* Includes a term (T_resx) in the mass balance to separate the solids retention time from hydraulic retention time.
	* Uses the empirical Hill function that describes the inhibition of acetogenesis and hydrogenotrophic methanogenesis by acetic acid with the noncompetitive inhibition model [#love99]_ [#osli85]_.
	* Describes the inhibition of acetic acid on acetoclastic methanogenesis with the Haldane equation [#hald30]_ [#andr68]_.
	* Includes a adsorption-inhibition term describing the long-chain fatty acid [#pala10]_ (LCFA) inhibition of LCFA degradation and methanogenesis.
	* Includes Arrhenius equations describing the effect of temperature on bioreaction kinetics [#nova74]_.
	* Includes a cation term to simulate the addition of NaOH for pH adjustment.
	
.. rubric:: References

.. [#love99] Love, N. G., R. J. Smith, K. R. Gilmore, and C. W. Randall. 1999. Oxime inhibition of nitrification during treatment of an ammonia-containing industrial waste. Water Environment Research 71:418–26.
.. [#osli85] Oslislo, A., and Z. Lewandowski. 1985. Inhibition of nitrification in the packed bed reactors by selected organic compounds. Water Research 19:423–26. 
.. [#hald30] Haldane, J. B. S. 1930. Enzymes. London: Longmans.
.. [#andr68] Andrews, J. F. 1968. A mathematical model for the continuous culture of microorganisms utilizing inhibitory substrates. Biotechnology and Bioengineering 10:707–23. 
.. [#nova74] Novak, J. T. 1974. Temperature-substrate interactions in biological treatment. Journal, Water Pollution Control Federation 46:1984–94.
.. [#pala10] Palatsi, J., Illa, J., Prenafeta-Boldú, F.X., Laureni, M., Fernandez, B., Angelidaki, I., Flotats. X. 2010. Long-chain fatty acids inhibition and adaptation process in anaerobic thermophilic digestion: Batch tests, microbial community structure and mathematical modelling. Bioresource Technology. 101, 7, 2243-2251.