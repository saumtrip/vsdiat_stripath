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




# Day 5 - Final steps for RTL2GDS using tritonRoute and openSTA










