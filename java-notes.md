# JAVA

### Throws and Throw
- **Throws**: If there is a **check exception**, they should be handle, otherwise we will get compiler time error like ```error: unreported exception ...```. We prevent this compile tme error either by using a **try catch** block, or a **throws clause** to postpone it then handle the exception at the place the method called. It gives an information to the programmer that there may occur an exception so it is better for the programmer to provide the exception handling code.
- **Throw**: mainly use for throw custom exceptions. ```throw new ArithmeticException("Error")```. Instance must be a type or subclass of **throwable**. When throw, have to make sure it is the last line of code. We can re-throw the same error in a catch block.
```java
if (age < 18) throw new ArithmeticException("Not valid");
//Output: Exception in thread main java.lang.ArithmeticException:not valid
``` 
- **Throws vs Throw**
| **Throws** | **Throw** |
| :---- | :---- |
| Used to declare an exception | Used to explicity throw an exception |
| Check exception can be propagated (forwarded in calling chain) with throws | Check exception cannot be propagated with throw only |
| Followed by class (throws AbcException) | Follow by an instance (throw new AbcException("Error")) |
| Used with method signature | Used within the method |
| Can declare multiple exceptions | Cannot throw multiple exceptions |

| Left-Aligned  | Center Aligned  | Right Aligned |
| :------------ |:---------------:| -----:|
| col 3 is      | some wordy text | $1600 |
| col 2 is      | centered        |   $12 |
| zebra stripes | are neat        |    $1 |
### User define Exception
```java
public class NegativeStartingBalance extends Exception{
	public NegativeStartingBalance() 
		super("Error: Negative starting balance");
	public NegativeStartingBalance(double amount) 			
		super("Error: Negative starting balance " + double amount);
}
```
```java
public BankAccount(double startBalance) throws NegativeStartingBalance {
    if (startBalance < 0)
        throw new NegativeStartingBalance(startBalance);
}
```
```java
public class AccountTest{
	public static void main(String[] args){
		try BankAccount = new BankAccount(-100);
		catch (NegativeStartingBalance e)
			System.out.println(e.getMessage());
	}
}
// Output: Error: Negative Starting balance: -100
```
### Binary File
- When a data stored in binary file, it cannot be open in text editors
- Create a binary output file (to write)
```java
int[] numbers = {1,2,3,4};
FileOutputStream fsteam = new FileOutputStream("Number.dat");
DataOutputSteam outputFile = new DataOutputStream(fstream);
for (int i = 0; i < numbers.length; i++){
  outputFile.writeInt(numbers[i]);
  System.out.println("Done.");
}
outputFile.close();
```
- Create a binary input file (to read)
```java
FileInputStream fstream = new FileInputStream("Numbers.dat");
DataInputStream inputFile = new DataInputStream(fstream);
 
System.out.println("Reading numbers from the file:");
 
while (!endOfFile){
  try{
     number = inputFile.readInt();
      System.out.print(number + " ");
   } catch (EOFException e){
      endOfFile = true;
   }
 }
 
 System.out.println("Done.");
inputFile.close();
```