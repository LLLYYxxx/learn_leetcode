1、位与字节的关系
  首先在64位系统中：
  1位(bit)=1比特(bit)
  1字节(byte)=8位(bit)
（字与字节的关系根据系统不同有所区别）

2、本题思路

2-1、int类型数据占四个字节，在计算机中本身按二进制数存储，int类型占四个字节，那么根据字节(byte)与(bit)关系，int类型=32位比特。

2-2、16进制数在计算机中应该是以四位比特来表示的，那么一个int整数则应该由8个十六进制数来表示。
比如  1(int)=0x00000001
     17(int)=0x00000011
     26(int)=0x0000001a
     -1(int)=0xffffffff
     
2-3、可以用位运算& ，0xf(0000…..1111b)和num相与，取得每一个十六进制数。
  比如 0xf&21=5
      0xf&26=10=a(hex)
  每四位运算完成后num向右移动四位

   2-4、考虑负数的情况，负数在计算机系统中以补码形式表示
   
   负数向右移动不能保证num为0，则限制num向右移8次。一次四位。
   
   左移，后空缺自动补0；
   
   右移，分为逻辑右移和算数右移
   
   1）逻辑右移 不管是什么类型，空缺自动补0；
   
   2）算数右移 若是无符号数，则空缺补0，若是负数，空缺补1；
   
右移：

       class Solution {
    public:
        string toHex(int num) {
            if(num==0) return "0";
            string hex=“0123456789abcdef”,res="";
            while(num&&res.size()<8)
            {
                ans=hex[num&0xf]+res;
                num>>=4;
            }
            return res;
        }
     };

左移：


        class Solution{
    public:
        string toHex(int num){    
        if(num==0) return “0”;
        string hex =“0123456789abcdef”,res=“”; 
        int size=0;
        unsigned move =0xf;
        unsigned s=0x0;
        int trans = 0;
        while(size<8)
        {
            s=(num&calc)>>trans;
            move<<=4;
            res=hex[s]+res;
            size++;
            trans+=4;
        }
        for(j=0;j<8;j++)
        {
            if(res[j]!='0')
                break;
        }
        res=res.substr(j,res.size());
        return res;
  }

