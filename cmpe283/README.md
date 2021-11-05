Questions:

1) Did the lab by myself.
2) Steps used to complete the assignment:
	- I forked the kernel source from the master linux git repository (https://github.com/torvalds/linux.git) to my github repo (https://github.com/serdardemirci55/linux).

	- Configured a GCP vm that has the VMX enable (refer to https://cloud.google.com/compute/docs/instances/nested-virtualization/enabling)

	  	#Create GCP vm
	  	gcloud compute instances create cmpe283 \
	  	--enable-nested-virtualization \
	  	--zone=us-central1-b \
	  	--min-cpu-platform="Intel Haswell" \
	  	--image-family=projects/ubuntu-os-cloud/global/images/family/ubuntu-1604-lts \
	  	--boot-disk-size=50GB

	  	#Check VMX enabled, should return non-zero value
  		grep -cw vmx /proc/cpuinfo

  	- Installed make tool and gcc compiler to my GCP vm:

  		sudo apt install gcc make

  	- Cloned my repo to the GCP vm:

  		git clone git@github.com:serdardemirci55/linux.git

  	- Downloaded the cmpe283.c source file source and MakeFile file to the GCP vm.

  	- I added codes to the cmpe283.c that read, interpret the VMX configuration MSRs to ascertain support capabilities/features, and print to the dmesg for the group's ◦Entry / Exit / Procbased / Secondary Procbased / Pinbased controls.

  	- Run make comamnd undeer the same directory with cmpe283.c and MakeFile.
  		make (will create .ko file)

  	- Inserted the module

  		sudo insmod cmpe283-1.ko 

  	- Checked the dmesg log:

  		dmesg

  	- Seen the log starting with "CMPE 283 Assignment 1 Module Start" which added the github as dmesg.out

  	- Removed the module

  		sudo rmmod cmpe283-1


