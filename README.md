Addtional notes about the codes on electron ptychography
2020/02/22 Dr. Zhen Chen, Prof. David A. Muller Group, Cornell University
	 
----------------------
----------------------
To run reconstruction, run the main drive script: ptychography_clean_drive.m. Before doing this, please refer to the notes below:
 
1. Download the ptychography package from PSI (http://www.psi.ch/sls/csaxs/software).

2. Replace the Data.m script by the new one from this deposit. Also put all the scripts given here to the same folder as the ptychogrpahy package.

3. Read README.md for details about the algorithms and settings from PSI's package. 

4. Experimental data (supple. Fig. 4 in the manuscript) is assumed to be put in the same folder as the main folder of the codes with the path: 
    .\rawdata_21\rawdata_1x_crop.mat
	You need to change the drive script accordingly if you put the data somewhere else.
		
5. Look into the script ptychography_clean_drive.m and check / modify parameters.

6. Important parameters are parameters for data related and some of the reconstruction ones.

7. For the example dataset and using the default parameters (300 iterations with 128 x 128 pixels for each diffraction), 
   it will take less than 10 minutes on a decent GPU card (memory > 1 GB) and about two hours on CPU.
   It is the top-left corner and only about contains 1/4 diffractoins. 
   
   if no computational GPU card is available, please changes to use CPU:
   param.use_gpu = false; % use GPU
   
8. The outputs are in a folder defined by variable 'dir_base' within data folder and the phase image is under name:
     MLs_backgroundremove_final_crop_phase.png
	 All input parameters are stored in sample_pty_inputs.mat 
	 Clean reconstructions are in MLs_backgroundremove_final_crop_data.mat
	 raw reconstructions are in sample_pty_refine_outputs.mat

9. There is an error when using multiple probe modes (param.Nprobes>1). 
For a quick fix, replace line 306 with "self.probe{ll} = apply_probe_contraints(self.probe{ll}, self.modes{min(ll,end)});" in LSQML-code/+engines/LSQML.m
----------------------
----------------------

License agreements
----------------------

The main ptychography toolkit developed at Paul Scherrer Institut, Switzerland is available at
 [www.psi.ch/sls/csaxs/software](http://www.psi.ch/sls/csaxs/software)
Copyright and license issues should follow the agreements in their codes and/or refer to their website. 

-----------------------
The interface and data handling parts of the codes were writen by Zhen Chen. 
Details on the data set and collection conditions can be found in
"Mixed-state electron ptychography enables sub-angstrom resolution imaging with picometer precision at low dose",
Zhen Chen, Michal Odstrcil, Yi Jiang, Yimo Han, Ming-Hui Chiu, Lain-Jong Li, David A. Muller, Nature Communications, 11, 2994 (2020).
https://doi.org/10.1038/s41467-020-16688-6

This paper should be cited whenever this code, dataset or their derivatives are used.
 
----------------------
----------------------

Contact information
----------------------
Zhen Chen (zhen.chen@conell.edu) or David A. Muller (david.a.muller@cornell.edu)
