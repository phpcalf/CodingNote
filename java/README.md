# 你好，世界！![image](https://github.com/xx13295/wxm/blob/master/images/o.png?raw=true)

	public class HelloWorld {
		    public static void main(String ... args) {
		        System.out.println(randomString(-229985452)+' '+randomString(-147909649));
		    }
	
		    public static String randomString(int seed) {
		        Random rand = new Random(seed);
		        StringBuilder sb = new StringBuilder();
		        while(true) {
		            int n = rand.nextInt(27);
		            if (n == 0) break;
		            sb.append((char) ('`' + n));
		        }
		        return sb.toString();
		    }
	}