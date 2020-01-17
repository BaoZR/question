## Validate the Relationships Between Integers in a String

You will be given a string consisting of a list of integers and their relationships to their neighboring integers. For instance:

```
"-15<-10<=0=0<5"
```

Test to see that all the relationships between the integers in the string are true. If they are, return `true`. If they are not, return `false`.

### Examples

```
validateTheRelationships("5>-1<0=0<-5>5=5") ➞ false
// This is false because 0 is not less than -5.

validateTheRelationships("-15<-10<=0=0<5") ➞ true

validateTheRelationships("0=807<1000<=1000>9990<-3605<=20") ➞ false
// This is false because 0 is not equal to 807.
```

### Notes

- This is a modifcation of Helen Yu's "Correct Signs" challenge.
- As the examples above show, there could be negative numbers in the string.
- The numbers will only be separated by: `=, <, >, >=, <=`
- Tests will not contain any spaces.



### solution

```java
import java.util.stream.IntStream;
public class Challenge {
  public static boolean validateTheRelationships(String str) {
      //opers代表操作符
	String[] nums = str.replaceAll("[^-\\d]", " ").split("\\s+");//复习[^ ]
    String[] opers = str.replaceAll("[-\\d]", " ").trim().split("\\s+");//优美的替换
    return IntStream.range(0, nums.length - 1)
        .mapToObj(i -> nums[i] + " " + opers[i] + " " + nums[i + 1])
        .allMatch(s -> validCompare(s));
  }
	
private static boolean validCompare(String s) {
	String[] strs = s.split(" ");
	int n1 = Integer.parseInt(strs[0]);
	String oper = strs[1];
	int n2 = Integer.parseInt(strs[2]);

	switch (oper) {
  		case "<=": return n1 <= n2;
  		case ">=": return n1 >= n2;
  		case "<": return n1 < n2;
  		case ">": return n1 > n2;
 		case "=": return n1 == n2;
			default: return false;
		}
	}
}
```
