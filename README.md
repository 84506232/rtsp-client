# rtsp-client
RTSP_Stream_Init(CallBackFunc) callbackfunc get rtsp data

live555编译方法：
	1.解压live555后，将config.armlinux中toolchain改成自己的，并添加-DLOCALE_NOT_USED -fPIC
		CROSS_COMPILE?=		arm-linux-gnueabihf-
		COMPILE_OPTS =		$(INCLUDES) -I. -O2 -DSOCKLEN_T=socklen_t -DNO_SSTREAM=1 -D_LARGEFILE_SOURCE=1 -D_FILE_OFFSET_BITS=64 -DLOCALE_NOT_USED -fPIC
	2.生成MakeFile并编译：
		./genMakefiles armlinux
	3.将install.sh脚本拷贝到live目录，运行后将Live555-LIB下面的include和lib拷贝到rtspliblive对应的include和lib目录
		
rtspliblive编译方法：
	1. cd rtspliblive/src
	2. make clean;make
	
		get libRtspStream.so in rtspliblive/src
		如需编译静态库改一下makefile：
		    #link dynamic lib
			$(CPP) -shared -o $(PROGRAM)  $(OBJECTS) $(LDLIBS)
			
			#link static lib
			#@for var in $(LDLIBS); do ar x $$var; done
			#ar rcs $(PROGRAM) $(OBJECTS) *.o
			#rm -f *.o

rtsp_liveclient编译方法：
	1.解压后，将libRtspStream.so拷贝进去
	4.make clean;make

Demo运行方法：
	1.将rtspclient和config.txt放到同一目录，
	2.如果没有将libRtspStream.so打包进软件，在运行前export libRtspStream.so到LD_LIBRARY_PATH
	3.运行demo： ./rtspclient config.txt
