# Gravitational_Waves_IDA
This is an example of extracting gravitational wave signals using IDA and USGS seismic arrays.  
The gravitational waves of interest are semi-continuous signals, typically from white-dwarf stars in ultra-compact, very short orbital period,  binary systems.

**** Warning!  You might not want to do this at home. ****

or if you do, be careful.
I burnt up my old Mac when the memory demands exceeded the real memory and data was paged to disk.
My present Mac Studio has 128G of memory and 20 standard cpus. (Apple M1 Ultra).
Using 16 cpus running all the scanning jobs will take about a week.  
128G is likely to be an overestimate of the memory requirements.
The results occupy about 3 TB.

The scanning jobs, the most cpu intensive parts, use the python Pool method to parallelize the work.  This assumes that all the cpus are available on one machine.
