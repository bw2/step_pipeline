# step-pipeline

Python library that makes it easier to define pipelines that 
1) run in container or VM execution environments like Batch, Terra, SGE, etc. 
2) are made up of "steps" that localize some input files, run some commands, and delocalize the output files. 

This library lets you define the steps, their input and output files, commands, etc. and then submits your pipeline to the execution environment. 

The main benefit is that it takes care of common pipeline aspects like: 
- before submitting the pipeline for execution, it skips steps whose outputs already exist and are newer than the inputs, and also checks initial input files so the pipeline doesn't immediately crash because an input file doesn't exist 
- localizes input files and delocalizes output files using different strategies (copy, gcfuse, etc.)
- defines command-line args for forcing re-execution of some steps
- optionally measures cpu and memory by starting a background process within a container to record cpu and memory at regular intervals while commands are running
- notifies you via slack or email when the pipeline completes

Downsides:
- some of these features only work if specific tools are installed inside the execution enviroment (container or VM). 
