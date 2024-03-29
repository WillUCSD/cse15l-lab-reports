# Lab Report 3
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
**How the fix adresses the issue**

The initial code fails as the same array is used for the source and destination. As such, when you are overwriting the original values of the array, these same values are then used again to overwrite the later values. In the end, the values of array are not properly reversed. This is fixed in the "After" code by adding `temp` to act as a temporary array for the destination. The original array is then changed to become equal to `temp` afterwards which is the properyly reversed version.

## Part 2 - Researching Commands 
**`grep` command-line options**

1. `grep -i `: The command line option `-i` makes it so that the search is case-insensitive, so the `grep` command will match the pattern regardless of if the lines are uppercase or lowercase.

Examples:

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

The following command displays all the lines that have the pattern "adults" inside it regardless if "adults" is capitalized at all. This can useful to indentfy portions of the text in which capitalization is not an issue or delineating factor. 

```
william@Williams-MacBook-Air-3 biomed % grep -i "overweight" 1468-6708-3-1.txt
        even though there is little evidence that overweight is
          BMI of 18.5 to 24.9; overweight as 25 to 29.9; and
        classified as normal, overweight or obese all had about the
        women and men. Women who were normal or overweight averaged
        women than for men in the normal and overweight groups, but
        underweight category. The effect size comparing overweight
        overweight (for men or women) or obese (for men) affects
          Optimal weight and overweight
          overweight (as opposed to the obese) are no different
          interventions for older adults who were merely overweight
          differences between the overweight and normal weight
        'overweight' by the NHLBI guidelines. This suggests using
        that address older adults who are merely overweight.
```
The following command displays all the lines that have the pattern "overweight" inside it regardless if "overweight" is capitalized at all. This can useful to indentfy portions of the text in which capitalization is not an issue or delineating factor. 
___

2. `grep -n` : The command line option `n` makes it so that the search will prefix the line of output with the 1-based line number of its input file

Examples:
```
william@Williams-MacBook-Air-3 biomed % grep -n "adults" 1468-6708-3-1.txt   
6:        Older adults are frequently counseled to lose weight,
10:        non-smoking older adults have investigated the association
16:        adults drew similar conclusions [ 7 ] .
17:        Many healthy older adults report gradual weight gain
27:        In older adults, risk factors may have a greater effect
36:        years of being healthy, in a cohort of older adults for
42:        modification interventions in older adults.
50:          population-based longitudinal study of 5,888 adults aged
324:          categories could be combined for older adults. Since
338:          interventions for older adults who were merely overweight
347:          adults are the subjects. This is particularly important
350:          33 34 ] . For older adults, the risks associated with
352:          outcome for a trial of weight loss in older adults
356:          found for underweight older adults. Clinical trials whose
406:        older adults, especially for women. Future efforts to
409:        no excess risk for older adults who would be classified as
412:        obese or underweight older adults, and discouraging trials
413:        that address older adults who are merely overweight.
```

The following command displays all the lines that have the pattern "adults" as well as prefixing the line of out put with the line number of its input file. This can be useful in identifying specific portion of the txt file that have that pattern.
  
```
william@Williams-MacBook-Air-3 biomed % grep -n "overweight" 1468-6708-3-1.txt
7:        even though there is little evidence that overweight is
70:          BMI of 18.5 to 24.9; overweight as 25 to 29.9; and
259:        classified as normal, overweight or obese all had about the
262:        women and men. Women who were normal or overweight averaged
268:        women than for men in the normal and overweight groups, but
291:        underweight category. The effect size comparing overweight
303:        overweight (for men or women) or obese (for men) affects
315:          Optimal weight and overweight
322:          overweight (as opposed to the obese) are no different
338:          interventions for older adults who were merely overweight
394:          differences between the overweight and normal weight
410:        'overweight' by the NHLBI guidelines. This suggests using
413:        that address older adults who are merely overweight.
```

The following command displays all the lines that have the pattern "overweight" as well as prefixing the line of out put with the line number of its input file. This can be useful in identifying specific portion of the txt file that have that pattern.

___

3. `grep -v` : The command line option `v` makes it so that the search will display lines that DO NOT follow the specified pattern.

Examples:

```
william@Williams-MacBook-Air-3 biomed % grep -v "adults" 1468-6708-3-1.txt   
      
        Introduction
        even though there is little evidence that overweight is
        associated with increased mortality in those over age 65.
        Six large controlled population-based studies of
        between body mass index (BMI) and mortality, controlling
        for relevant covariates [ 1 2 3 4 5 6 ] . All studies found
        excess risk for persons with very low BMI, but that persons
        with moderately high BMI had little or no extra risk except
        in certain small subsets. A review of 13 studies of older
        throughout adult life. It may be that a small amount of
        gradual weight gain is normative and associated with the
        most robust health as we age. It has been suggested that
        weight standards be adjusted upwards for age [ 8 ] . Such
        recommendations remain controversial, however, because the
        number of studies of older persons is fairly small, and
        because few studies have examined the relation of BMI to
        quality of life or years of healthy life (YHL) in the
        elderly [ 9 ] .
        on health than on mortality. If so, then behavior change
        trials of weight modification might be more successful if
        they were evaluated on improved health, rather than on
        decreased mortality. Clinical trials powered to detect
        differences in YHL would often require fewer subjects than
        trials to detect survival differences or cardiovascular
        events [ 10 ] . In this paper we study whether BMI at
        baseline is associated with living longer, and/or with more
        whom risk factors, subclinical disease, and morbidity are
        well characterized. The goal is to determine whether
        analyses based on years of life (YOL) or on YHL would
        provide substantively different results, and which measure
        would yield more powerful evaluations of weight
      
      
        Materials and methods
        
          Study design: The Cardiovascular Health
          Study
          The Cardiovascular Health Study (CHS) is a
          65 and older at baseline [ 11 ] . Subjects were recruited
          from a random sample of the Medicare eligibility lists in
          four US counties. Extensive baseline data were collected
          for all subjects using a baseline home interview, an
          annual mail questionnaire, and annual clinic
          examinations. Additional information was collected in a
          brief telephone interview 6 months after each scheduled
          visit. Two cohorts were followed, one with 7 years of
          follow-up (n = 5,201) and the second (all African
          American, n = 687) with 4 years of follow-up to date.
          Data collection began in 1989, and follow-up is virtually
          complete for all surviving subjects [ 12 ] .
        
        
          Body mass index
          BMI was calculated as measured weight in kilograms
          divided by the square of measured height in meters. A
          report from the National Heart Lung and Blood Institute
          classifies normal weight (without reference to age) as a
          BMI of 18.5 to 24.9; overweight as 25 to 29.9; and
          obesity as 30.0 and higher [ 13 ] . We consider
          separately the group with BMI between 18.5 and 20, which
          was associated with lower survival in studies cited
          above.
        
        
          Years of life and years of healthy life
          YOL is the number of years that a person lived in the
          7 years after baseline. YHL is the number of years in
          which the person was 'healthy', and is similar in concept
          to quality-adjusted life-years, healthy year equivalents,
          or active life expectancy [ 14 ] . We based YHL on
          self-rated health (is your health excellent, very good,
          good, fair, or poor?) (EVGFP) which was collected every 6
          months. EVGFP is a simple but well-known measure, which
          has been studied in detail [ 15 16 ] , and is predictive
          of health events in many studies [ 17 ] . Because we are
          examining health status over time, we added a sixth
          health state, dead. Data were available about 93% of the
          time. We used linear interpolation to estimate missing
          data when there were known values before and after the
          missing value, bringing the percent complete to 95% [ 18
          ] .
          For this analysis we defined YHL as the number of
          years (of 7) in which a person reported excellent, very
          good, or good health (were 'healthy'). YHL ranges from 0
          (for persons who were never in excellent, very good, or
          good health) to 7 years (for persons who were healthy
          throughout). Since people reported their health every 6
          months, YHL has a reasonably continuous distribution. A
          drawback of this simple definition of 'healthy' is that
          it does not distinguish between fair or poor health and
          death, since all are considered 'not healthy'. We also
          used an alternative approach, which assigns a different
          value to each level of EVGFP [ 19 ] . Preliminary results
          were similar for the two approaches, however, and we
          report results using only the simpler definition.
          The calculations had to be modified to include the 438
          persons in the second African American cohort, who have
          been followed only 4 years to date. For those persons,
          and for 70 persons in the first cohort who did not have
          complete data, we estimated the last 4 years of YOL and
          YHL from their age, sex, and health at the end of 3
          years, using validated methods presented elsewhere [ 20 ]
          . That article showed that estimated 4-year YOL and YHL
          were unbiased for the African American cohort. In the
          primary analysis we used observed 7-year YOL and YHL when
          they were available, and observed 3-year YOL and YHL plus
          4-year estimated YOL and YHL when they were not (about
          10% of the sample). We performed all analyses with and
          without the persons who had partially estimated data, to
          ensure that the estimation had not distorted the
          findings.
        
        
          Covariates
          The goal is to examine the association of YOL and YHL
          with BMI. To adjust for possible confounding we chose
          baseline covariates that were prevalent in the elderly,
          related to mortality and morbidity in previous studies,
          and likely to be related to BMI. Self-reported covariates
          include age, gender, smoking (never or former), history
          of arthritis, cancer, diabetes, fair or poor self-rated
          health status, limitations in activities of daily living
          or in instrumental activities of daily living, and 10
          pounds or more unintended weight loss in the year before
          baseline. Clinical covariates include hypertension,
          cardiovascular disease (prevalent heart disease,
          peripheral vascular disease, or cerebrovascular disease),
          maximum thickness of the internal carotid artery,
          depression (CESD score), serum albumin, serum
          cholesterol, and serum creatinine. These measures are
          explained in more detail elsewhere [ 21 22 23 24 ] . We
          excluded 697 current smokers and 313 others with
          incomplete covariate data, leaving 4,878 persons on whom
          this analysis is based.
        
        
          Analysis
          All analyses were performed separately for men and
          women. We calculated two sets of adjusted values, as
          follows. We regressed YOL and YHL first on age, age
          squared, race, and smoking history (former or never), and
          second on all of the covariates listed above. We
          calculated adjusted YOL as a person's observed YOL minus
          predicted YOL (from the regression) plus the mean YOL
          (6.52 years for women or 6.06 for men). That is, a
          person's adjusted YOL is his residual from the regression
          plus the grand mean. The mean of this new variable, for a
          group of subjects, is the adjusted mean YOL for that
          group. Adjusted YHL was calculated in a similar manner.
          We calculated two sets of adjusted variables because of
          the possibility of 'over-adjustment', controlling
          inappropriately for factors (such as diabetes) which may
          have been causally affected by the person's weight. We
          plotted mean adjusted YOL and YHL against BMI, and tested
          for difference among BMI groups using confidence
          intervals or analysis of variance. Finally we calculated
          the effect size for each measure, comparing each BMI
          subgroup to the 'normal' group. The effect size is the
          difference in mean YOL (or YHL) in two groups divided by
          their common standard deviation. Since the sample size
          required to detect an effect of this magnitude is
          proportional to the inverse of the squared effect size,
          large effect sizes are desirable.
        
      
      
        Results
        Table 1shows the distribution of key variables by sex
        and race. Mean age at baseline was 73.1 and about two
        thirds of the men and a third of the women were former
        smokers. Black women had a higher mean BMI and higher
        percent obese (BMI ≥ 30) than the other three groups. Black
        men were most likely to have unintentionally lost more than
        10 pounds in the past year; white women were least
        likely.
        About 78% of the subjects were healthy at baseline,
        declining to 57% at the end of 7 years; 20% had died (data
        not shown). Of the 22% who were unhealthy (fair or poor) at
        baseline, about 24% were healthy 7 years later. There was
        thus substantial change in EVGFP over time, in both
        directions. Table 1shows the mean YOL and YHL (calculated
        from EVGFP) in the first seven years of the study, adjusted
        to age 73. For example, black women averaged 6.3 YOL, but
        only 4.2 YHL of a maximum possible 7. We calculated some
        additional descriptive statistics, shown in the final two
        lines: years of unhealthy life (YOL minus YHL) and years
        lost to death (7 minus YOL). White women had the most YHL
        and black men the fewest; black women had the most years of
        unhealthy life, and white men the fewest; black men lost
        the most years to death (1.3 out of 7) while white women
        lost only 0.4 years. For blacks, about 68% of their YOL
        were healthy (YHL/YOL, not shown); for whites, about 75%
        were healthy.
        Among whites, the gender differences in Table 1were
        statistically significant (p <.05) except for BMI and
        unintended weight loss. Among blacks, gender differences
        were significant except for 10 pounds unintended weight
        loss and weight loss since age 50. Among males, there were
        significant differences between black and white for BMI,
        unintended weight loss, YOL, YHL, years of unhealthy life,
        and years lost to death. Whites in the sample had higher
        income and education (data not shown). After adjusting for
        income and education, as well as age and former smoking,
        the difference in BMI was no longer statistically
        significant. Among females, blacks and whites differed
        significantly on BMI, BMI>30, weight loss since age 50,
        YOL, YHL, years of unhealthy life, and years lost to death.
        After adjustment for income and education, the difference
        in weight loss since age 50 was no longer significant.
        Blacks had significantly lower YOL and YHL than whites
        after adjustment for age, but the difference disappeared
        after adjustment for the entire set of health-related
        baseline covariates (analyses not shown).
        We next examined the relationship of BMI to YOL and YHL.
        Table 2presents the mean values of YOL and YHL, adjusted
        for age, race, and previous smoking (columns 1 and 3), and
        also adjusted for the entire set of covariates (columns 2
        and 4). For example, YOL for women, adjusted for age, race,
        and smoking, averaged 6.0 years for women with a baseline
        BMI below 18.5, but averaged 6.6 years for women with a BMI
        from 25 to 29.9. The second column, which shows results
        adjusted for all covariates, is not very different (the
        only discrepancy is for men with BMI < 18.5, a category
        containing only 14 men). Adjustment for extensive
        covariates also made little difference for YHL (columns 3
        and 4). Subsequent analyses are adjusted only for age,
        race, and former smoking. As mentioned above, the group
        with BMI from 18.5 to 20 would be considered 'normal' by
        the NHLBI guidelines, but had lower YOL and YHL than those
        with 20-24.9 in all comparisons. For this reason, and to
        increase sample size for those with low BMI, we combined
        the two lower categories, defining underweight as a BMI
        under 20.
        Figure 1is a plot of adjusted YOL and YHL by sex and
        BMI. For each BMI category the mean and its 95% confidence
        interval are plotted. Categories whose confidence intervals
        do not overlap, or overlap only slightly, are significantly
        different. The bars are slightly offset to permit all error
        bars to be seen.
        YOL for women (the uppermost curve on Figure 1) averaged
        about 6.5 out of 7 years, and showed no evident association
        between BMI and YOL for BMI above 20. Underweight women
        averaged about .25 fewer YOL than other women (p < .05
        compared with normal group). Underweight men also had lower
        YOL, but this group was not significantly different from
        the normal group, in part because of low sample size. Men
        classified as normal, overweight or obese all had about the
        same YOL.
        The lowermost two lines in Figure 1show mean YHL for
        women and men. Women who were normal or overweight averaged
        about 4.9 YHL. The YHL for underweight or obese women was
        about 4.5 years, which was significantly lower than the
        normal group. The relationship of BMI to YHL for men is
        similar, but differences among BMI groups were not
        statistically significant. YHL was significantly higher for
        women than for men in the normal and overweight groups, but
        the sexes had similar YHL in the underweight and obese
        groups.
        We next present the effect size for comparing each group
        to the normal BMI group. The effect sizes are shown in
        Table 3, with the significance results of the associated
        t-tests for the differences in means of the two groups
        being compared. For example, underweight women averaged
        4.50 YHL compared to 4.92 for normal women, and the common
        standard deviation was 1.44. The effect size is thus
        (4.92-4.50)/1.44 = .29. The two groups had significantly
        different YHL, implying that the effect size is also
        significantly greater than zero. A clinical trial of a
        treatment to help underweight women achieve normal weight
        (presumably by addressing the underlying cause) could be
        expected to have 80% power with N = (1.96+.84) 2/.29 2=
        about 93 women per treatment arm, if 7-year YHL were the
        outcome measure.
        The biggest effect sizes are in the first row, comparing
        underweight to normal. YHL and YOL have similar effect
        sizes for women, and are significantly different from zero.
        The effect sizes are not significantly different from zero
        for men, in part because there were only 42 men in the
        underweight category. The effect size comparing overweight
        to normal yielded small, non-significant effect sizes, with
        inconsistent signs, suggesting extremely large sample sizes
        would be needed. For comparing obese to normal, only YHL
        for women showed a large and significant effect size. Thus,
        an intervention to improve the health of underweight women
        to that of their normal weight peers could be performed
        using either YHL or YOL as the outcome variable. Trials to
        make obese women comparable to normal women could be
        evaluated using YHL, but not YOL. Trials to improve the
        health of the other groups to that of the normals would
        probably be fruitless since there is no evidence that being
        overweight (for men or women) or obese (for men) affects
        YOL or YHL.
        As mentioned above, we repeated these analyses excluding
        the persons with partially estimated data, and using two
        different ways of coding YHL. The only substantive change
        was that some of the differences between blacks and whites
        shown in Table 1were no longer statistically significant,
        due to a smaller sample size.
      
      
        Discussion
        
          Optimal weight and overweight
          Recent studies have defined obesity without reference
          to age [ 6 13 30 ] . Andres 
          et al proposed a desirable BMI of
          24-30 for persons aged 60 to 69 [ 8 ] . Allison 
          et al [ 31 ] proposed 27-30 for
          older men and 30-35 for older women. In Figure 1, the
          overweight (as opposed to the obese) are no different
          from those of normal weight, suggesting that these two
          future improvements in life expectancy may be limited [
          32 ] , the greatest advances may be made by improving
          people's YHL. This suggests that the development of
          future guidelines should take YHL or other measures of
          quality of life into account.
        
        
          Implications for clinical trials
          Based on these findings, trials to address obesity in
          older women could be efficient if YHL (but not YOL) was
          the outcome measure. That is, women who changed from
          being obese to being normal would likely show changes in
          YHL, but not YOL. Clinical trials of weight modification
          would appear to be fruitless since the interventions
          would probably not have a direct effect on either YOL or
          YHL.
          Weight or weight change are sometimes used as the
          outcome in evaluations of interventions such as diet or
          exercise programs. The fact that weight is not associated
          in a consistent way with health suggests that such
          evaluations should be considered critically when older
          in the light of recent findings, which found that
          interventions such as weight-loss drugs may be harmful [
          higher weight are especially unclear, and the optimal
          requires specific attention to improved health and
          mortality.
          Interestingly, the strongest health relationships were
          objective was to make the underweight as healthy as their
          normal-weight peers (presumably by addressing the
          underlying conditions that caused the low weight) could
          be performed efficiently using either YOL or YHL as the
          outcome measure. Both YOL and YHL would be clinically
          significant in this patient group.
        
        
          Potential limitations
          CHS participants were somewhat healthier than the
          average older adult; however, adjustment for detailed
          covariates made little difference in the findings. We
          estimated the last four years of health data for about
          10% of the sample, but results with and without this
          group were similar. Analysis of mean YOL instead of the
          more traditional survival analysis survival analysis was
          appropriate here, since virtually no persons were lost to
          follow-up. Biases caused by over-adjustment are probably
          not large, since the findings were not sensitive to the
          number of variables adjusted for.
          These results are for a 7-year follow-up. The relative
          superiority of YHL to YOL would probably hold in trials
          with shorter follow-up. The effect sizes in Table 3might
          also be appropriate in shorter trials, since lengthy
          trials often add little information [ 10 ] .
          EVGFP, on which YHL was based, might have missed some
          effects of obesity on risk factors for future health. A
          person who is depressed because of a poor self-image
          related to obesity or who has osteo-arthritis related to
          obesity and limits to activities to successfully avoid
          pain would surely have worse EVGFP than others, based on
          results from many studies. However, health measures
          designed specifically to measure those conditions might
          be more sensitive to change in weight than EVGFP. If YHL
          were based on such measures, the superiority of YHL to
          YOL would likely be even greater than that shown here.
          These more sensitive measures might also have detected
          differences between the overweight and normal weight
          persons, but we think this is unlikely given the absence
          of any differences in EVGFP.
        
      
      
        Conclusion
        Recommendations for desirable weight have been
        criticized for emphasizing mortality rather than health. We
        found associations between YHL and obesity that were not
        present in the mortality analysis, suggesting that YHL may
        be a more sensitive measure of the burden of obesity in
        determine desirable weight guidelines should include
        measures of YHL. Using either YOL or YHL, however, we found
        'overweight' by the NHLBI guidelines. This suggests using
        YHL as the outcome measure in clinical trials involving
      
      
        Competing interests
        None declared
      
      
        Abbreviations
        BMI Body mass index
        CESD Center for Epidemiologic Studies Depression
        Scale
        CHS Cardiovascular Health Study
        EVGFP Is your health excellent, very good, good, fair or
        poor?
        QALY Quality-adjusted life years
        YHL Years of healthy life
        YOL Years of life
```

The following command displays all the lines that do not have the pattern "adults". This can be useful in narrowing down certain lines that you want to look at.

```
william@Williams-MacBook-Air-3 biomed % grep -v  "overweight" 1468-6708-3-1.txt

  
    
      
        Introduction
        Older adults are frequently counseled to lose weight,
        associated with increased mortality in those over age 65.
        Six large controlled population-based studies of
        non-smoking older adults have investigated the association
        between body mass index (BMI) and mortality, controlling
        for relevant covariates [ 1 2 3 4 5 6 ] . All studies found
        excess risk for persons with very low BMI, but that persons
        with moderately high BMI had little or no extra risk except
        in certain small subsets. A review of 13 studies of older
        adults drew similar conclusions [ 7 ] .
        Many healthy older adults report gradual weight gain
        throughout adult life. It may be that a small amount of
        gradual weight gain is normative and associated with the
        most robust health as we age. It has been suggested that
        weight standards be adjusted upwards for age [ 8 ] . Such
        recommendations remain controversial, however, because the
        number of studies of older persons is fairly small, and
        because few studies have examined the relation of BMI to
        quality of life or years of healthy life (YHL) in the
        elderly [ 9 ] .
        In older adults, risk factors may have a greater effect
        on health than on mortality. If so, then behavior change
        trials of weight modification might be more successful if
        they were evaluated on improved health, rather than on
        decreased mortality. Clinical trials powered to detect
        differences in YHL would often require fewer subjects than
        trials to detect survival differences or cardiovascular
        events [ 10 ] . In this paper we study whether BMI at
        baseline is associated with living longer, and/or with more
        years of being healthy, in a cohort of older adults for
        whom risk factors, subclinical disease, and morbidity are
        well characterized. The goal is to determine whether
        analyses based on years of life (YOL) or on YHL would
        provide substantively different results, and which measure
        would yield more powerful evaluations of weight
        modification interventions in older adults.
      
      
        Materials and methods
        
          Study design: The Cardiovascular Health
          Study
          The Cardiovascular Health Study (CHS) is a
          population-based longitudinal study of 5,888 adults aged
          65 and older at baseline [ 11 ] . Subjects were recruited
          from a random sample of the Medicare eligibility lists in
          four US counties. Extensive baseline data were collected
          for all subjects using a baseline home interview, an
          annual mail questionnaire, and annual clinic
          examinations. Additional information was collected in a
          brief telephone interview 6 months after each scheduled
          visit. Two cohorts were followed, one with 7 years of
          follow-up (n = 5,201) and the second (all African
          American, n = 687) with 4 years of follow-up to date.
          Data collection began in 1989, and follow-up is virtually
          complete for all surviving subjects [ 12 ] .
        
        
          Body mass index
          BMI was calculated as measured weight in kilograms
          divided by the square of measured height in meters. A
          report from the National Heart Lung and Blood Institute
          classifies normal weight (without reference to age) as a
          obesity as 30.0 and higher [ 13 ] . We consider
          separately the group with BMI between 18.5 and 20, which
          was associated with lower survival in studies cited
          above.
        
        
          Years of life and years of healthy life
          YOL is the number of years that a person lived in the
          7 years after baseline. YHL is the number of years in
          which the person was 'healthy', and is similar in concept
          to quality-adjusted life-years, healthy year equivalents,
          or active life expectancy [ 14 ] . We based YHL on
          self-rated health (is your health excellent, very good,
          good, fair, or poor?) (EVGFP) which was collected every 6
          months. EVGFP is a simple but well-known measure, which
          has been studied in detail [ 15 16 ] , and is predictive
          of health events in many studies [ 17 ] . Because we are
          examining health status over time, we added a sixth
          health state, dead. Data were available about 93% of the
          time. We used linear interpolation to estimate missing
          data when there were known values before and after the
          missing value, bringing the percent complete to 95% [ 18
          ] .
          For this analysis we defined YHL as the number of
          years (of 7) in which a person reported excellent, very
          good, or good health (were 'healthy'). YHL ranges from 0
          (for persons who were never in excellent, very good, or
          good health) to 7 years (for persons who were healthy
          throughout). Since people reported their health every 6
          months, YHL has a reasonably continuous distribution. A
          drawback of this simple definition of 'healthy' is that
          it does not distinguish between fair or poor health and
          death, since all are considered 'not healthy'. We also
          used an alternative approach, which assigns a different
          value to each level of EVGFP [ 19 ] . Preliminary results
          were similar for the two approaches, however, and we
          report results using only the simpler definition.
          The calculations had to be modified to include the 438
          persons in the second African American cohort, who have
          been followed only 4 years to date. For those persons,
          and for 70 persons in the first cohort who did not have
          complete data, we estimated the last 4 years of YOL and
          YHL from their age, sex, and health at the end of 3
          years, using validated methods presented elsewhere [ 20 ]
          . That article showed that estimated 4-year YOL and YHL
          were unbiased for the African American cohort. In the
          primary analysis we used observed 7-year YOL and YHL when
          they were available, and observed 3-year YOL and YHL plus
          4-year estimated YOL and YHL when they were not (about
          10% of the sample). We performed all analyses with and
          without the persons who had partially estimated data, to
          ensure that the estimation had not distorted the
          findings.
        
        
          Covariates
          The goal is to examine the association of YOL and YHL
          with BMI. To adjust for possible confounding we chose
          baseline covariates that were prevalent in the elderly,
          related to mortality and morbidity in previous studies,
          and likely to be related to BMI. Self-reported covariates
          include age, gender, smoking (never or former), history
          of arthritis, cancer, diabetes, fair or poor self-rated
          health status, limitations in activities of daily living
          or in instrumental activities of daily living, and 10
          pounds or more unintended weight loss in the year before
          baseline. Clinical covariates include hypertension,
          cardiovascular disease (prevalent heart disease,
          peripheral vascular disease, or cerebrovascular disease),
          maximum thickness of the internal carotid artery,
          depression (CESD score), serum albumin, serum
          cholesterol, and serum creatinine. These measures are
          explained in more detail elsewhere [ 21 22 23 24 ] . We
          excluded 697 current smokers and 313 others with
          incomplete covariate data, leaving 4,878 persons on whom
          this analysis is based.
        
        
          Analysis
          All analyses were performed separately for men and
          women. We calculated two sets of adjusted values, as
          follows. We regressed YOL and YHL first on age, age
          squared, race, and smoking history (former or never), and
          second on all of the covariates listed above. We
          calculated adjusted YOL as a person's observed YOL minus
          predicted YOL (from the regression) plus the mean YOL
          (6.52 years for women or 6.06 for men). That is, a
          person's adjusted YOL is his residual from the regression
          plus the grand mean. The mean of this new variable, for a
          group of subjects, is the adjusted mean YOL for that
          group. Adjusted YHL was calculated in a similar manner.
          We calculated two sets of adjusted variables because of
          the possibility of 'over-adjustment', controlling
          inappropriately for factors (such as diabetes) which may
          have been causally affected by the person's weight. We
          plotted mean adjusted YOL and YHL against BMI, and tested
          for difference among BMI groups using confidence
          intervals or analysis of variance. Finally we calculated
          the effect size for each measure, comparing each BMI
          subgroup to the 'normal' group. The effect size is the
          difference in mean YOL (or YHL) in two groups divided by
          their common standard deviation. Since the sample size
          required to detect an effect of this magnitude is
          proportional to the inverse of the squared effect size,
          large effect sizes are desirable.
        
      
      
        Results
        Table 1shows the distribution of key variables by sex
        and race. Mean age at baseline was 73.1 and about two
        thirds of the men and a third of the women were former
        smokers. Black women had a higher mean BMI and higher
        percent obese (BMI ≥ 30) than the other three groups. Black
        men were most likely to have unintentionally lost more than
        10 pounds in the past year; white women were least
        likely.
        About 78% of the subjects were healthy at baseline,
        declining to 57% at the end of 7 years; 20% had died (data
        not shown). Of the 22% who were unhealthy (fair or poor) at
        baseline, about 24% were healthy 7 years later. There was
        thus substantial change in EVGFP over time, in both
        directions. Table 1shows the mean YOL and YHL (calculated
        from EVGFP) in the first seven years of the study, adjusted
        to age 73. For example, black women averaged 6.3 YOL, but
        only 4.2 YHL of a maximum possible 7. We calculated some
        additional descriptive statistics, shown in the final two
        lines: years of unhealthy life (YOL minus YHL) and years
        lost to death (7 minus YOL). White women had the most YHL
        and black men the fewest; black women had the most years of
        unhealthy life, and white men the fewest; black men lost
        the most years to death (1.3 out of 7) while white women
        lost only 0.4 years. For blacks, about 68% of their YOL
        were healthy (YHL/YOL, not shown); for whites, about 75%
        were healthy.
        Among whites, the gender differences in Table 1were
        statistically significant (p <.05) except for BMI and
        unintended weight loss. Among blacks, gender differences
        were significant except for 10 pounds unintended weight
        loss and weight loss since age 50. Among males, there were
        significant differences between black and white for BMI,
        unintended weight loss, YOL, YHL, years of unhealthy life,
        and years lost to death. Whites in the sample had higher
        income and education (data not shown). After adjusting for
        income and education, as well as age and former smoking,
        the difference in BMI was no longer statistically
        significant. Among females, blacks and whites differed
        significantly on BMI, BMI>30, weight loss since age 50,
        YOL, YHL, years of unhealthy life, and years lost to death.
        After adjustment for income and education, the difference
        in weight loss since age 50 was no longer significant.
        Blacks had significantly lower YOL and YHL than whites
        after adjustment for age, but the difference disappeared
        after adjustment for the entire set of health-related
        baseline covariates (analyses not shown).
        We next examined the relationship of BMI to YOL and YHL.
        Table 2presents the mean values of YOL and YHL, adjusted
        for age, race, and previous smoking (columns 1 and 3), and
        also adjusted for the entire set of covariates (columns 2
        and 4). For example, YOL for women, adjusted for age, race,
        and smoking, averaged 6.0 years for women with a baseline
        BMI below 18.5, but averaged 6.6 years for women with a BMI
        from 25 to 29.9. The second column, which shows results
        adjusted for all covariates, is not very different (the
        only discrepancy is for men with BMI < 18.5, a category
        containing only 14 men). Adjustment for extensive
        covariates also made little difference for YHL (columns 3
        and 4). Subsequent analyses are adjusted only for age,
        race, and former smoking. As mentioned above, the group
        with BMI from 18.5 to 20 would be considered 'normal' by
        the NHLBI guidelines, but had lower YOL and YHL than those
        with 20-24.9 in all comparisons. For this reason, and to
        increase sample size for those with low BMI, we combined
        the two lower categories, defining underweight as a BMI
        under 20.
        Figure 1is a plot of adjusted YOL and YHL by sex and
        BMI. For each BMI category the mean and its 95% confidence
        interval are plotted. Categories whose confidence intervals
        do not overlap, or overlap only slightly, are significantly
        different. The bars are slightly offset to permit all error
        bars to be seen.
        YOL for women (the uppermost curve on Figure 1) averaged
        about 6.5 out of 7 years, and showed no evident association
        between BMI and YOL for BMI above 20. Underweight women
        averaged about .25 fewer YOL than other women (p < .05
        compared with normal group). Underweight men also had lower
        YOL, but this group was not significantly different from
        the normal group, in part because of low sample size. Men
        same YOL.
        The lowermost two lines in Figure 1show mean YHL for
        about 4.9 YHL. The YHL for underweight or obese women was
        about 4.5 years, which was significantly lower than the
        normal group. The relationship of BMI to YHL for men is
        similar, but differences among BMI groups were not
        statistically significant. YHL was significantly higher for
        the sexes had similar YHL in the underweight and obese
        groups.
        We next present the effect size for comparing each group
        to the normal BMI group. The effect sizes are shown in
        Table 3, with the significance results of the associated
        t-tests for the differences in means of the two groups
        being compared. For example, underweight women averaged
        4.50 YHL compared to 4.92 for normal women, and the common
        standard deviation was 1.44. The effect size is thus
        (4.92-4.50)/1.44 = .29. The two groups had significantly
        different YHL, implying that the effect size is also
        significantly greater than zero. A clinical trial of a
        treatment to help underweight women achieve normal weight
        (presumably by addressing the underlying cause) could be
        expected to have 80% power with N = (1.96+.84) 2/.29 2=
        about 93 women per treatment arm, if 7-year YHL were the
        outcome measure.
        The biggest effect sizes are in the first row, comparing
        underweight to normal. YHL and YOL have similar effect
        sizes for women, and are significantly different from zero.
        The effect sizes are not significantly different from zero
        for men, in part because there were only 42 men in the
        to normal yielded small, non-significant effect sizes, with
        inconsistent signs, suggesting extremely large sample sizes
        would be needed. For comparing obese to normal, only YHL
        for women showed a large and significant effect size. Thus,
        an intervention to improve the health of underweight women
        to that of their normal weight peers could be performed
        using either YHL or YOL as the outcome variable. Trials to
        make obese women comparable to normal women could be
        evaluated using YHL, but not YOL. Trials to improve the
        health of the other groups to that of the normals would
        probably be fruitless since there is no evidence that being
        YOL or YHL.
        As mentioned above, we repeated these analyses excluding
        the persons with partially estimated data, and using two
        different ways of coding YHL. The only substantive change
        was that some of the differences between blacks and whites
        shown in Table 1were no longer statistically significant,
        due to a smaller sample size.
      
      
        Discussion
        
          Recent studies have defined obesity without reference
          to age [ 6 13 30 ] . Andres 
          et al proposed a desirable BMI of
          24-30 for persons aged 60 to 69 [ 8 ] . Allison 
          et al [ 31 ] proposed 27-30 for
          older men and 30-35 for older women. In Figure 1, the
          from those of normal weight, suggesting that these two
          categories could be combined for older adults. Since
          future improvements in life expectancy may be limited [
          32 ] , the greatest advances may be made by improving
          people's YHL. This suggests that the development of
          future guidelines should take YHL or other measures of
          quality of life into account.
        
        
          Implications for clinical trials
          Based on these findings, trials to address obesity in
          older women could be efficient if YHL (but not YOL) was
          the outcome measure. That is, women who changed from
          being obese to being normal would likely show changes in
          YHL, but not YOL. Clinical trials of weight modification
          would appear to be fruitless since the interventions
          would probably not have a direct effect on either YOL or
          YHL.
          Weight or weight change are sometimes used as the
          outcome in evaluations of interventions such as diet or
          exercise programs. The fact that weight is not associated
          in a consistent way with health suggests that such
          evaluations should be considered critically when older
          adults are the subjects. This is particularly important
          in the light of recent findings, which found that
          interventions such as weight-loss drugs may be harmful [
          33 34 ] . For older adults, the risks associated with
          higher weight are especially unclear, and the optimal
          outcome for a trial of weight loss in older adults
          requires specific attention to improved health and
          mortality.
          Interestingly, the strongest health relationships were
          found for underweight older adults. Clinical trials whose
          objective was to make the underweight as healthy as their
          normal-weight peers (presumably by addressing the
          underlying conditions that caused the low weight) could
          be performed efficiently using either YOL or YHL as the
          outcome measure. Both YOL and YHL would be clinically
          significant in this patient group.
        
        
          Potential limitations
          CHS participants were somewhat healthier than the
          average older adult; however, adjustment for detailed
          covariates made little difference in the findings. We
          estimated the last four years of health data for about
          10% of the sample, but results with and without this
          group were similar. Analysis of mean YOL instead of the
          more traditional survival analysis survival analysis was
          appropriate here, since virtually no persons were lost to
          follow-up. Biases caused by over-adjustment are probably
          not large, since the findings were not sensitive to the
          number of variables adjusted for.
          These results are for a 7-year follow-up. The relative
          superiority of YHL to YOL would probably hold in trials
          with shorter follow-up. The effect sizes in Table 3might
          also be appropriate in shorter trials, since lengthy
          trials often add little information [ 10 ] .
          EVGFP, on which YHL was based, might have missed some
          effects of obesity on risk factors for future health. A
          person who is depressed because of a poor self-image
          related to obesity or who has osteo-arthritis related to
          obesity and limits to activities to successfully avoid
          pain would surely have worse EVGFP than others, based on
          results from many studies. However, health measures
          designed specifically to measure those conditions might
          be more sensitive to change in weight than EVGFP. If YHL
          were based on such measures, the superiority of YHL to
          YOL would likely be even greater than that shown here.
          These more sensitive measures might also have detected
          persons, but we think this is unlikely given the absence
          of any differences in EVGFP.
        
      
      
        Conclusion
        Recommendations for desirable weight have been
        criticized for emphasizing mortality rather than health. We
        found associations between YHL and obesity that were not
        present in the mortality analysis, suggesting that YHL may
        be a more sensitive measure of the burden of obesity in
        older adults, especially for women. Future efforts to
        determine desirable weight guidelines should include
        measures of YHL. Using either YOL or YHL, however, we found
        no excess risk for older adults who would be classified as
        YHL as the outcome measure in clinical trials involving
        obese or underweight older adults, and discouraging trials
      
      
        Competing interests
        None declared
      
      
        Abbreviations
        BMI Body mass index
        CESD Center for Epidemiologic Studies Depression
        Scale
        CHS Cardiovascular Health Study
        EVGFP Is your health excellent, very good, good, fair or
        poor?
        QALY Quality-adjusted life years
        YHL Years of healthy life
        YOL Years of life
```
The following command displays all the lines that do not have the pattern "overweight". This can be useful in narrowing down certain lines that you want to look at.
___

4. `grep -l`: Command line option `-l` makes it so that the search will display the names of the file that have the matching pattern. This is useful when you are searching for a pattern through multiple files without wanting to display the matched lines.

Examples:

```
william@Williams-MacBook-Air-3 biomed % grep -l "adults" 1468-6708-3-1.txt 1468-6708-3-3.txt 1468-6708-3-4.txt
1468-6708-3-1.txt
```

The following command displays the files that have the pattern "adult" within it. This is useful if have to look through multiple files and need to narrow it down through a keyword.

```
william@Williams-MacBook-Air-3 biomed % grep -l "overweight" 1468-6708-3-1.txt 1468-6708-3-3.txt 1468-6708-3-4.txt
1468-6708-3-1.txt
```

The following command displays the files that have the pattern "overweight" within it. This is useful if have to look through multiple files and need to narrow it down through a keyword.


**Sources**
https://www.gnu.org/savannah-checkouts/gnu/grep/manual/grep.html#Command_002dline-Options


