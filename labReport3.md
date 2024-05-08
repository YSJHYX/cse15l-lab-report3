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

   Test Fail Screenshot:

  ![Image](testFail.png)

   Test Pass Screenshot:

 ![Image](testPass.png)

- ## Bug <br>
Original code:

```
  static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = newArray[arr.length - i - 1];
    }
    return arr;
  }
```


  Code after changing:

```
  static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      newArray[i] = arr[arr.length - i - 1];
    }
    return newArray;
  }
```

In the previous code, we changed elements in the old array `arr` by assigning each element in `arr` with the data of elements in the new array `newArray`. So, we switched `arr` and `newArray` in line 4, and made this method return `newArray`. In this way, the bug was successfully fixed and both these two inputs can pass the test.

## Part 2 - Researching Commands: grep
- -c: This prints only a count of the lines that match a pattern.

```
harry@HarrydeMacBook-Pro technical % grep -c -r "report" | head -n 10
./government/About_LSC/LegalServCorp_v_VelazquezSyllabus.txt:0
./government/About_LSC/Progress_report.txt:17
./government/About_LSC/Strategic_report.txt:27
./government/About_LSC/Comments_on_semiannual.txt:14
./government/About_LSC/Special_report_to_congress.txt:60
./government/About_LSC/CONFIG_STANDARDS.txt:0
./government/About_LSC/commission_report.txt:22
./government/About_LSC/LegalServCorp_v_VelazquezDissent.txt:0
./government/About_LSC/ONTARIO_LEGAL_AID_SERIES.txt:3
./government/About_LSC/LegalServCorp_v_VelazquezOpinion.txt:0
```

When I ran the command, it counted the occurrence of the word "report" in files under the directory `technical`, and then it showed the output to the first 10 lines. This command is useful since it can quickly find out where specific keywords or phrases occur in multiple files within a director, it also counts the occurrence of the keywords in each file.

```
harry@HarrydeMacBook-Pro technical % grep -c -r "report" | sort -t ":" -k 3 -n | head -n 10
./911report/chapter-1.txt:56
./911report/chapter-10.txt:6
./911report/chapter-11.txt:17
./911report/chapter-12.txt:5
./911report/chapter-13.1.txt:21
./911report/chapter-13.2.txt:140
./911report/chapter-13.3.txt:226
./911report/chapter-13.4.txt:631
./911report/chapter-13.5.txt:325
./911report/chapter-2.txt:17
```

Running this command searches for the occurrences of the word "report" in files under the directory `technical`. After counting the occurrences of each match, it sorts the results based on the 3rd field (the file path) using ":" as the field separator, in numerical order, and then shows the first 10 lines of the sorted output.

By using this command, we are able to effectively find the files where the word "report" occurs most frequently and display the top 10 files based on the count of occurrences.


- -l: Displays list of filenames only.

```
harry@HarrydeMacBook-Pro technical % grep -l -r "report" | head -n 10
./government/About_LSC/Progress_report.txt
./government/About_LSC/Strategic_report.txt
./government/About_LSC/Comments_on_semiannual.txt
./government/About_LSC/Special_report_to_congress.txt
./government/About_LSC/commission_report.txt
./government/About_LSC/ONTARIO_LEGAL_AID_SERIES.txt
./government/About_LSC/diversity_priorities.txt
./government/About_LSC/reporting_system.txt
./government/About_LSC/State_Planning_Report.txt
./government/About_LSC/Protocol_Regarding_Access.txt
```

It searches for files that contain "report" under the `technical` directory and displays the names of the first 10 files found. It is useful since it helps quickly identify files containing the specific keyword within their content under the current directory.

```
harry@HarrydeMacBook-Pro technical % grep -l -r "report" | xargs grep -c "report" | sort -t ":" -k 2 -n | head -n 10
./biomed/1471-2091-2-7.txt:1
./biomed/1471-2091-3-15.txt:1
./biomed/1471-2091-3-22.txt:1
./biomed/1471-2091-3-8.txt:1
./biomed/1471-2091-4-1.txt:1
./biomed/1471-2105-1-1.txt:1
./biomed/1471-2105-2-1.txt:1
./biomed/1471-2105-3-12.txt:1
./biomed/1471-2105-3-16.txt:1
./biomed/1471-2105-3-2.txt:1
```

This is a complex command since it uses `|` to combine four commands to achieve the goal of finding the top 10 files with the most occurrences of the specific keyword "report". It is useful since it helps identify files where the specific keyword "report" appears most frequently, which allows users to prioritize these files further.


- -n: Display the matched lines and their line numbers.

```
harry@HarrydeMacBook-Pro technical % grep -n -r "report" | head -n 10
./government/About_LSC/Progress_report.txt:9:I am pleased to submit to you our report concerning the progress
./government/About_LSC/Progress_report.txt:11:Planning Team with some statistical and reporting assistance from
./government/About_LSC/Progress_report.txt:14:I would like to put this report in its proper perspective. We
./government/About_LSC/Progress_report.txt:36:news, however, can be found in reports like this one. Reports that
./government/About_LSC/Progress_report.txt:56:This report demonstrates that our grantees and the broader equal
./government/About_LSC/Progress_report.txt:71:report that would be gathering dust on a shelf down in our
./government/About_LSC/Progress_report.txt:73:I think this report shows that we have had an inordinately
./government/About_LSC/Progress_report.txt:378:Grant conditions, riders, or reporting requirements are being
./government/About_LSC/Progress_report.txt:382:calling on each state to evaluate and report on their state
./government/About_LSC/Progress_report.txt:623:training, evaluations, periodic reports, staffing on-going support,
```
