# Cadence Generic FinFET PDK OpAmp

This design is a basic OpAmp, designed for the Cadence Generic FinFet 
(12nm-16nm equivalent) PDK.
It includes schematics and testbenches with performance metrics. 
It requires Virtuoso and Spectre to run the simulation and electrical 
verification flow. PVS and QRC are recommended for layout verification flow.

## Testcase setup. 

### Setup GPDK

In addition to the testcase file (which contained this README), 
you need to download and untar and unzip the ADVGPDK: 
https://support.cadence.com/apex/ArticleAttachmentPortal?id=a1Od000000051TqEAI&pageName=GPDKs
From this page, download the ADVGPDK (Version 0.5) - Advanced Node PDK: cds_ff_mpt_v_0.5

Note: Downloading a GPDK requires a login to http://support.cadence.com. 
Current customers and any universities which are part of the Cadence Academic 
Network should be able to get support.cadence.com login access. For current
customers please contact Cadence support to get a login. If you are a 
university student or professor, please contact Elias (information below) if
you don't already have a login.

Untar this in an accessible location as well.

### setup.csh

Ensure you are in the opamp_gpdk_finfet directory.
Edit the setup.csh file, you need to set the following environment variables:
All of these should already be at the top of the file, just edit the paths for
your environment.

1. CDSHOME - Set the path to the Virtuoso installation, we have tested most recently with ICADVM18.1 ISR8
2. MMSIMHOME - Set the path to the Spectre installation, we have tested most recently with Spectre 191 ISR2
3. PVEHOME - Set the path to PVS for LVS and DRC
4. QRC_HOME - Set the path to QRC for extraction
5. CDS_LIC_FILE - The address of your Cadence license server (usually 5280@<hostname>)
6. GPDKFFHOME - Path to the cds_ff_mpt_v_0.5 that you installed above

Once it is set, save and do: `source setup.csh`

## Open the design

In the opamp_gpdk_finfet directory, start virtuoso: `virtuoso &`

### Design Schematic

Lib: Two_Stage_OpAmp
Cell: bias_amp
View: schematic

### Testbench Schematics

Lib: Two_Stage_OpAmp
Cell: bias_amp_AC
View: schematic

Lib: Two_Stage_OpAmp
Cell: bias_amp_TRAN
View: schematic

### Simulation Setup and Run

Open:

Lib: Two_Stage_OpAmp
Cell: bias_amp
View: maestro

This has the full simulation configuration to run both testbenches and 
extract some performance metrics. With "Single Run, Sweeps and Corners" selected
as the run mode in the top toolbar, simply click the green "Play" button or
in the "Run" menu select the "Single Run, Sweeps and Corners" 

Current results with testing at Cadence are showing:
- TRAN, Swing = 988.6mV
- TRAN, SettlingTime = 10.52 ns
- AC, UGF = 304M
- AC, Gain = 35.66

# Questions & Answers

If you run into any issues or problems, please contact Elias Fallon <fallon@cadence.com>
