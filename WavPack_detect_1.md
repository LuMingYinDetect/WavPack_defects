Affected Version:
WavPack 5.6.0 029ab905a0c4d62da35349c4c09441f9864c70c3

Vulnerability Description:
The vulnerability is a memory leak bug located at line 120 of the file /WavPack/cli/caff_write.c. This vulnerability could potentially be exploited maliciously to cause resource exhaustion and denial of service attacks.

WavPack download address:
https://github.com/dbry/WavPack.git

Detailed Description of the Defect:

1.A variable named channel_identities is defined at line 94 in the file /WavPack/cli/caff_write.c, and a dynamic memory block is allocated for it using malloc. Subsequently, this variable is passed into the WavpackGetChannelIdentities function at line 105, as shown in the following diagram:

![image](https://github.com/LuMingYinDetect/WavPack_defects/blob/main/WavPack_1.png)

2.In the WavpackGetChannelIdentities function, the variable channel_identities is referred to as identities. In this function, only the values in identities are modified, and the pointer is not passed to any other pointer, as shown in the following diagram:

![image](https://github.com/LuMingYinDetect/WavPack_defects/blob/main/WavPack_2.png)

3.When the if statement at line 118 evaluates to true, the function will return at line 120, and consequently, the deallocation operation for the pointer channel_identities at line 280 will not be executed, leading to a memory leak defect, as illustrated in the following diagram:

![image](https://github.com/LuMingYinDetect/WavPack_defects/blob/main/WavPack_3.png)
