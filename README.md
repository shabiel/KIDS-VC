# KIDS Version Control Extensions
Developed by Sam Habiel, who needs money more than fame; but a rich wife will do.

## Introduction
VISTA is really behind modern development practices that include Unit Testing, versioning, automated regression testing upon check-in, and logging. A lot of these issues have been remedied by Dr. Joel Ivey in various tools for deveopers, notably the Unit Testing framework and the M-plugin for Eclipse which is a great VISTA development environment.

A huge challenge in the VISTA world is how to version its components for version control. Versioning source routines is easily done in GT.M due to its exposure of all routines as source system files, yet the challenge remains of how to version other VISTA components. Previous attempts to do that (e.g. the VISTA Imaging approach) are in my opinion difficult to use and rather unelegant. This project provides a native VISTA solution. At this point, you need to have access to the File system to perform the version control, but this code should provide everything else that is needed. The envisioned target version control system is git.

The way the M routines work is that they decompose either a KID build on the VISTA system or a KID build located on the host file system into components based on the KID format into the File system. The files are deposited in the Kernel Primary Directory. The XPDOS file takes care of all File system operations. Cache and GT.M are supported on Windows and all Unix-like operating systems.

## Installation
The file `XPD_8P0_11310.KID` is a normal KID file. Here's a sample installtion:

	RPMS>D DT^DICRW,HOME^%ZIS,^XPDIL,^XPDI


	Enter a Host File: C:\Users\shabiel\workspace\KIDS-VC\XPD_8P0_11310.KID

	KIDS Distribution saved on Sep 01, 2014@15:25:18
	Comment: KIDS Version Control

	This Distribution contains Transport Globals for the following Package(s):
	Want to Continue with Load? YES//
	Loading Distribution...

	   XPD*8.0*11310
	Use INSTALL NAME: XPD*8.0*11310 to install this Distribution.

	Select INSTALL NAME: <SPACEBAR ENTER>   XPD*8.0*11310     Loaded from Distribution     Loaded fr
	om Distribution  9/8/14@11:26:29
	     => KIDS Version Control  ;Created on Sep 01, 2014@15:25:18

	This Distribution was loaded on Sep 08, 2014@11:26:29 with header of
	   KIDS Version Control  ;Created on Sep 01, 2014@15:25:18
	   It consisted of the following Install(s):
	  XPD*8.0*11310
	Checking Install for Package XPD*8.0*11310

	Install Questions for XPD*8.0*11310


	Want KIDS to Rebuild Menu Trees Upon Completion of Install? NO//


	Want KIDS to INHIBIT LOGONs during the install? NO//
	Want to DISABLE Scheduled Options, Menu Options, and Protocols? NO//
					 XPD*8.0*11310
	qqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqq
	 Installing Routines:
		       Sep 08, 2014@11:26:33

	 Installing PACKAGE COMPONENTS:

	 Installing OPTION
		       Sep 08, 2014@11:26:33

	 Updating Routine file...

	 Updating KIDS files...

	 XPD*8.0*11310 Installed.
		       Sep 08, 2014@11:26:34

	 Not a VA primary domain

	 NO Install Message sent
	qqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqq
		  lqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqk
	  100%    x             25             50             75               x
	Complete  mqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqj


	Install Completed

## Usage on development systems
There are two supported menu options, both of them placed on the KIDS 'Edits and Distributions' menu `[XPD DISTRIBUTION MENU]`.

	   VC1    Export for version control comp from a local build [XPD VC BUILD]
	   VC2    Export for version control components from a file [XPD VC FILE]

The first one exports a local build. At this time, only primary builds are supported. Wrapper multibuilds created as a KID build and global distributions are not supported. Don't worry; there is a DIC("S") which will prevent you from selecting them. The second one loads a build from the host file system and breaks it down. I believe it handles multibuilds, but I haven't tried. It used to! Global distributions are not supported here either.

It's worth distinguishing where the Version Controlled files get spit out. In a local build, they are spit out at the Primary HFS Directory configured in the Kernel in a OSEHRA formatted directory name (see below). On a KID build imported from the file system, an OSEHRA formatted directory name is created in the same location as the original KID build.

An OSEHRA formatted directory name is like this: `XPD*8.0*11310` becomes `XPD_8.0_11310`; `ABM 2.6` stays as `ABM 2.6`.

Here are a couple of examples, one for each option.

### VC1
	Select Edits and Distribution Option: VC1  Export for version control comp from a local build
	Select BUILD NAME: BI,8
	     1   BI*8.0*1       IMMUNIZATION     IMMUNIZATION
	     2   BI*8.0*2       IMMUNIZATION     IMMUNIZATION
	     3   BI*8.1*1       IMMUNIZATION     IMMUNIZATION
	     4   BI*8.2*1       IMMUNIZATION     IMMUNIZATION
	     5   BI*8.3*1       IMMUNIZATION     IMMUNIZATION
	Press <RETURN> to see more, '^' to exit this list, OR
	CHOOSE 1-5:
	     6   BI*8.3*3       IMMUNIZATION     IMMUNIZATION
	     7   BI*8.3*4       IMMUNIZATION     IMMUNIZATION
	     8   BI*8.4*1       IMMUNIZATION     IMMUNIZATION
	     9   BI*8.4*2       IMMUNIZATION     IMMUNIZATION
	     10  BI*8.5*1       IMMUNIZATION     IMMUNIZATION
	Press <RETURN> to see more, '^' to exit this list, OR
	CHOOSE 1-10:
	     11  BI*8.5*2       IMMUNIZATION     IMMUNIZATION
	     12  BI*8.5*3       IMMUNIZATION     IMMUNIZATION
	     13  BI*8.5*4       IMMUNIZATION     IMMUNIZATION
	     14  BI*8.5*5       IMMUNIZATION     IMMUNIZATION
	     15  BI*8.5*6       IMMUNIZATION     IMMUNIZATION
	Press <RETURN> to see more, '^' to exit this list, OR
	CHOOSE 1-15:
	     16  BI*8.5*7       IMMUNIZATION     IMMUNIZATION
	     17  BI*8.5*8       IMMUNIZATION     IMMUNIZATION
	CHOOSE 1-17: 17  BI*8.5*8     IMMUNIZATION     IMMUNIZATION
	     BI*8.5*8...

	Transport Global ^XTMP("XPDT",4492) created for BI*8.5*8



	Exporting Patch BI*8.5*8
	Exporting at C:\HFS\BI_8.5_8\KIDComponents\
	Wrote Build.zwr
	Exporting files DD and Data to Files/
	Exported 9002084.33+BI TABLE ERROR CODE.DD.zwr
	Exported 9002084.81+BI TABLE CONTRA REASON.DD.zwr
	Exported 9002084.91+BI TABLE DATA ELEMENT.DD.zwr
	Exported 9002084.33+BI TABLE ERROR CODE.Data.zwr
	Exported 9002084.81+BI TABLE CONTRA REASON.Data.zwr
	Exported 9002084.91+BI TABLE DATA ELEMENT.Data.zwr
	Wrote Package.zwr
	Wrote KernelFMVersion.zwr
	Wrote EnvironmentCheck.zwr
	Wrote PostInstall.zwr
	Wrote RequiredBuild.zwr
	Wrote InstallQuestions.zwr
	Exporting these routines to C:\HFS\BI_8.5_8\KIDComponents\Routines\
	BIENVCHK BIEXPRT3 BIEXPRT4 BIEXPRT6 BILOGO BINTEG BIPATUP BIPATUP1 BIPATUP2 BIPA
	TVW1 BIPATVW3 BIPOST BISITE1 BISITE2 BISITE3 BISITE4 BITN BITN2 BIUTL11 BIUTL2 B
	IUTL5 BIUTL8 BIXTCH
	Wrote ORD.zwr for FORM
	Exported BI FORM-CASE DATA EDIT.zwr in FORM
	Wrote ORD.zwr for PROTOCOL
	Exported BI MENU PATIENT VIEW.zwr in PROTOCOL
	Exported BI IMMUNIZATION VISIT EDIT.zwr in PROTOCOL
	Exported BI HEALTH SUMMARY.zwr in PROTOCOL
	Exported BI IMMUNIZATION VISIT DELETE.zwr in PROTOCOL
	Exported BI IMMUNIZATION VISIT ADD.zwr in PROTOCOL
	Exported BI SKIN TEST VISIT ADD.zwr in PROTOCOL
	Exported BI PATIENT CASE DATA EDIT.zwr in PROTOCOL
	Exported BI CONTRAINDICATIONS.zwr in PROTOCOL
	Exported BI LETTER PRINT INDIVIDUAL.zwr in PROTOCOL
	Exported BI BLANK.zwr in PROTOCOL
	Exported BI MENU PATIENT VIEW ONLY.zwr in PROTOCOL
	Exported BI PATIENT PROFILE VIEW.zwr in PROTOCOL
	Exported BI OFFICIAL IMM REC PRINT.zwr in PROTOCOL

File system view using the Windows tree command (I didn't know there was one!!):

	C:\HFS\PX_1.0_201>tree /f
	Folder PATH listing for volume Windows7_OS
	Volume serial number is 3A9E-458F
	C:.
	+---KIDComponents
	    ¦   Build.zwr
	    ¦   InstallQuestions.zwr
	    ¦   KernelFMVersion.zwr
	    ¦   Package.zwr
	    ¦   PostInstall.zwr
	    ¦   RequiredBuild.zwr
	    ¦
	    +---Files
	    ¦       9000010.11+V IMMUNIZATION.DD.zwr
	    ¦       920+VACCINE INFORMATION STATEMENT.Data.zwr
	    ¦       920+VACCINE INFORMATION STATEMENT.DD.zwr
	    ¦       920.1+IMMUNIZATION INFO SOURCE.Data.zwr
	    ¦       920.1+IMMUNIZATION INFO SOURCE.DD.zwr
	    ¦       920.2+IMM ADMINISTRATION ROUTE.Data.zwr
	    ¦       920.2+IMM ADMINISTRATION ROUTE.DD.zwr
	    ¦       920.3+IMM ADMINISTRATION SITE -BODY-.Data.zwr
	    ¦       920.3+IMM ADMINISTRATION SITE -BODY-.DD.zwr
	    ¦       9999999.04+IMM MANUFACTURER.Data.zwr
	    ¦       9999999.04+IMM MANUFACTURER.DD.zwr
	    ¦       9999999.14+IMMUNIZATION.DD.zwr
	    ¦       9999999.41+IMMUNIZATION LOT.DD.zwr
	    ¦
	    +---INPUT TEMPLATE
	    ¦       ORD.zwr
	    ¦       PXV IMM EDIT WITH CVX.zwr
	    ¦
	    +---OPTION
	    ¦       ORD.zwr
	    ¦       PXTT EDIT IMMUNIZATIONS.zwr
	    ¦
	    +---Routines
		    PXVP201.header
		    PXVP201.m
		    PXVPST01.header
		    PXVPST01.m
		    PXVUTIL.header
		    PXVUTIL.m

### VC2
	Select Edits and Distribution Option: VC2  Export for version control components from a file
	Enter a file to import then break down: C:\HFS\PX_1_201_T1.KID


	Exporting Patch PX*1.0*201
	Exporting at C:\HFS\PX_1.0_201\KIDComponents\
	Wrote Build.zwr
	Exporting files DD and Data to Files/
	Exported 920+VACCINE INFORMATION STATEMENT.DD.zwr
	Exported 920.1+IMMUNIZATION INFO SOURCE.DD.zwr
	Exported 920.2+IMM ADMINISTRATION ROUTE.DD.zwr
	Exported 920.3+IMM ADMINISTRATION SITE -BODY-.DD.zwr
	Exported 9000010.11+V IMMUNIZATION.DD.zwr
	Exported 9999999.04+IMM MANUFACTURER.DD.zwr
	Exported 9999999.14+IMMUNIZATION.DD.zwr
	Exported 9999999.41+IMMUNIZATION LOT.DD.zwr
	Exported 920+VACCINE INFORMATION STATEMENT.Data.zwr
	Exported 920.1+IMMUNIZATION INFO SOURCE.Data.zwr
	Exported 920.2+IMM ADMINISTRATION ROUTE.Data.zwr
	Exported 920.3+IMM ADMINISTRATION SITE -BODY-.Data.zwr
	Exported 9999999.04+IMM MANUFACTURER.Data.zwr
	Wrote Package.zwr
	Wrote KernelFMVersion.zwr
	Wrote PostInstall.zwr
	Wrote RequiredBuild.zwr
	Wrote InstallQuestions.zwr
	Exporting these routines to C:\HFS\PX_1.0_201\KIDComponents\Routines\
	PXVP201 PXVPST01 PXVUTIL
	Wrote ORD.zwr for INPUT TEMPLATE
	Exported PXV IMM EDIT WITH CVX.zwr in INPUT TEMPLATE
	Wrote ORD.zwr for OPTION
	Exported PXTT EDIT IMMUNIZATIONS.zwr in OPTION

File system view using the Windows tree command: 

	C:\HFS\PX_1.0_201>tree /f
	Folder PATH listing for volume Windows7_OS
	Volume serial number is 3A9E-458F
	C:.
	+---KIDComponents
	    ¦   Build.zwr
	    ¦   InstallQuestions.zwr
	    ¦   KernelFMVersion.zwr
	    ¦   Package.zwr
	    ¦   PostInstall.zwr
	    ¦   RequiredBuild.zwr
	    ¦
	    +---Files
	    ¦       9000010.11+V IMMUNIZATION.DD.zwr
	    ¦       920+VACCINE INFORMATION STATEMENT.Data.zwr
	    ¦       920+VACCINE INFORMATION STATEMENT.DD.zwr
	    ¦       920.1+IMMUNIZATION INFO SOURCE.Data.zwr
	    ¦       920.1+IMMUNIZATION INFO SOURCE.DD.zwr
	    ¦       920.2+IMM ADMINISTRATION ROUTE.Data.zwr
	    ¦       920.2+IMM ADMINISTRATION ROUTE.DD.zwr
	    ¦       920.3+IMM ADMINISTRATION SITE -BODY-.Data.zwr
	    ¦       920.3+IMM ADMINISTRATION SITE -BODY-.DD.zwr
	    ¦       9999999.04+IMM MANUFACTURER.Data.zwr
	    ¦       9999999.04+IMM MANUFACTURER.DD.zwr
	    ¦       9999999.14+IMMUNIZATION.DD.zwr
	    ¦       9999999.41+IMMUNIZATION LOT.DD.zwr
	    ¦
	    +---INPUT TEMPLATE
	    ¦       ORD.zwr
	    ¦       PXV IMM EDIT WITH CVX.zwr
	    ¦
	    +---OPTION
	    ¦       ORD.zwr
	    ¦       PXTT EDIT IMMUNIZATIONS.zwr
	    ¦
	    +---Routines
		    PXVP201.header
		    PXVP201.m
		    PXVPST01.header
		    PXVPST01.m
		    PXVUTIL.header
		    PXVUTIL.m

## Overview of the version control format and normalization of components
The entire objective of version control is to track changes and give the ability to merge changes together. It's secondarily used for release management, but I don't think we will do that with VISTA. To not introduce extranenous changes that KIDS introduces when exporting a build, several replacements had to be done which are completely non-destructive.

The version control format is very simple: it's the same format that KIDs uses for transporting globals, with some minor adjustments.

### Normalization of IENs treated by KIDS installation as insignificant
Through out KIDS, various elements are subscripted by the Build IEN. This IEN is completely arbitrary and depends on the build's IEN on the source system. To prevent "false positives" in diffs, the build IEN is replaced by the literal 'IEN'. For example,

	^XTMP("K2VC","EXPORT","BLD",IEN,0)="BI*8.5*8^IMMUNIZATION^0^3140908^y"
	^XTMP("K2VC","EXPORT","BLD",IEN,1,0)="^^1^1^3131125^"
	^XTMP("K2VC","EXPORT","BLD",IEN,1,1,0)="Imm v8.5, patch 7, with new TCH Forecaster."
	^XTMP("K2VC","EXPORT","BLD",IEN,4,0)="^9.64PA^9002084.81^3"
	^XTMP("K2VC","EXPORT","BLD",IEN,4,9002084.33,0)=9002084.33
	^XTMP("K2VC","EXPORT","BLD",IEN,4,9002084.33,222)="y^y^f^^n^^y^o^n"
	^XTMP("K2VC","EXPORT","BLD",IEN,4,9002084.81,0)=9002084.81
	^XTMP("K2VC","EXPORT","BLD",IEN,4,9002084.81,222)="y^y^f^^n^^y^r^n"
	^XTMP("K2VC","EXPORT","BLD",IEN,4,9002084.91,0)=9002084.91
	^XTMP("K2VC","EXPORT","BLD",IEN,4,9002084.91,222)="n^y^f^^n^^y^r^n"
	^XTMP("K2VC","EXPORT","BLD",IEN,4,"B",9002084.33,9002084.33)=""
	^XTMP("K2VC","EXPORT","BLD",IEN,4,"B",9002084.81,9002084.81)=""
	^XTMP("K2VC","EXPORT","BLD",IEN,4,"B",9002084.91,9002084.91)=""

IENs sent as part of transported data are preserved.

Normalization of IENs takes place as well in all Kernel compoents (Options, Parameters, Bulletins, etc.)

Each Kernel component has an ORD component which is also preserved.

Routines sent via KIDs get a build number appended on the second line. That is a false positive in a diff as it is completely immaterial. When routines are exported, the build number is taken out.

## Use Cases
### A bird's eye view of what's in a build
While the option `[XPD PRINT BUILD]` provides a good view of the components, it doesn't display transported data and doesn't display sub-components that KIDS sneaks in, like Blocks or Parameter values at the package level.
### Versioning of builds
Mulitple exports overwrite the previous export. If you initialize a version control system in the main directory, you can use your version control system's diff tools to see how the KID build changed.

For example, on VISTA,

	Select Edits and Distribution <TEST ACCOUNT> Option: vc1  Export for version con
	trol comp from a local build
	Select BUILD NAME:    XPD*8.0*11310     KIDS     KIDS
	     XPD*8.0*11310...

	Transport Global ^XTMP("XPDT",8948) created for XPD*8.0*11310

	Exporting Patch XPD*8.0*11310
	Exporting at C:\HFS\XPD_8.0_11310\KIDComponents\
	Wrote Build.zwr
	Wrote Package.zwr
	Wrote KernelFMVersion.zwr
	Wrote RequiredBuild.zwr
	Wrote InstallQuestions.zwr
	Exporting these routines to C:\HFS\XPD_8.0_11310\KIDComponents\Routines\
	XPDK2V0 XPDK2V1 XPDK2VC XPDOS
	Wrote ORD.zwr for OPTION
	Exported XPD DISTRIBUTION MENU.zwr in OPTION
	Exported XPD VC BUILD.zwr in OPTION
	Exported XPD VC FILE.zwr in OPTION

On the file system:

	C:\HFS>cd XPD_8.0_11310

	C:\HFS\XPD_8.0_11310>git init .
	Initialized empty Git repository in C:/HFS/XPD_8.0_11310/.git/

	C:\HFS\XPD_8.0_11310>git add .

	C:\HFS\XPD_8.0_11310>git status
	On branch master

	Initial commit

	Changes to be committed:
	  (use "git rm --cached <file>..." to unstage)

		new file:   KIDComponents/Build.zwr
		new file:   KIDComponents/InstallQuestions.zwr
		new file:   KIDComponents/KernelFMVersion.zwr
		new file:   KIDComponents/OPTION/ORD.zwr
		new file:   KIDComponents/OPTION/XPD DISTRIBUTION MENU.zwr
		new file:   KIDComponents/OPTION/XPD VC BUILD.zwr
		new file:   KIDComponents/OPTION/XPD VC FILE.zwr
		new file:   KIDComponents/Package.zwr
		new file:   KIDComponents/RequiredBuild.zwr
		new file:   KIDComponents/Routines/XPDK2V0.header
		new file:   KIDComponents/Routines/XPDK2V0.m
		new file:   KIDComponents/Routines/XPDK2V1.header
		new file:   KIDComponents/Routines/XPDK2V1.m
		new file:   KIDComponents/Routines/XPDK2VC.header
		new file:   KIDComponents/Routines/XPDK2VC.m
		new file:   KIDComponents/Routines/XPDOS.header
		new file:   KIDComponents/Routines/XPDOS.m


	C:\HFS\XPD_8.0_11310>git commit -m "Initial XPD*8.0*11310 components"
	[master (root-commit) 3315771] Initial XPD*8.0*11310 components
	 17 files changed, 1016 insertions(+)
	 create mode 100644 KIDComponents/Build.zwr
	 create mode 100644 KIDComponents/InstallQuestions.zwr
	 create mode 100644 KIDComponents/KernelFMVersion.zwr
	 create mode 100644 KIDComponents/OPTION/ORD.zwr
	 create mode 100644 KIDComponents/OPTION/XPD DISTRIBUTION MENU.zwr
	 create mode 100644 KIDComponents/OPTION/XPD VC BUILD.zwr
	 create mode 100644 KIDComponents/OPTION/XPD VC FILE.zwr
	 create mode 100644 KIDComponents/Package.zwr
	 create mode 100644 KIDComponents/RequiredBuild.zwr
	 create mode 100644 KIDComponents/Routines/XPDK2V0.header
	 create mode 100644 KIDComponents/Routines/XPDK2V0.m
	 create mode 100644 KIDComponents/Routines/XPDK2V1.header
	 create mode 100644 KIDComponents/Routines/XPDK2V1.m
	 create mode 100644 KIDComponents/Routines/XPDK2VC.header
	 create mode 100644 KIDComponents/Routines/XPDK2VC.m
	 create mode 100644 KIDComponents/Routines/XPDOS.header
	 create mode 100644 KIDComponents/Routines/XPDOS.m

On VISTA, make a few changes, completely up to you. I will edit some routines, change the verbage on the options, and add a required dependency. Then I will re-export it. Finally, I will create a diff (I usually just look at it rather than re-direct it to a file).

	C:\HFS\XPD_8.0_11310>git diff -w -u > xpd_8.0_11310.diff

Here's the complete diff:

	diff --git a/KIDComponents/Build.zwr b/KIDComponents/Build.zwr
	index 158aa30..8ab1ef1 100644
	--- a/KIDComponents/Build.zwr
	+++ b/KIDComponents/Build.zwr
	@@ -1,6 +1,6 @@
	 ^XTMP("K2VC","EXPORT","BLD",IEN,0)="XPD*8.0*11310^KIDS^0^3140908^y"
	 ^XTMP("K2VC","EXPORT","BLD",IEN,4,0)="^9.64PA^^"
	-^XTMP("K2VC","EXPORT","BLD",IEN,6.3)=5
	+^XTMP("K2VC","EXPORT","BLD",IEN,6.3)=6
	 ^XTMP("K2VC","EXPORT","BLD",IEN,"KRN",0)="^9.67PA^779.2^20"
	 ^XTMP("K2VC","EXPORT","BLD",IEN,"KRN",.4,0)=.4
	 ^XTMP("K2VC","EXPORT","BLD",IEN,"KRN",.401,0)=.401
	@@ -16,7 +16,7 @@
	 ^XTMP("K2VC","EXPORT","BLD",IEN,"KRN",9.8,"NM",1,0)="XPDK2V0^^0^B92910048"
	 ^XTMP("K2VC","EXPORT","BLD",IEN,"KRN",9.8,"NM",2,0)="XPDK2V1^^0^B25126356"
	 ^XTMP("K2VC","EXPORT","BLD",IEN,"KRN",9.8,"NM",3,0)="XPDK2VC^^0^B189402324"
	-^XTMP("K2VC","EXPORT","BLD",IEN,"KRN",9.8,"NM",4,0)="XPDOS^^0^B13271785"
	+^XTMP("K2VC","EXPORT","BLD",IEN,"KRN",9.8,"NM",4,0)="XPDOS^^0^B14234500"
	 ^XTMP("K2VC","EXPORT","BLD",IEN,"KRN",9.8,"NM","B","XPDK2V0",1)=""
	 ^XTMP("K2VC","EXPORT","BLD",IEN,"KRN",9.8,"NM","B","XPDK2V1",2)=""
	 ^XTMP("K2VC","EXPORT","BLD",IEN,"KRN",9.8,"NM","B","XPDK2VC",3)=""
	@@ -58,3 +58,7 @@
	 ^XTMP("K2VC","EXPORT","BLD",IEN,"KRN","B",8989.51,8989.51)=""
	 ^XTMP("K2VC","EXPORT","BLD",IEN,"KRN","B",8989.52,8989.52)=""
	 ^XTMP("K2VC","EXPORT","BLD",IEN,"KRN","B",8994,8994)=""
	+^XTMP("K2VC","EXPORT","BLD",IEN,"QUES",0)="^9.62^^"
	+^XTMP("K2VC","EXPORT","BLD",IEN,"REQB",0)="^9.611^1^1"
	+^XTMP("K2VC","EXPORT","BLD",IEN,"REQB",1,0)="KERNEL 8.0^1"
	+^XTMP("K2VC","EXPORT","BLD",IEN,"REQB","B","KERNEL 8.0",1)=""
	diff --git a/KIDComponents/OPTION/XPD VC BUILD.zwr b/KIDComponents/OPTION/XPD VC BUILD.zwr
	index a7ff632..929555b 100644
	--- a/KIDComponents/OPTION/XPD VC BUILD.zwr	
	+++ b/KIDComponents/OPTION/XPD VC BUILD.zwr	
	@@ -1,8 +1,9 @@
	 ^XTMP("K2VC","EXPORT","KRN",19,IEN,-1)="0^1"
	 ^XTMP("K2VC","EXPORT","KRN",19,IEN,0)="XPD VC BUILD^Export for version control comp from a local build^^R^^^^^^^^KIDS^y"
	-^XTMP("K2VC","EXPORT","KRN",19,IEN,1,0)="^^3^3^3140901^"
	+^XTMP("K2VC","EXPORT","KRN",19,IEN,1,0)="^^4^4^3140908^"
	 ^XTMP("K2VC","EXPORT","KRN",19,IEN,1,1,0)="This option lets you export version controlled components from a KIDS"
	-^XTMP("K2VC","EXPORT","KRN",19,IEN,1,2,0)="build on your system. Use this to version control builds from your system "
	-^XTMP("K2VC","EXPORT","KRN",19,IEN,1,3,0)="every time you create a build."
	+^XTMP("K2VC","EXPORT","KRN",19,IEN,1,2,0)="build located on your system. Use this along with a version control "
	+^XTMP("K2VC","EXPORT","KRN",19,IEN,1,3,0)="tool to version control builds from your system every time you create a"
	+^XTMP("K2VC","EXPORT","KRN",19,IEN,1,4,0)="build."
	 ^XTMP("K2VC","EXPORT","KRN",19,IEN,25)="EXPKIDIN^XPDK2VC"
	 ^XTMP("K2VC","EXPORT","KRN",19,IEN,"U")="EXPORT FOR VERSION CONTROL COM"
	diff --git a/KIDComponents/OPTION/XPD VC FILE.zwr b/KIDComponents/OPTION/XPD VC FILE.zwr
	index a1490a4..3ac876a 100644
	--- a/KIDComponents/OPTION/XPD VC FILE.zwr	
	+++ b/KIDComponents/OPTION/XPD VC FILE.zwr	
	@@ -1,6 +1,6 @@
	 ^XTMP("K2VC","EXPORT","KRN",19,IEN,-1)="0^2"
	 ^XTMP("K2VC","EXPORT","KRN",19,IEN,0)="XPD VC FILE^Export for version control components from a file^^R^^^^^^^^^y"
	-^XTMP("K2VC","EXPORT","KRN",19,IEN,1,0)="^^3^3^3140901^"
	+^XTMP("K2VC","EXPORT","KRN",19,IEN,1,0)="^19.06^3^3^3140908^^"
	 ^XTMP("K2VC","EXPORT","KRN",19,IEN,1,1,0)="This option loads a KIDs formatted HFS file into a temporary ^TMP "
	 ^XTMP("K2VC","EXPORT","KRN",19,IEN,1,2,0)="global, exports its contents in a version control format, and then "
	 ^XTMP("K2VC","EXPORT","KRN",19,IEN,1,3,0)="deletes the temporary ^TMP global. Use this to decompose an HFS KIDS file."
	diff --git a/KIDComponents/Routines/XPDOS.header b/KIDComponents/Routines/XPDOS.header
	index 3fa88e2..3004dad 100644
	--- a/KIDComponents/Routines/XPDOS.header
	+++ b/KIDComponents/Routines/XPDOS.header
	@@ -1 +1 @@
	-0^4^B13271785
	\ No newline at end of file
	+0^4^B14234500
	\ No newline at end of file
	diff --git a/KIDComponents/Routines/XPDOS.m b/KIDComponents/Routines/XPDOS.m
	index 23f6141..ac1fc44 100644
	--- a/KIDComponents/Routines/XPDOS.m
	+++ b/KIDComponents/Routines/XPDOS.m
	@@ -1,4 +1,4 @@
	-XPDOS ; VEN/SMH - KIDS Operating System Interface ;2014-03-31  1:27 PM
	+XPDOS ; VEN/SMH - KIDS Operating System Interface ; 9/8/14 1:33pm
	  ;;8.0;KERNEL;**11310**;Mar 28, 2014
	  ;
	  ; (C) Sam Habiel 2014, who needs more money than fame (but a rich wife will do!)
	@@ -71,9 +71,9 @@ D() ; [PUBLIC] $$ - Delimiter
	  QUIT  ; Decorative quit
	  ;
	 CD(ND) ; [PUBLIC] $$ - Change directory
	- I +$SY=47 S $ZD=ND Q $$PWD()
	- I +$SY=0 N % S %=$ZU(168,ND) Q $$PWD()
	- S $EC=",U-M-VM-NOT-SUPPORTED,"
	+ I +$SY=47 S $ZD=ND Q $$PWD() ; GT.M
	+ I +$SY=0 N % S %=$ZU(168,ND) Q $$PWD() ; Cache
	+ S $EC=",U-M-VM-NOT-SUPPORTED," ; Not GT.M or Cache
	  QUIT  ; Decorative quit
	  ;
	 RDPIPE(RTN,CMD) ; [PUBLIC] $$ - Execute a read only (non-interactive) command as a pipe
	@@ -85,11 +85,12 @@ RDPIPE(RTN,CMD) ; [PUBLIC] $$ - Execute a read only (non-interactive) command as
	  . N CNT S CNT=1
	  . N X F  R X:1 Q:$ZEOF  U $P D EN^DDIOL(X) S RTN(CNT)=X,CNT=CNT+1 U P  ; just loop around until we are done.
	  . C P
	+ ; Cache below. No return value as Cache pipe doesn't support that
	  I +$SY=0 D  Q 0
	- . O CMD:"QR"
	+ . O CMD:"QR" ; Open pipe (Queued, Read-Only)
	  . U CMD
	  . N CNT S CNT=1
	  . N X F  R X:1 Q:$ZEOF  U $P D EN^DDIOL(X) S RTN(CNT)=X,CNT=CNT+1 U CMD  ; ditto
	- . C CMD
	- S $EC=",U-M-VM-NOT-SUPPORTED,"
	+ . C CMD ; close pipe
	+ S $EC=",U-M-VM-NOT-SUPPORTED," ; Not Cache nor GT.M
	  QUIT  ; Decorative quit

### Extraction of components for later comparison
This would happen if you have components from two unrelated bulids that you want to compare together. For example, part of the examples shown above are immunization builds from VISTA and RPMS. Because I extracted them from the KID host files, I can diff them.

It turns out they have nothing in common, but it is educational none the less. We find out, for example, that the VA really decided to move all the files they can out of the IHS numberspace.

	C:\HFS>diff -r BI_8.5_8 PX_1.0_201

	Only in BI_8.5_8/KIDComponents: EnvironmentCheck.zwr
	Only in BI_8.5_8/KIDComponents/Files: .9002084.33+BI TABLE ERROR CODE.Data.zwr.swp
	Only in PX_1.0_201/KIDComponents/Files: 9000010.11+V IMMUNIZATION.DD.zwr
	Only in BI_8.5_8/KIDComponents/Files: 9002084.33+BI TABLE ERROR CODE.Data.zwr
	Only in BI_8.5_8/KIDComponents/Files: 9002084.33+BI TABLE ERROR CODE.DD.zwr
	Only in BI_8.5_8/KIDComponents/Files: 9002084.81+BI TABLE CONTRA REASON.Data.zwr

	Only in BI_8.5_8/KIDComponents/Files: 9002084.81+BI TABLE CONTRA REASON.DD.zwr
	Only in BI_8.5_8/KIDComponents/Files: 9002084.91+BI TABLE DATA ELEMENT.Data.zwr Only in BI_8.5_8/KIDComponents/Files: 9002084.91+BI TABLE DATA ELEMENT.DD.zwr
	Only in PX_1.0_201/KIDComponents/Files: 920.1+IMMUNIZATION INFO SOURCE.Data.zwr Only in PX_1.0_201/KIDComponents/Files: 920.1+IMMUNIZATION INFO SOURCE.DD.zwr
	Only in PX_1.0_201/KIDComponents/Files: 920.2+IMM ADMINISTRATION ROUTE.Data.zwr Only in PX_1.0_201/KIDComponents/Files: 920.2+IMM ADMINISTRATION ROUTE.DD.zwr
	Only in PX_1.0_201/KIDComponents/Files: 920.3+IMM ADMINISTRATION SITE -BODY-.Data.zwr
	Only in PX_1.0_201/KIDComponents/Files: 920.3+IMM ADMINISTRATION SITE -BODY-.DD.zwr
	Only in PX_1.0_201/KIDComponents/Files: 920+VACCINE INFORMATION STATEMENT.Data.zwr
	Only in PX_1.0_201/KIDComponents/Files: 920+VACCINE INFORMATION STATEMENT.DD.zwr

	Only in PX_1.0_201/KIDComponents/Files: 9999999.04+IMM MANUFACTURER.Data.zwr
	Only in PX_1.0_201/KIDComponents/Files: 9999999.04+IMM MANUFACTURER.DD.zwr
	Only in PX_1.0_201/KIDComponents/Files: 9999999.14+IMMUNIZATION.DD.zwr
	Only in PX_1.0_201/KIDComponents/Files: 9999999.41+IMMUNIZATION LOT.DD.zwr

### Reconstitution of a build from version controlled components (future)
This is not operational right now. It needs quite a bit of work. If you are interested, `LOAD^XPDK2V0` is the entry point. The mathematical proof of this tool working is that a loaded build will be the same as a exported build.

## Known bugs
### Holding on to directories
On Cache/Windows, probably as a side effect of `$ZSEARCH`, a handle is kept on the last used directory. I honestly haven't figure out how to get around it yet; it will probably be easy, but I didn't track it down. I use Sysinternals' Process Monitor and search for the process holding the directory. Sometimes I forget that I am on the directory in Explorer.

## Build Information

	PACKAGE: XPD*8.0*11310     Sep 08, 2014 1:58 pm                          PAGE 1
	-------------------------------------------------------------------------------
	TYPE: SINGLE PACKAGE                               TRACK NATIONALLY: YES
	NATIONAL PACKAGE: KIDS                           ALPHA/BETA TESTING: NO

	DESCRIPTION:

	ENVIRONMENT CHECK:                               DELETE ENV ROUTINE:
	 PRE-INIT ROUTINE:                          DELETE PRE-INIT ROUTINE:
	POST-INIT ROUTINE:                         DELETE POST-INIT ROUTINE:
	PRE-TRANSPORT RTN:

	ROUTINE:                                       ACTION:
	   XPDK2V0                                        SEND TO SITE
	   XPDK2V1                                        SEND TO SITE
	   XPDK2VC                                        SEND TO SITE
	   XPDOS                                          SEND TO SITE

	OPTION:                                        ACTION:
	   XPD DISTRIBUTION MENU                          USE AS LINK FOR MENU/ITEM/SUBS
	CRIBERS
	   XPD VC BUILD                                   SEND TO SITE
	   XPD VC FILE                                    SEND TO SITE

## Random tid-bits
 * Import and export of routines modified on the OS are done by GT's % routine.
 * Loading DD's from the file system can be done as follows (52 = file; 52.1 = file or subfile)

	M ^DD(52.1)=^XTMP("K2VC","EXPORT","^DD",52,52.1)
	S DA(1)=52.1,DIK="^DD(52.1," D IXALL^DIK

## Acknowledgements
Portions of the ZWRITE PEP were written by Maury Pepper. The actual ZWRITE implementation is my code.

OSEHRA funded the bulk of this work as part of the Patch Module project.

I also need to thank myself (!!) for spending an unfunded 30 hours making the tools work with KIDS and making the XPDOS work with Windows, which was not easy; plus the time to write this documentation of course.

-- Always interested in funding,

Sam Habiel
