package 课堂作业;
import java.security.SecureRandom;
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;
import java.util.*;
import java.util.regex.Pattern;


public class 加密字符串 {
	public static void main(String[] args) {		
		Scanner sc=new Scanner(System.in);
		while(true) {
			System.out.println("==============================");
			System.out.println("欢迎使用密码管理系统");
			System.out.println("==============================");
			System.out.println("请选择操作:\n"+"1.加密\n"+"2.解密\n"+"3.判断密码强度\n"+
			"4.密码生成\n"+"5.退出");
			System.out.println("请输入选项序号:");
		int n=sc.nextInt();
		if(n==1) {
			encrypt();
		}
		else if(n==2) {
			decrypt();
		}
		else if(n==3) {
			judge();
		}
		else if(n==4) {
			generate();
		}
		else if(n==5) {
			break;
		}
	}
}

	public static void encrypt() {
		Scanner sc=new Scanner(System.in);
		String password;			
		while(true) {
			System.out.println("请输入密码:");	
			password=sc.nextLine();
			if(password.length()<16) {
				break;
			}
			else {
				System.out.println("请输入正确格式的密码:");				
			}
		}			
		char[]arr=password.toCharArray();
	    int[]a=new int[arr.length];
	        for (int i = 0; i < arr.length; i++) {	        	
	            a[i]=(int)arr[i]+(i+1)+3;
	        }
	    int temp=a[0];
	    a[0]=a[a.length-1];
	    a[a.length-1]=temp;//创建临时变量，将字符串的第一位和最后一位调换顺序
	        for (int i = 0; i < a.length; i++) {
	            arr[i]=(char)a[i];
	        }
	    String point=new String(arr);
	    StringBuffer s=new StringBuffer(point);
	    s.reverse();//利用SttingBuffer的内置reverse方法反转字符串
	    String newpassword= s.toString();
	    System.out.println("加密后的结果是："+newpassword);
	    }
    public static void decrypt() {
    	Scanner sc=new Scanner(System.in);
		String password;		
		while(true) {
			System.out.println("请输入密码:");
			password=sc.nextLine();
			if(password.length()<16) {
				break;
			}
			else {
				System.out.println("请输入正确格式的密码:");				
			}
		}
		StringBuffer b=new StringBuffer(password);
		char[]arr=b.reverse().toString().toCharArray();
		int temp=arr[0];
		arr[0]=arr[arr.length-1];
		arr[arr.length-1]=(char) temp;
		int[]a=new int[arr.length];
		    for (int i = 0; i < arr.length; i++) {
	            a[i]=(int)arr[i]-(i+1)-3;
        }
		    String Initialpassword=a.toString();
		    System.out.println("解密后的结果是："+Initialpassword);
    }     
    public static void judge() {
    	Scanner sc=new Scanner(System.in);
		String password;
		String weakIntensity="^[0-9]{0,8}+$||^[0-9a-z]{8,}+$||[0-9A-Z]{8,}+$";
		String medialIntensity="^(?![0-9]+$)(?![a-zA-Z]+$)[0-9a-z\\W][0-9A-Z\\\\W]{8,}+$";
		String highIntensity="^(?=.*[A-Za-z])(?=.*\\d)[A-Za-z\\d]{8,}+$";
		while(true) {
			System.out.println("请输入密码:");
			password=sc.nextLine();
			if(password.matches(weakIntensity)) {
	        	System.out.println("该密码为弱强度");
	        	break;
	        }	        
			else if(password.matches(medialIntensity)) {
	        	System.out.println("该密码为中强度");
	        	break;
	        }	        
			else if(password.matches(highIntensity)) {
	        	System.out.println("该密码为高强度");
	        	break;
	        }
	        else {
				System.out.println("请输入正确格式的密码");			
				}
		}
    }
        private static final String lowStr = "abcdefghijklmnopqrstuvwxyz";        
        private static final String numStr = "0123456789";               
        public static void generate() { 
        	for (int i = 0; i < 8; i++) {               
            	int num=8;             	    	
        	System.out.println("您的密码是:"+getRandomPwd(1));
        	}
        }
        private static char getRandomChar(String str) {
            SecureRandom random = new SecureRandom();
            return str.charAt(random.nextInt(str.length()));
        }    	
        private static char getLowChar() {
            return getRandomChar(lowStr);
        }
        private static char getUpperChar() {
            return Character.toUpperCase(getLowChar());
        }

        private static char getNumChar() {
            return getRandomChar(numStr);
        }                  
        private static char getRandomChar(int funNum) {
            switch (funNum) {
                case 0:
                    return getLowChar();
                case 1:
                    return getUpperChar();
                default:
                    return getNumChar();
                }			
            }
        private static String getRandomPwd(int length) {
            if (length>20||length<8) {
                System.out.println("长度不满足要求");
                return "";
            }
            List<Character> list = new ArrayList<>(length);
            list.add(getLowChar());
            list.add(getUpperChar());
            list.add(getNumChar());          

            for (int i = 3; i < length; i++) {
                SecureRandom random = new SecureRandom();
                int funNum = random.nextInt(3);
                list.add(getRandomChar(funNum));
            }

            Collections.shuffle(list);   // 打乱排序
            StringBuilder stringBuilder = new StringBuilder(list.size());
            for (Character c : list) {
                stringBuilder.append(c);
            }
            return stringBuilder.toString();
        }
}
