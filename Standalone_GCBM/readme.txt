Before you begin
---
Refer to moja.global's GCBM training video series before proceeding to run the model.

Description of contents
---
input_database\
    The GCBM input database for the project which contains all of the non-spatial model parameters, plus the files needed to generate
    the input database using the Recliner2GCBM tool.
    
    1. Modify the yield curves and create Growth_Curves.csv file using the ForestType, Distrubance and Climate classifiers
    2. Run the run_recliner2hcbm_gui tool to get a configuration
    2.1. Configuration: Project Type: Spatially explicit; Module Configuration: CBM Classic; AIDB Path: Path to
    ArchiveIndex_Beta_Install in input_database folder; Output type: SQLite; Path: path to gcbm_inpt database in input_database folder
    2.2. Added ForestType, Disturbance and CLimate classifiers on the Growth_Curves.csv file
    2.3. Selected the Growth_Curves.csv file, set the columns of the three classifiers; Growth Curve Interval set to 1; Increments in
    columns 4 to 154; Species in column 3
    2.4. No Transition rules configured for now
    2.5. No changes in disturbance categories (all disrturbances set as anthropogenic
    2.6. GCBM input database loaded and configuration saved in recliner2gcbm_config.json file

layers\
    The spatial layers for the project, both the originals and the output of the tiler script which processes the original layers into
    the format used by GCBM.
    
    3. Include a dummy inventory layer (inventory.shp) and a temperature layer 
     
processed_output\
    Contains the fully-processed (analysis ready) output of the simulation:
    Spatial output in GeoTIFF format, and database output in SQLite format.
    Analysis ready tables containing various ecosystem indicators are the tables prefixed with "v_".
    
tools\
    Tiler - Converts raster and vector layers into the format required by GCBM.
    
    4. Configure the tiler python code (toold/tyler/tyler.py):
    4.1. Resolution to 0.001 degrees (aprox 100 m)
    4.2. Change the classifier names in the inventory layer
    4.3. Change the age attribute name
    4.4. Delete the disturbance for now

---

To run the project (the short version):

Set up your Python environment and make any necessary modifications to run_all.bat as described in
    documentation\GCBM_Installation_Guide_2019_11_14.docx.
    
    5. Change the run_all simulations years (start, end)

---

To run the project (the detailed version):
    Install Python 3:
        If you have Python 3 already installed:
            From the command prompt in tools\python_3_installer, type:
            install_modules_only (path to existing Python installation)
            
            For example, if your computer already has 64-bit Python 3 installed
            in c:\Python37:
            install_modules_only c:\Python37
    
        If you do not have Python 3 installed:
            From the command prompt in tools\python_3_installer, type:
            install_python
            
    If you do not have MS Access installed, you will need to install a driver in order to connect to MS Access databases. The driver can
    be found in:
    tools\python_3_installer\x64\AccessDatabaseEngine_x64.exe
    
    Install the Visual C++ Redistributable packages required to run the GCBM and related tools:
        tools\VC_redist\2008\vcredist_x64.exe
        tools\VC_redist\2013\vcredist_x64.exe
        tools\VC_redist\2015\VC_redist.x64.exe
        tools\VC_redist\2017\VC_redist.x64.exe
        
    Install the .NET framework 4.7.2 redistributable package required to run the
    Recliner2GCBM tool:
        tools\VC_redist\NDP472-KB4054530-x86-x64-AllOS-ENU.exe
            
    Edit run_all.bat and set the GCBM_PYTHON path and PLATFORM variables in the USER CONFIGURATION section near the top to the correct
    values for your system.

    Run run_all.bat
