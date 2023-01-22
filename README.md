# Results of multiprocessing tutorial

Research is based on video [**Python Multiprocessing Tutorial: Run Code in Parallel Using the Multiprocessing Module**](https://www.youtube.com/watch?v=fKl2JW_qrso&ab_channel=CoreySchafer)

**To run these files and verify the correctness of the programs yourself, you will also need an image library**

to install it you need:

on **macOS**/**linux**:

```
python3 -m venv env

source env/bin/activate

pip3 install Pillow
```

on **windows**:

```
python -m venv env

env/Scripts/activate.bat //In CMD
env/Scripts/Activate.ps1 //In Powershel

pip install Pillow
```

**once installed you can use the following commands**:

on **macOS**/**linux**:

```
python3 <filename>
```

on **windows**:

```
python <filename>
```

<br />

## Test example

1. [Initial example](initial_example.py)

   First, consider a test case in which we call a function that sleeps for one second twice.

   The result of the program will be:

   ```
    Sleeping for 1 second...
    Done sleeping!
    Sleeping for 1 second...
    Done sleeping!
    Finished in 2.01 second(s)
   ```

   These functions are run one after the other, running for 1 second each, so the script takes 2 seconds to execute in this case.

2. [Initial example with process](initial_example_with_process.py)

   Let's add process to the previous program.

   The result of the program will be:

   ```
    Sleeping 5 second(s)...
    Sleeping 4 second(s)...
    Sleeping 3 second(s)...
    Sleeping 2 second(s)...
    Sleeping 1 second(s)...
    Done Sleeping...5
    Done Sleeping...4
    Done Sleeping...3
    Done Sleeping...2
    Done Sleeping...1
    Finished in 5.13 second(s)
   ```

   As we can see, the result of the execution of this program is slightly different from the version we got for the same [program using threads](https://github.com/ss-o-furda/multithreading-tutorial).

   It's not a big difference of 0.13 seconds, but it's there. This happens because Python needs to initialize a new process in the system, which takes extra time.

   That is why it is better to use threads than processes for such I/O programs.

## Real world example

In this case, we will consider a more real-world example of using multiprocessing.

Here we will look at a program that processes heavy images on disk and stores them in a different folder.

1. [Real world example](real_worlds_example.py)

   In this case, the processing is completely synchronous, that is, one image is processed first, after which the processing of the next one begins.

   The result of the program will be:

   ```
   photo-1516117172878-fd2c41f4a759.jpg was processed!
   photo-1532009324734-20a7a5813719.jpg was processed!
   photo-1524429656589-6633a470097c.jpg was processed!
   photo-1530224264768-7ff8c1789d79.jpg was processed!
   photo-1564135624576-c5c88640f235.jpg was processed!
   photo-1541698444083-023c97d3f4b6.jpg was processed!
   photo-1522364723953-452d3431c267.jpg was processed!
   photo-1493976040374-85c8e12f0c0e.jpg was processed!
   photo-1504198453319-5ce911bafcde.jpg was processed!
   photo-1530122037265-a5f1f91d3b99.jpg was processed!
   photo-1516972810927-80185027ca84.jpg was processed!
   photo-1550439062-609e1531270e.jpg was processed!
   photo-1549692520-acc6669e2f0c.jpg was processed!
   Finished in 13.44 second(s)
   ```

2. [Real world example with process](initial_example_with_process.py)

   However, if we rewrite the program above to use processes , we will get a significant speedup, since image processing operations use the CPU as much as possible in this case.

   In case of process the result of the program will be:

   ```
   photo-1516117172878-fd2c41f4a759.jpg was processed!
   photo-1524429656589-6633a470097c.jpg was processed!
   photo-1522364723953-452d3431c267.jpg was processed!
   photo-1530224264768-7ff8c1789d79.jpg was processed!
   photo-1532009324734-20a7a5813719.jpg was processed!
   photo-1564135624576-c5c88640f235.jpg was processed!
   photo-1541698444083-023c97d3f4b6.jpg was processed!
   photo-1516972810927-80185027ca84.jpg was processed!
   photo-1504198453319-5ce911bafcde.jpg was processed!
   photo-1530122037265-a5f1f91d3b99.jpg was processed!
   photo-1493976040374-85c8e12f0c0e.jpg was processed!
   photo-1550439062-609e1531270e.jpg was processed!
   photo-1549692520-acc6669e2f0c.jpg was processed!
   Finished in 5.75 second(s)
   ```

## Conclusions

As we can see on a real example, using process for operations that require image processing, code compilation, etc., gives an increase in speed of about two-three times.
