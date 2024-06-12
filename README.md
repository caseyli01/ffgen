# ffgen_RESP_mae
combine forcefield generator (GAFF) in veloxchem and esp charge with jaguar output to generate *xyz and *itp for molecular dynamics running 
# How to use 
mae = 'er_M1_Co2TCPP_opt_B3LYP-D3_LACVPss.01.mae'  # "*01.mae"\
charge_column = 7 #default esp output column in *01.mae, *count the first column as 1* \
charge_column = 7 #please check your *01.mae to find which column is atom_label like(C1,N2...) *count the first column as 1*\
grofile_name = 'TCPP_lacvpss' \
residue_name = 'TCP' # 3letters\
std_thresh = 0.12 #standard deviation threshold which should a reasonable value\
# Strategy 
RESP charge without addtional rerun of DFT but using mean value of the ESP charges calculated by jaguar software of equivalent atoms (call veloxchem atom identifier). \
If the group of equivalent atoms has reasonable distributed ESP charges which means small std deviation the average operate will be excecute and recalculate the value to satisify precision requirement. (to fix the issue caused by decimal precison like a -0.00007 unneutral system in gromacs)
# Output
The updated RESP charge itp file will be named by new**.itp in the subfolder with same name of input *01.mae file.\
The original *gro *itp *top file in the subfolder are generated by veloxchem forcefield generator with GAFF(for bond etc.) and UFF (unbonded LJ).\
The *xyz file in the subfolder with a note column of ESP charge read from the jaguar calculation result.
