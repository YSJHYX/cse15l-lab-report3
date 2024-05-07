# Lab Report 3

## Part 1 - Bugs

Bug in method `reversed()`: <br>

- ## Input inducing failure:
```
@Test
  public void testReversed() {
    int[] input2 = {0, 1, 2, 3};
    assertArrayEquals(new int[]{3, 2, 1, 0}, ArrayExamples.reversed(input2));
  }
```
- ## Input that does not induce failure:
```
@Test
  public void testReversed() {
    int[] input1 = { };
    assertArrayEquals(new int[]{ }, ArrayExamples.reversed(input1));
  }
```
- ## Symptom
