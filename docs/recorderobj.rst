.. include:: sub.txt

Recorder Object
================

.. class:: recorder()

   The :class:`recorder` object is to monitor what is happening during the
   analysis and generate output for the user.
   Use :ref:`recorder-class-methods` below to create recorderes.

Object methods
---------------------

#. :attr:`recorder.automatic`

   An object attribute (get) |int|.
   If it's ``1``, the recorder will be called in each time step to
   record outputs. Otherwise, the user should invoke the call.

   ::
   
      if re.automatic == 0:
          re.record()

	   
     
Object methods
---------------------

#. :meth:`recorder.__str__`
#. :meth:`recorder.record`

.. method:: recorder.__str__()

   The string reprsentation of the :class:`recorder`. Usually
   used in the |print| function.

   ::

      print(m)

.. method:: recorder.record()

   Record the outputs. This method will be called automatically
   after the analysis if :attr:`recorder.automatric` is ``1``.

   ::

      re.record()

.. _recorder-class-methods:


Class methods
---------------

#. :meth:`recorder.pvd`
#. :meth:`recorder.Node`


.. classmethod:: recorder.pvd(filename,automatic=1,dT=0.0,disp=0,vel=0,accel=0,incrDisp=0,reaction=0,pressure=0,unbalancedLoad=0,mass=0,eigen=0,precision=10,indent=2)

   Create a pvd recorder object, which can loaded in `ParaView`_.

   ========================   ======================================================================
   ``filename`` |str|         A string for the name of pvd files. A directory with the
		              name ``filename`` should be created by the user
                              and ``filename.pvd`` will be created by OpenSees.
   ``automatic`` |int|        Set the value of :attr:`recorder.automatic`. (optional)
   ``dT`` |float|             Time interval for recording. will record when next step
		              is ``dT`` greater than last recorder step.
                              (optional, ``dT=0`` means to record at every time step)
   ``disp`` |int|             Include nodal displacement in the outputs or not. (optional)
   ``vel`` |int|              Include nodal velocity in the outputs or not. (optional)
   ``accel`` |int|            Include nodal acceleration in the outputs or not. (optional)
   ``incrDisp`` |int|         Include nodal incremental displacement in the
                              outputs or not. (optional)
   ``reaction`` |int|         Include nodal reaction in the outputs or not. (optional)
   ``pressure`` |int|         Include nodal fluid pressure in the outputs or not. (optional)
   ``unbalancedLoad`` |int|   Include nodal unbalanced load in the outputs or not. (optional)
   ``mass`` |int|             Include nodal mass in the outputs or not. (optional)
   ``eigen`` |int|            The number of eigen values to be includeded
		              in the outputs. (optional)
   ``precision`` |int|        Output data precision. (optional)
   ``indent`` |int|           Indentation of output files. (optional)
   ========================   ======================================================================


   ::

      pvd = recorder.pvd('test',automatic = 0)
      pvd.record()


.. classmethod:: recorder.Node(nds,dofs,automatic=1,file='',xml='',binary='',csv='',inetAddr='',port=0,precision=6,scientific=0,timeSeries=[],time=0,dT=0.0,closeOnWrite=0,disp=0,vel=0,accel=0,incrDisp=0,reaction=0,reactionIncInertia=0,pressure=0,unbalancedLoad=0,rayleighForces=0)

   Create a Node recorder object.

   ========================   ======================================================================
   ``nds`` |list|             A list of :class:`node` objects, whose response is
		              being recorded.
   ``dofs`` |listi|           The specified dof at the :class:`node` objects
		              whose response is requested.
   ``automatic`` |int|        Set the value of :attr:`recorder.automatic`. (optional)
   ``file`` |str|             Name of file to which output is sent in textual format.
		              including file extension. (optional)
   ``xml`` |str|              Name of file to which output is sent in xml format.
		              including file extension. (optional)
   ``binary`` |str|           Name of file to which output is sent in binary format.
		              including file extension. (optional)
   ``csv`` |str|              Name of file to which output is sent in csv format.
		              including file extension. (optional)
   ``inetAddr`` |str|         ip address, ``'xx.xx.xx.xx'``, of
		              remote machine to which data is sent. (optional)
   ``port`` |int|             port on remote machine awaiting tcp. (optional)
   ``precision`` |int|        Output data precision. (optional)
   ``scientific`` |int|       Use scientific notation for output data. (optional)
   ``timeSeries`` |list|      A list of :class:`timeSeries` objects.
		              Results from node at each time step are added to
                              load factor from series. (optional)
   ``time`` |float|           Set this option to ``1`` to place domain time in first
		              entry of each data line. (optional)
   ``dT`` |float|             Time interval for recording. will record when next step
		              is ``dT`` greater than last recorder step.
                              (optional, ``dT=0`` means to record at every time step)
   ``closeOnWrite`` |int|     Set this option to ``1`` to instruct the recorder to
		              invoke a close on the data handler after every timestep.
                              If this is a file it will close the file on every step
                              and then re-open it for the next step. Note,
                              this greatly slows the execution time, but is
                              useful if you need to monitor the data during
                              the analysis. (optional)
   ``disp`` |int|             Include nodal displacement in the outputs or not. (optional)
   ``vel`` |int|              Include nodal velocity in the outputs or not. (optional)
   ``accel`` |int|            Include nodal acceleration in the outputs or not. (optional)
   ``incrDisp`` |int|         Include nodal incremental displacement in the
                              outputs or not. (optional)
   ``reaction`` |int|         Include nodal reaction in the outputs or not. (optional)
   ``reactionIncInertia``     Include nodal reaction with inertia forces
		              in the outputs or not. (optional)
   ``pressure`` |int|         Include nodal fluid pressure in the outputs or not. (optional)
   ``unbalancedLoad`` |int|   Include nodal unbalanced load in the outputs or not. (optional)
   ``rayleighFoces`` |int|    Include damping forces in the outputs or not. (optional)
   ========================   ======================================================================


   ::

      ndrecorder = recorder.Node(nds=[nd1,nd2,nd3],dofs=[1,2],
                                 file='nodesD.out',disp=1)
      ndrecorder = recorder.Node(nds=[nd1,nd2],dofs=[1],timeSeries=[ts1],
                                 file='nodesA.out',accel=1)

   .. note::

      #. One must set one of ``file``, ``xml``, ``binary``, ``csv``, or ``inetAddr`` and ``port``.
      #. One must set one of the response types.
      #. In the last example, for a :meth:`pattern.UniformExcitation` analysis, this method generates output file ``nodesA.out`` that contains absolute accelerations (ground motion acceleration + relative acceleration) in x direction for ``nd1`` and ``nd2``. NOTE that if no :class:`timeSeries` is provided and a :meth:`pattern.UniformExcitation` analysis is performed, the relative accelerations are recorded.




