Download Link: https://assignmentchef.com/product/solved-ece3610-lab1-introduction-to-arm-assembly-language-programming
<br>
This laboratory is an introduction to the operation and basic programming of the ARM Cortex A9 processor. For this laboratory we will be using the Intel <em>DE10-Standard</em> development board.  The FPGA on the board includes two ARM processors, in addition to the reprogrammable logic circuitry which you used in the prerequisite course ECE 2220.

<strong>IMPORTANT</strong>: The circuitry on the development board is sensitive to electrostatic discharge. Before handling components, ensure that you ground yourself in order to discharge any static electricity that may be present on your person. Grounding straps may be provided at your workstations for this purpose. Also, try to handle the board without making contact with pins and connectors.

<strong>NOTE</strong>: Before leaving the laboratory room, you need to demonstrate a working system to the teaching assistant.

<h1>Procedure</h1>

The ARM processor may be programmed in a high-level language (i.e. C, C++, Python, etc.), which is what is typically done when developing software for most computer systems. However, when working with system software at that level, much of the detail of what the processor is doing is not directly observable. While this separation can be considered an advantage of a high-level language, it is our objective in this course for you to understand the details of what the CPU is doing when it’s running programs and executing instructions. Therefore, we want to be able to monitor the CPU as it processes instructions and observe the low-level changes that happen along the way. In order to achieve that, we will be working with programs written in assembly language.

The programming tool we will be using is specifically intended for use with Intel/Altera FPGA development boards and is similar to the programming environment shown in the course textbook. The tool is called the <em>Intel FPGA Monitor Program</em> and can be found in Windows <em>Start</em> menu under the <em>Intel FPGA UP 18.0</em> folder, or through a shortcut icon on the desktop.

Connect the power supply to your <em>DE10-Standard</em> FPGA board, then connect a USB cable from your PC to the USB port just above the power connector. Power-on the board and launch the <em>Intel FPGA Monitor Program</em>. Once the programming tool loads, you will see the following application window.

The window is divided into separate sections (panes). The main section, titled <em>Disassembly</em> shows the version of the program code that is loaded into the processor. When executing the program in single-step mode (discussed later), this pane will highlight the current instruction and allow you to set breakpoints. The <em>Registers</em> pane shows the contents of the 16 internal registers within the processor. The <em>Info &amp; Errors</em> pane provides messages associated with the assembly and downloading of the machine code to the processor.

The first step in preparing to compile and execute a program is to create a new project to contain the project files. From the <em>File</em> menu select the <em>New Project…</em> menu item. This will open the <em>New Project Wizard</em>.

e first page of the wizard is shown in the figure to the right. Use the <em>Browse…</em> button to select a <em>Project Directory</em> that will hold your project files. <em>Note that the file path to this directory, and the directory name itself <strong>can not</strong> have spaces or the project will not compile properly later.</em> The <em>Project Name</em> field can be anything you like, but once again, it may not have spaces in the name. The <em>Project Name</em> does not need to be the same as the <em>Project Directory</em>, although in this example they happen to be the same. The last selection for this window is the <em>Architecture</em> of the processor for which the program is being assembled. For our purposes, this should always be set to <em>ARM Cortex-A9</em>.

Click <em>Next&gt;</em> to advance to the next page of the wizard.

This page of the wizard is used to select the target system on which the programs will be run. From the pop-up menu, choose <em>DE10-Standard Computer</em>. Doing so will auto-complete the remainder of the page.

Click Next&gt;.




e next page of the wizard concerns the type of

programs the project will be working with. In our case, we will be writing assembly code, so the <em>Program Type</em> should be set to <em>Assembly Program</em>.

This page also allows us to include code from several example programs. To do this, select the checkbox to <em>Include a sample program with this project</em>. We will start with a very simple example, appropriately titled <em>Simple Program</em>.

One these options have been chosen, click <em>Next&gt;</em>.

The page which follows allows you to add your own source files to the project. At this point we have no files to include beyond those already provided by the example program, so click <em>Next&gt;</em> to continue.

The next step is to select parameters for the processor in the FPGA. For the <em>Host Connection</em>, select <em>DE-SoC</em>, if it is not already selected.  If the Host Connection list is blank, then verify that your FPGA board is powered on and plugged into the PC. Then click the <em>Refresh</em> button to update the USB device list.

The FPGA contains two processors, which are able to run independent programs. For our purposes, we will only be using one of these. From the <em>Processor</em> list, select the <em>ARM_A9_HPS_arm_a9_0</em>.

The <em>Terminal</em> device can be left at its default value of <em>Semihosting</em>.

Once again, click <em>Next&gt;</em> to continue.

e final page of the wizard allows for selection of

memory settings. For the programs in this laboratory, the default <em>Basic</em> setting is what will be used.

At this point, clicking <em>Save</em> will create the project files in the project directory.

The ARM processor is one component within the FPGA chip. The processor is directly connected to some of the physical pins on the chip and through those pins to some of the devices on the development board. However, in order to connect the processor to other devices on the board, it is necessary to provide logical circuitry for the FPGA to make those connections. Fortunately, the project wizard has already included the design files needed to accomplish this, so there is no need to prepare one ourselves, in this case.

After saving the project configuration in the New Project Wizard (above), you will be offered the option of downloading the needed logic to the FPGA. Clicking <em>Yes</em> with bring you back to the original application window. In the <em>Info &amp; Errors</em> pane you will see the FPGA design file being compiled by Quartus and then downloaded to the board.

If you receive a warning from Windows Defender attempting to block the Java component of the tool from performing the download, simply choose <em>Cancel</em> to dismiss those warnings<em>.</em> After doing so, or any other time where the power to the board has been interrupted and therefore the FPGA configuration has been lost, simply choose the <em>Download System…</em> item from the <em>Actions</em> menu.

<h1>Assembling and Executing a Program</h1>

The entire process up to this point has prepared the development board and the software tool in preparation for the software. Now we are able to actually assemble the sample program and load it into the memory on the DE10 board so that the ARM processor can run it.

Below the <em>Edit</em> menu is the <em>Compile</em> button. Clicking that button will compile the assembly language program. To the right of the <em>Compile</em> button is the <em>Load</em> button. Clicking that button will copy the machine code into the main memory on the FPGA board ready for the ARM processor to execute it.

Once the load is complete, the additional program execution controls will become available below the <em>Help</em> menu and the Disassembly window will show the program, with the first instruction highlighted.

The program instructions shown in red are the instructions as they were written by the programmer. The instructions in green are the actual instructions that result from the assembly (compilation) of the programmer’s assembly code. Some modifications to the programmer’s code are made by the assembler in order to get the intended result while adjusting for some limitations of the instructions themselves.

Now that a program is actually loaded into the processor, the <em>Registers</em> pane shows the current contents of the processor’s registers. The ARM processor has 16 registers in total. Registers r0 through r12 are general purpose and can be used by the programmer to hold any 32-bit value as needed. The remaining three registers have specialized functions, so they are not shown as r13, r14, r15, but rather are given the special labels sp, lr, and pc. The last entry in the list is the cpsr, which in the ARM architecture is known as the <em>Current Processor Status Register</em>. It stores the condition code bits (N, Z, C, V) as the most significant 4 bits of the 32-bit word.




To execute the program, click on the green <em>Play</em> button (just below and slightly to the right of the Help menu). This will run the program, but will not actively update the view in the monitor window. To stop the execution, click the <em>Pause</em> button (to the right of the <em>Play</em> button). Alternatively, you can step through the program, one instruction at a time, by using the <em>Step</em> button (located right below the <em>Help</em> menu). When doing so, the highlighted instruction in the Disassembly pane tracks where the program is, while the Registers window updates (in red type) the registers which were just modified by the last instruction.

Step through the sample program, while changing the switch settings on the DE10 board and observe the changes which occur to the registers as this is done. Notice that the CPSR does not change, since none of the program instructions indicate that an update should be performed.

<h1>Modifying the Program</h1>

The <em>Intel FPGA Monitor Program</em> does not allow you to directly edit the assembly code.  That must be done in another text editor, such as <em>NotePad++</em>. The assembly code source file for the example above can be found in the file simple_program.s within your project directory.

For convenience in performing the program modifications below, a copy of Table 3.1 from the textbook is reproduced here for your reference. It is a short list of some basic assembly language instructions.

<ol>

 <li>For the first program modification, instead of simply reading the switch value and storing it directly to the LEDs, modify the code so that it now reads the switch value, multiplies that value by 16, and stores that result to the LEDs. Assemble the modified code and download it to the DE10. Run the program and describe how the LEDs now change in response to the switches.</li>

 <li>The second modification is intended for you to explore the behaviour of the status bits stored in the CPSR. Instead of simply reading the switch value and storing it directly to the LEDs, modify the code to read the switch value, subtract 8 from the value, and store that result to the LEDs. Use the version of the subtraction operation that updates the CPSR. Assemble the modified code and download it to the DE10. Both run and single-step through the program to see how it operates. Pay particular attention to the value of the status bits (most significant bits) in the CPSR.</li>

 <li></li>

</ol>

<table>

 <tbody>

  <tr>

   <td width="150"></td>

  </tr>

  <tr>

   <td></td>

   <td></td>

  </tr>

 </tbody>

</table>

<ul>

 <li>For the next modification we wish to explore the use of a branch (BEQ) statement. Change the code so that the value of the switches is read, and if the lowest-order switch is 0, then light the lowest 2 LEDs, while if it is 1, then light the top two LEDs. (The values of the other switches need not be considered.)</li>

</ul>

<ol start="4">

 <li>Finally, make your own modification of the original code (or further modify any of the above three changes in your own way). Describe what the modified code is intended to do, and verify its operation by running the code on the DE10.</li>

</ol>