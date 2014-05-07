queue
=====

Qsub array submit tool for large arrays. It processes your jobs in small definable segments and keeps running available segments until your user job limit (definable) is reached. This procedes asynchronously so you can keep using the queue.py tool to submit new jobs to the managed queue. The benefit of this tool is a managed queue of any number of jobs, of which they have variable run time. If a small batch of 10 jobs finishes quickly, then the next available batch of 10 jobs will begin.

#### Configuration
Step one, configure the first few lines of the submit tool, queue.py

    #!pathToPythonHere
    # path to python, if you want to run this without explicitly calling python (./queue.py myscript.sh)
    
    # where is your writable directory? Jobs will be managed in a .queue directory here.
    SCRATCH="pathToNetworkWritableFolder" #for me this is /mnt/scratch/jory
    
    # username
    USER="yourUserNameHere"
    
    # how big is one batch of jobs? ex 10 means there must be 10 free slots to run another batch.
    JOB_ARRAY_MAX=10
    
    # max total jobs to run in parallel with this tool (ideally multiple of JOB_ARRAY_MAX)
    QUEUE_MAX=200

Usage:
    python queue.py myarrayjob.sh
or if you've set up the path to python and set the executable flag on queue.py
    ./queue.py myarrayjob.sh

This assumes your qsub array job is formatted using the PBS -t #-# syntax as below. All qsub valid spacing is valid here.

    #PBS -t 1 - 1024

#### Roadmap
In no particular order.
* Move config options to an external config file that is generated with sane values if it doesn't exist already.
* Support qsub array shorthand description such as #PBS -t 5
* Add ability to query status of all jobs / projects. Such as ./queue.py status

#### Licensing
Copyright (c) 2014, Jory Schossau
All rights reserved.

Redistribution and use in source and binary forms, with or without
modification, are permitted provided that the following conditions are met:

1. Redistributions of source code must retain the above copyright notice, this list of conditions and the following disclaimer. 
2. Redistributions in binary form must reproduce the above copyright notice, this list of conditions and the following disclaimer in the documentation and/or other materials provided with the distribution.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS" AND
ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED
WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE
DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT OWNER OR CONTRIBUTORS BE LIABLE FOR
ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES
(INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES;
LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND
ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT
(INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS
SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.

The views and conclusions contained in the software and documentation are those
of the authors and should not be interpreted as representing official policies, 
either expressed or implied, of the FreeBSD Project.
