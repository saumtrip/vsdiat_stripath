# Day 1 -Inception of open-source EDA, OpenLANE and sky130 PDK
An introduction to and an overview of arduino boards, chips, die etc. 

![image](https://github.com/user-attachments/assets/9c4ef5ee-f37b-498a-b9b4-37cefcb906dd)

This is the complete RTL to GDS Flow- 

![image](https://github.com/user-attachments/assets/4c0e98a2-8870-45ce-a135-40945d0b4e88)

Directory structure of openlane- 

![image](https://github.com/user-attachments/assets/4ec9ff35-a6cc-4a7a-8ae0-347affc564c3)

./flow.tcl will run the entire process step wise- 

![image](https://github.com/user-attachments/assets/5342e097-3b26-4b4f-b18b-d86bcc73f323)

Design setup stage- 
![image](https://github.com/user-attachments/assets/d177f8cb-55dd-486b-b2bf-a84a4a03a596)

Command to run synthesis- run_synthesis

Objective- To find out flop ratio 
Flop ratio= Number of flip flops/Number of cells
          = 1013/14876 =  0.068
![image](https://github.com/user-attachments/assets/3680a294-50f3-4de9-b675-32cde44b9466)

# Day 2 - Good floorplan vs bad floorplan and introduction to library cells

![image](https://github.com/user-attachments/assets/0ded7a87-1b61-4068-9349-06f6941c5f68)

-Pre placed cells are fixed in the design before floor routing takes place. They need to be surrounded by decoupling capacitors. 
## Running floorplanning- 
-Run command- run_floorplan

![image](https://github.com/user-attachments/assets/108bd83d-ae87-4864-83ad-e688a843bdf5)

-Lower priority is given to system default (floorplanning.tcl), the next priority is given to config.tcl and then priority is given to PDK varient.tcl (sky130A_sky130_fd_sc_hd_congig.tcl).

-This is how floorplan def looks like-
![image](https://github.com/user-attachments/assets/bf4d9d9a-7e66-4a9b-adff-8b69c8996d6d)

![image](https://github.com/user-attachments/assets/5dac3c12-0d7a-4a21-9478-2b144f108c58)

-Standard cell placement view- 
![image](https://github.com/user-attachments/assets/45136dec-a76a-4725-89fc-3298234a0a3a)


# Day 3 - Design library cell using Magic Layout and ngspice characterization 

-Git cloning-

![image](https://github.com/user-attachments/assets/02185e1f-e6f1-4aaf-b946-5813e6227742)

-tech file view-

![image](https://github.com/user-attachments/assets/8e47fdf0-97db-439f-a507-eddceef3e95c)

-To extract spice netlist- 

![image](https://github.com/user-attachments/assets/86320c96-cbb2-472d-be37-743273c5ffe7)

![image](https://github.com/user-attachments/assets/59f93f36-62a9-4767-8602-f149e9123326)

-Spice deck- 
![image](https://github.com/user-attachments/assets/0c2c20a6-9bb5-4d3b-9580-cc4fcd39f04e)

-Visual representation of spice deck for reference- 

![image](https://github.com/user-attachments/assets/ed8d259a-5ae3-4ad0-aeea-63c6d701c09e)

- Include lib files for pshort and nshort in spice deck-
  
![image](https://github.com/user-attachments/assets/6c6c5480-7f06-49b1-9629-d80d8c0683af)

-After running spice-
![image](https://github.com/user-attachments/assets/b4ad77c2-018e-43d2-b938-4e5b21fe595b)

-Plot for y vs time- 

![image](https://github.com/user-attachments/assets/d79473b4-656b-48cd-ada0-9d820727e294)

-Fixing tech file violations-

![image](https://github.com/user-attachments/assets/a3a71ab1-bf90-4d15-af6a-358ebc8106c6)

![image](https://github.com/user-attachments/assets/06e0fd07-d796-4a8c-888e-600cb1ddfa9e)

![image](https://github.com/user-attachments/assets/302a8147-0f7c-4893-9b8e-93ec47e997c3)

# Day 4 - Pre-layout timing analysis and importance of good clock tree

-Mag viewer-

![image](https://github.com/user-attachments/assets/0d6c01fe-c239-4877-9a92-dfa87b012e2f)

-Help grid command in tkcon window will write command according to track file required

![image](https://github.com/user-attachments/assets/f81e490a-b113-42a8-b41b-9ece2c18b6a7)

![image](https://github.com/user-attachments/assets/ba03f592-5368-4e52-b8f5-59b4cd9b59e8)

We can set values and parameters for different ports etc. 
![image](https://github.com/user-attachments/assets/414d6de5-4ffa-41c1-91ab-d987aeb465d4)

-Configure synthesis settings to fix slack and include vsdinv-

We will give the following commmands in the terminal in openlane directory

prep -design picorv32a -tag 01-04_12-54 -overwrite

set lefs [glob $::env(DESIGN_DIR)/src/*.lef]

add_lefs -src $lefs

echo $::env(SYNTH_STRATEGY)

set ::env(SYNTH_STRATEGY) "DELAY 3"

echo $::env(SYNTH_BUFFERING)

echo $::env(SYNTH_SIZING)

set ::env(SYNTH_SIZING) 1

echo $::env(SYNTH_DRIVING_CELL)

run_synthesis

prep -design picorv32a -tag 01-04_12-54 -overwrite is used to overwrite the existing files with previous values of simulations.

After synthesis, we have observed that the slack is nagative.

wns(worst negative slack)= -23.89

tns(total negative slack)= -711.59.

-Now we run_synthesis and run_floorplan to see the effect of changes made on the chip area and slack value. 

-Commands for floorplan:
init_floorplan
place_io
tap_decap_or

Then, run_placement

![image](https://github.com/user-attachments/assets/17ebf9b5-2a65-4f99-bd5e-b1d6e869392f)


-Configuring OpenSTA for post-synth timing analysis-
 Run synthesis using the following commands in openlane directory-
 
docker
./flow.tcl -interactive
package require openlane 0.9
prep -design picorv32a
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs
set ::env(SYNTH_SIZING) 1
run_synthesis

![image](https://github.com/user-attachments/assets/3026838c-823c-4564-87ec-ba0d0cab947c)

-Make a new pre_sta.conf file now- 

![image](https://github.com/user-attachments/assets/0f0c0a91-2816-49da-a57f-0996e7861fff)

-my_base.sdc file defining environment variables:

![image](https://github.com/user-attachments/assets/10e2cfe8-9fdb-4297-90f7-b03d010a4bdb)

-Execute the sta pre_sta.conf command:

![image](https://github.com/user-attachments/assets/3d89f013-f0fa-4874-a30b-94d43b05c6ba)



## Optimize synthesis to reduce setup violations-

prep -design picorv32a -tag 02-04_05-27 -overwrite

set lefs [glob $::env(DESIGN_DIR)/src/*.lef]

add_lefs -src $lefs

set ::env(SYNTH_SIZING) 1

set ::env(SYNTH_MAX_FANOUT) 4

echo $::env(SYNTH_DRIVING_CELL)

run_synthesis

-Now, run the sta pre_sta.conf command in a new terminal in openlane directory itself,

![image](https://github.com/user-attachments/assets/a327af75-a308-40a7-94fc-f230aa501f81)

## Run CTS using Triton
-Floorplan, synthesis, CTS: 

![image](https://github.com/user-attachments/assets/d4789592-493b-4ca8-ad92-bbb366306a15)

![image](https://github.com/user-attachments/assets/4e3cf956-9fd9-48c3-9ad6-e10ec1aff62e)

![image](https://github.com/user-attachments/assets/ddefcb28-2ba7-4355-a158-3005d13bb0aa)


-To Generate the custom timing report

report_checks -fields {net cap slew input_pins} -digits 4

![image](https://github.com/user-attachments/assets/833c2499-f442-4ba3-b317-fd2531054876)

![image](https://github.com/user-attachments/assets/473081a7-268b-450d-8e8a-8aaa49f07427)


# Day 5 - Final steps for RTL2GDS using tritonRoute and openSTA

## Building power distribution network

-gen_pdn 

![image](https://github.com/user-attachments/assets/f78d20ef-955c-4950-8de7-fa65dceea542)

-The final generated layout looks like this:

![image](https://github.com/user-attachments/assets/e23f8122-3da9-4480-a767-f86ae3bc1df9)













