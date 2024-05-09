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
- `-c`: This prints only a count of the lines that match a pattern.

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

When I ran the command, it counted the occurrence of the word "report" in files under the directory `technical` and its subdirectories, and then it showed the output to the first 10 lines. This command is useful since it can quickly find out where specific keywords or phrases occur in multiple files within a director, it also counts the occurrence of the keywords in each file.

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

Running this command searches for the occurrences of the word "report" in files under the directory `technical` and its subdirectories. After counting the occurrences of each match, it sorts the results based on the 3rd field (the file path) using ":" as the field separator, in numerical order, and then shows the first 10 lines of the sorted output.

By using this command, we are able to effectively find the files where the word "report" occurs most frequently and display the top 10 files based on the count of occurrences.


- `-l`: Displays list of filenames only.

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

It searches for files that contain "report" under the `technical` directory and its subdirectories, it also displays the names of the first 10 files found. It is useful since it helps quickly identify files containing the specific keyword within their content under the current directory and its subdirectories.

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


- `-n`: Display the matched lines and their line numbers.

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

This command searches for the specific keyword "report" under the directory `technical` and its subdirectories, also, it shows the matching lines and the corresponding line numbers. This is useful since it can quickly identify where the specific keyword "report" appears in files and in what content.

```
harry@HarrydeMacBook-Pro technical % grep -c -r "successful" | sort -t ":" -k 2 -n | tail -n 1 | cut -d ":" -f 1 | xargs grep -n "successful"
199:successful outcomes. The first knowledge point occurs when the
222:probability of successful cost and schedule outcomes. Problems
257:control before committing to full production. The more successful
332:companies had more successful outcomes. For example, the AIM-9X and
418:DOD programs that had more successful outcomes used key best
430:On the other hand, DOD programs with less successful outcomes
460:facilitate better decisions and more successful acquisition program
535:process, specifically product development and ways to successfully
600:points 2 and 3, particularly at how successful companies design and
609:have successful cost and schedule outcomes. Programs that do not
673:that have led to more successful product development and production
682:practices that resulted in successful product development. We
706:turbines, derived from its successful jet engine programs, for
850:considered them to be in two basic categories-successful and
851:unsuccessful cost and schedule performance outcomes. This basis for
943:We found that the most successful programs had taken steps to
955:validated before committing to production. The most successful DOD
966:successful cases had captured. They increased investments in
1004:basis, we believe other factors contributed to a successful
1086:processes than more successful cases. For example, at its limited
1111:successful programs that the product can be manufactured within
1123:Leading commercial companies have been successful in achieving
1166:had relatively successful outcomes. The other DOD
1233:more successfully and cost-effectively develop new, but
1243:had relatively successful cost and schedule outcomes. They
1526:making the prototypes a key ingredient to successful outcomes.
1813:successful production outcome to date. Program officials took steps
2035:successful acquisition program outcomes. As demonstrated by
2036:successful companies, using these criteria can help ensure that the
2367:measure design stability and process controls. Third, successful
```

The command searches for the specific keyword "successful" within files under the `technical` directory and its subdirectories, counts the occurrences of this keyword in each file, sorts the filenames in numerical order, selects the last file, extracts its filename, and finally searches or the occurrences of the keyword within the specific file, also shows their line numbers. It is useful for identifying the file with the highest count of occurrences of the specific keyword "successful" and shows the occurrences of "successful" within that file, along with their line numbers.

- `-h`: Display the matched lines, but do not display the filenames.

```
harry@HarrydeMacBook-Pro technical % grep -h -r "Mark" | head -n 10
Mark Schacht, California Rural Legal Assistance Foundation)
Endriss, Attorney at Law); March Comments at 82 (comment of Mark
March Comments at 82 (comment of Mark Miller, American Friends
(comment of Mark Miller, American Friends Service Committee); March
Northwest Justice Project); March Comments at 76 (comment of Mark
Talamantes, Attorney at Law); March Comments at 83 (comment of Mark
Comments at 76-77 (comment of Mark Talamantes, Attorney at Law);
April testimony at 80; March Comments at 76 (comment of Mark
March Comments at 77 (comment of Mark Talamantes, Attorney at Law);
Attorney at Law); March Comments at 77 (comment of Mark Talamantes,
```

This command searches for the string "Mark" within files in the `technical` directory and its subdirectories, and it shows the matching lines without displaying the filenames. It is useful if we want to check the occurrences of a specific keyword, like "Mark", in multiple files.

```
harry@HarrydeMacBook-Pro technical % grep -h -r "China" | uniq -c
   1 Committee on United States-China Relations
   1 is the withdrawal of China as an importer of ammonia. China
   1 precipitously since China, formerly a major buyer, decided to
   1 strive for self-sufficiency. From 1994 to 1997, China opened nine
   1 U.S. producers knew China would bring on the new, more-efficient
   1 activities of the White House China Trade Relations Working Group,
   1 China, the World Trade Organization, and last year's presidential
   1         of rural poverty in the tropics, including southern China [5], the Indian subcontinent [6],
   1         populations living in hookworm-endemic regions of Brazil and China ([30]; J. Bethony, A.
   1         China, two introgressions from a wild relative of rice have been associated with a 30%
   1         mid-level Chinese government officials seeking promotions systematically enhanced China's
   1         The FAO data show that catches, excluding a recent surge in anchoveta and China's
   1         developing countries. For example, Latin America and China, although representing,
   1         species of tree in China and Australia, and on cotton in China and Greece, suggesting
   1         Himalayas, the Tibetan plateau, or Yunnan province in China. But these are big places, and
   1           from China and central Asia, is also placed outside of
   1           Filifolium occurs in China and
   1           Phillipines, Taiwan, southern Japan, and China, whereas 
   1           Siberia, Mongolia, and China [ 2 ] . It was segregated
   1           two species that occur in central Asia and China. They
   1         crop for oil and protein source. While China, USA and India
   1         postmenopausal women. Studies from China [ 7] and Japan [
   1         also been introduced into India from China and Japan,
   1         Kanva-2 (K2) and two exotic varieties China White (CW) and
   1           China White (CW), Kanwa2 (K2), Mandalay (MAN), S1531,
   1           Shanghai, China). Before use in experiments, MCF7/ADR
   1           Ltd, Shanghai, China) for 2 h at room temperature. The
   1         malignant diseases in China. Although the GC has been
   1         in northern China.
   1           China. No selection process was involved. Of the 60
   1                 he traveled to China, the Philippines, Pakistan, Bosnia (a second time), Brazil,
   1                     China-would be housed in whatever department or agency is best suited for them.
   1                 issues-among them, Haiti, Bosnia, Russia, China, Somalia, Kosovo, NATO enlargement,
   1                 Tucson, Arizona, in the late 1980s, went as far afield as China, Malaysia, the
   1                 state-of-the-art video cameras obtained from China and from dealers in Germany. The
   1                 priorities included China, missile defense, the collapse of the Middle East peace
   1                 Russia and China should be encouraged to participate.
   1                 that the attacks provided a great opportunity to engage Russia and China. Secretary
```

This command counts the occurrences of each unique line containing the specific keyword "China" across all files in the `technical` directory and its subdirectories. I think this is useful if we want to use the distribution and patterns of occurrences of the keyword "China" within our files to process data analysis.

Source: https://www.geeksforgeeks.org/grep-command-in-unixlinux/
