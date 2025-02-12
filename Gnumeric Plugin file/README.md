# Interactive Register Debugging using Linux FIFOs
**Pre-requisites to be installed**: EUVM, Icarus Verilog, Gnumeric, GCC
## Steps to be followed
1. Clone this repository to your working directory
```
$cd path/to/your/working/directory 
$git clone  https://github.com/utkarshb1/Register-Debug-using-APB.git
```
2. Setting up plugins for Gnumeric <br/>
2.1 Make sure gnumeric is installed, if not run `sudo apt install gnumeric` in terminal <br/>
2.2 Install the Gnumeric Plugins by running `sudo apt install gnumeric-plugins-extra` in terminal <br/>
2.3 Enable Python plugins in Gnumeric. Open gnumeric go to Tools-> Plug-ins-> Check box Python Functions-> Close. <br/> 
2.3 Now in terminal, make directory: <br/>
```
$mkdir ~/.gnumeric 
$mkdir ~/.gnumeric/(version) 
$mkdir ~/.gnumeric/(version)/plugins 
$mkdir ~/.gnumeric/(version)/plugins/myfunc 
$cd ~/.gnumeric/(version)/plugins/myfuncs/ 
```

In the `path/to/your/working/directory/Register-Debug-using-APB/Gnumeric Plugin File/`, there's a `reg_vf.py` file, change the file locations of the fifos at line 30 and 31 to <br>
`apb_fifo = path/to/your/working/directory/Register-Debug-using-APB/sim/qemu_apb_req.fifo` and <br>
`fifo_read = path/to/your/working/directory/Register-Debug-using-APB/testbench/data.txt` respectively.

Now copy the plugin files from the `Gnumeric Plugin File` directory to the plugin directory created above in step 2.3.
```
$cp path/to/your/working/directory/Register-Debug-using-APB/Gnumeric Plugin File/reg_vf.py /home/user/.gnumeric/(version)/plugins/myfuncs/reg_vf.py
$cp path/to/your/working/directory/Register-Debug-using-APB/Gnumeric Plugin File/plugin.xml /home/user/.gnumeric/(version)/plugins/myfuncs/plugin.xml
```


3. Change the current directory to the following: `$cd path/to/your/working/directory/Register-Debug-using-APB/sim/` 

You can see various files in this directory.<br/>
3.1 To compile and run the Simulation, open terminal in this directory and run following commands:
```
make clean
make 
make run 
```

 **Note**: Make sure that EUVM is in your PATH, example `echo $PATH` = `/home/user/Intern_Project/euvm-1.0-beta14/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin`

4. In main directory, there’s file named : `apb_registers.gnumeric`

Open this file which will look like this:

https://drive.google.com/file/d/1AIRfKR8JHnrIB_fWDi3SesIcqLA6yFUF/view?usp=sharing
<br>
You can change the write data as per your convenience.

Now in an empty cell write function `=py_write(start_range:end_range)` where start_range and end_range are the cells of Gnumeric representing the data to be passed to the function and then hit enter. For eg, to perform write operation on Register 2, the arguments will be, `=py_write(B8:I8)`. If the write operation is successful you’ll be able to see the simulation in the terminal where it is running as well as a message “DONE” will be seen in Gnumeric cell.

Similar approach is for read operation, `=py_read(start_range:end_range)`

5 After you’re done with the simulation, write function `=py_exit()` in any empty cell to stop the Simulation.
