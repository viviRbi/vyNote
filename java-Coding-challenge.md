```java
// Count duplicate

		 Scanner in = new Scanner(System.in);
	        String inputString = in.nextLine();

	        HashMap<String, Integer> b = new HashMap<>();

	        
	        String[] c = inputString.toCharArray();

	        for (int i =0; i < a.length; i ++){
	            if (b.get(c) == null ){
	                b.put(c , 1);
	            }else{
	                b.put(c, b.get(c) + 1)  ;
	            }
	        }
	        
	        Set<String> wordsInString = b.keySet();
	        
	        for (String word : wordsInString) {
	        	System.out.println(word + " : " + b.get(word));
	        }
	        
	        System.out.println(b);
/*
banana
a : 3
b : 1
n : 2
*/
```