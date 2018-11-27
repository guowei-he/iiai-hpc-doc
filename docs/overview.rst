Overview
####################

This page serves as the 'one-page' instructions for IIAI HPC Pilot System. Eligible users should be able to submit their first computational task with GPU by following this documentation.

Prerequisite
********************

The operating system is Linux. Make sure you know the basics. Useful links:

* http://linuxcommand.org/
* http://software-carpentry.org/lessons/
* https://www.edx.org/course/introduction-linux-linuxfoundationx-lfs101x-0


Account
********************

Refer to this page :doc:`/account` for getting an account.

Access
********************

With your account ready, you can access the system by ssh. With the VPN to data center turned on:

.. code-block:: bash

        ssh <your-account>@hpc.inceptioniai.org

For more information, check this page :doc:`access`.

Storage
********************

TODO


Data Transfer
********************
TODO

Hardware
********************
TODO

Software
********************
TODO

Running Jobs
********************
To run a job on the system:

#. Write a job script.
#. Submit the job.
#. Relax, have a coffee. If you wish, take a safari trip to Kenya.
#. Examine the result.

Let's say you have a python script called 'hello-tensorflow.py' to run. You need 1 V100 GPU, maximum 24 hours.

Job Script
====================

The job script defines your job. Most importantly:

#. What resources you need.
#. What you want to run.

For example::

  #!/bin/bash
  # Specify how many GPUs you need
  #SBATCH --gres=v100:1
  # Walltime format hh:mm:ss
  #SBATCH --time=24:00:00

  # All #SBATCH directive must be above the actual commands

  # Here I assume you already installed and set up your Tensorflow
  # If not, you might need to export PATH and/or PYTHONPATH to avail Tensorflow
  python hello-tensorflow.py

The directives are very intuitive. ``#SBATCH`` directives defines what resources you need. Then everything under is simply bash command.

If you need 2 V100 GPUs::

  #SBATCH --gres=v100:2


What happen if your job doesn't finish in 24 hours? The system will simply kill it. If you need maximum 48 hours::

  #SBATCH --time=48:00:00

You can save the job script in any name you want. For example, ``job.sh``.

Submit the Job
====================

Let say you go through the above example and saved the job script ``job.sh``. Now, you are ready to submit it to the system::

  sbatch job.sh

After the submission, it will return the corresponding ``${JOBID}``::

  [guowei@login]$ sbatch job.sh
  Submitted batch job 775602

Congratulation! You have successfully submitted your first job. You can relax and log off the system:)

Examine the Result
====================

Once started, the job will save its screen output, by default, to a file called ``slurm-${JOBID}.out``. In this example, it will be ``slurm-775602.out``
