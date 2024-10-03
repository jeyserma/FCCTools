# Particle gun
Generator of particle gun in the ```hepmc3``` format. Uniform in polar angle and exponential in momentum range.

## Compile
The gun needs to compile on a ```cc7``` machine. On ```el9```, do:

```
cmssw-cc7
source /cvmfs/sw.hsf.org/spackages6/key4hep-stack/2022-12-23/x86_64-centos7-gcc11.2.0-opt/ll3gi/setup.sh
HEPMC3_PATH="/cvmfs/sw.hsf.org/spackages7/hepmc3/3.2.5/x86_64-centos7-gcc11.2.0-opt/rysg6"
export LD_LIBRARY_PATH=$HEPMC3_PATH/lib64:$LD_LIBRARY_PATH
g++ --std=c++11 -I${HEPMC3_PATH}/include -L${HEPMC3_PATH}/lib64 -lHepMC3 -o gun gun.cpp
```

## Generate events

Create an input file (```gun.input```):
```
npart_range 1,1
theta_range 90.0,90.0
mom_range 20.0,80.0
drmax 0.001
pid_list 13,-13
nevents 100000
```
This generates 100000 events (```nevents```), each event containing 1 muon (```pid_list ``` and ```npart_range```) at 90 degrees and within a momentum range of 20 to 80 GeV. The ```drmax``` can be used to generate the events within a certain cone around the random direction. To run (in the same environment as it was compiled in):

```
./gun gun.input  # on a cc7 machine
``` 

To run directly on an ```el9``` machine, one can use the gun directly in a ```cc7``` singularity:

```
chmod 755 run_singularity.sh
./run_singularity.sh gun.input # on a el9 machine
```
The output is stored in the ```events.hepmc``` file.
