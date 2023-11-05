package 课堂作业;
import java.util.*;
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
}
