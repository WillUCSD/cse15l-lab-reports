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

## Part 2 - Researching Commands 
**`grep` command-line options**

*1. `grep -i `: The command line option `-i` makes it so that the search is case-insensitive, so the `grep` command will match the pattern regardless of if the lines are uppercase or lowercase.*

Examples:
1.
```
  william@Williams-MacBook-Air-3 biomed % grep -i "adults" 1468-6708-3-1.txt
        Older adults are frequently counseled to lose weight,
        non-smoking older adults have investigated the association
        adults drew similar conclusions [ 7 ] .
        Many healthy older adults report gradual weight gain
        In older adults, risk factors may have a greater effect
        years of being healthy, in a cohort of older adults for
        modification interventions in older adults.
          population-based longitudinal study of 5,888 adults aged
          categories could be combined for older adults. Since
          interventions for older adults who were merely overweight
          adults are the subjects. This is particularly important
          33 34 ] . For older adults, the risks associated with
          outcome for a trial of weight loss in older adults
          found for underweight older adults. Clinical trials whose
        older adults, especially for women. Future efforts to
        no excess risk for older adults who would be classified as
        obese or underweight older adults, and discouraging trials
        that address older adults who are merely overweight.`
```
- The following command finds all the lines that have the pattern "adult" 
   
2. `grep -n` : The command line option `n` makes it so that the search will prefix the line of output with the 1-based line number of its input file

Examples:
- 
-

3. `grep -v` : The command line option `v` makes it so that the search will display lines that DO NOT follow the specified pattern.

Examples:
- 
-

4. `grep -x`: Command line option `x` makes it so that the search will displauy lines that only follow the exact entire pattern and not just a part of it.

Examples:
- 
-

- **Sources**
https://www.gnu.org/savannah-checkouts/gnu/grep/manual/grep.html#Command_002dline-Options


