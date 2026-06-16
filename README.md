# Gravitational_Waves_IDA

This is a description of how to run the gravitational wave 
scans and create the plots for the attached paper.

The scanning runs are now set up to use 16 CPUs.
The Python Pool method is used to parallelize the scanning process.
This assumes all the CPUs are in one machine.  
The number of CPUs used can be changed from 16 to 4 for all the scanning 
runs by executing './CPU_numbers_change_all.csh'.

To run the full process from scanning to the plotting, run 
'./AA-run-everything.csh'.  The processes in 'AA-run-everything.csh' are described 
below.  Running this will require about 2.4 TB of disk space.  

On a Mac Studio using 16 of 20 Apple M1 Ultra CPUs, the scanning jobs take about 7 days
to run.  The blocking and plotting runs will take about a day.
Changing the number of CPUs from 16 to 4 will increase the run 
time for the scanning from 7 days to 28 days.  The time will likely
increase even more if the CPUs are slower than the M1 processors on the 
Mac Studio.  You can use 'CPU_numbers_change_all.csh' to change the number
of CPUs from 16 to 4.


Care should be taken with the memory use.  The Mac Studio I am using has 
128 GB of memory. This is likely to be more than enough.  Some of the first
attempts on an old Mac used more memory than existed, causing memory to be
paged to disk.  The repeated disk access burnt up that Mac's disk.


The 'setup-data.csh' simply takes the input data in GW-DATA and copies
it to the various directories in preparation to scan.  There may be
better ways to do this, but this is a simple way to recreate the 
original runs. 

The 'all_scan_dirs.csh' is the main computational step.  In each of the 
directories, Framework-try0005, Framework00013, Framework00013pad, and GW9-4, the 
scanning process will examine the input data for consistent gravitational 
wave signals.  

After the scans are done, the 'all_blocking_dirs.csh'  will extract
a range of frequencies to output in frequency order.  The scanning step
outputs the data in a latitude and longitude order.  The blocking steps 
arranges a range of the data in frequency slices for the plotting jobs.

The 'all_plotting_dirs.csh' step will extract the disired blocked data
and plot it.  Each of the desired figures generated here will be copied to 
the Figures directory.

If your system has machines with only 4 CPUs, you can break up 'all_scan_dirs.csh' 
and run the scanning steps independently.  If you would like to use another number
of CPUs, change the 'change_ncpu_all.csh' in each of the Framework-try0005, Framework00013, 
Framework00013pad, and GW9-4 directories and then run each of the 'change_ncpu_all.csh' job.

The scanning runs assume that you are using Python 3.
There are a number of packages that need to be imported:
numpy
scipy
matplotlib 
math
sys
time 
os
pymeeus
multiprocessing
functools
datetime
mpl_toolkits





There are some obvious improvements in the processed used here.  Perhaps the most
important would be to change the fast Fourier transform in the scanning programs to 
a slow Fourier transforms.  This will not be as bad as it sounds since only a small range
of frequencies are needed. one of the problems with detecting these sources is that
the source frequency may be difficult to detect if that frequency overlaps adjacent
frequency samples. Making a finer frequency increment output may make the events 
easier to find.  In the scanning processes here, if the desired signal falls across more
than one frequency increment, the signal may be lost.  This is the reason that 
Framework00013 and Framework00013pad together can extract signals that are lost.  Simply padding
the the input as is done in Framework00013pad changes the frequency increment.
A slow Fourier transform with a frequency increment that is finer than that produced by a 
FFT would be slower, but may still be faster than producing all the frequencies with a
FFT.

Another obvious research direction would be to automate the denoising of the IDA and 
USGS array data.  The 1984 to 1987 data took four people 5 months to denoise.  
The data from 2017 was my only successful attempt with the newer data to clean these data.  
The 40 years of data we have of IDA and USGS data might be denoised more efficiently.
This may be a possible application of machine learning.
40 years of monitoring gravitational wave data from these binary systems might be 
interesting in that we could see the evolution of the binary system's orbital periods.  

Finally the signals from the binary systems seen here were previously discovered.
Even when the frequencies of the known sources are available, it is still difficult to
find the signal since the frequency increment is small and the number of frequencies 
to examine is large.  It would be interesting to attempt to find new sources,
and perhaps find signals from other types of sources.  Once again, this seems to be
another possible application of machine learning.

Correcting the signals to account for the frequency shifts caused by the velocity of the
Earth in its orbit would be useful in improving the detection of source near the ecliptic 
equator.  The present software ignores these shifts, creating a bias toward detecting signals
near the ecliptic poles.  One of the problems in making this correction is that the true 
direction of the source must be known, while the response of the Earth to these gravitational
waves is uncertain.  
