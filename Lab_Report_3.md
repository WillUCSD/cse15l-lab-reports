## Part 1 - Bugs
1. **Failure Inducing Bug**
   
- JUnit Test (Failure Inducing Input)
```
public void testReversed() {
    int[] input1 = {1,2,3};
    assertArrayEquals(new int[]{3,2,1 }, ArrayExamples.reversed(input1));
 }
```
- JUnit Test (Success Inducing Input)
```
public void testReverseInPlace() {
    int[] input1 = { 3 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{ 3 }, input1);
	}
```
- **Symptom**

![Image](/More_Images/Symptom.png)

- **The Bug (Before and After)**
  
Before
```
static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  }
```
After
```
static void reverseInPlace(int[] arr) {
    int[] temp = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      temp[i] = arr[arr.length - i - 1];
    }
    for (int i = 0; i < arr.length;i++) {
      arr[i] = temp[i];
    }
  }
```
- **How the fix adresses the issue**

The initial code fails as the same array is used for the source and destination. As such, when you are overwriting the original values of the array, these same values are then used again to overwrite the later values. In the end, the values of array are not properly reversed. This is fixed in the "After" code by adding `temp` to act as a temporary array for the destination. The original array is then changed to become equal to `temp` afterwards which is the properyly reversed version.
