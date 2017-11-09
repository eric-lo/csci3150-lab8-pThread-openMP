# Configuration {#configuration}

You can use`lscpu`to check the CPU configuration of your VM.

![](/assets/lscpu_1.png)

If you find \`CPU\(s\)' is 1 and Core\(s\) per socket is 1, which denotes that in your ubuntu virtual machine, you only have one cpu core.

As we need 4 core CPU for our assignment, therefore we need to change the default settings.

1. First shutdown the VM. Then go to VirtualBox Manager.
2. Right click your virtual machine -&gt; "Settings" -&gt; "System" -&gt;"Processor"
3. Change the number of processor\(s\) to **4**![](/assets/VM_ChangeCPU.png)
4. Restart your VM now and verify the setting by`lscpu`.![](/assets/lscpu_4.png)



