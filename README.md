# "See Link for More Details": Towards a Pragmatic Open Methodology at NIME
[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.194436176.svg)](https://doi.org/10.5281/zenodo.19443616)

- ["See Link for More Details": Towards a Pragmatic Open Methodology at NIME](#see-link-for-more-details-towards-a-pragmatic-open-methodology-at-nime)
  - [Abstract](#abstract)
  - [Important Dates:](#important-dates)
  - [Data](#data)
    - [NIME 2025 Zenodo Archives with Additional Files](#nime-2025-zenodo-archives-with-additional-files)
  - [Audit](#audit)
    - [Download NIME papers](#download-nime-papers)
    - [Grepping](#grepping)
    - [Searching for URLs](#searching-for-urls)
      - [Prune Search](#prune-search)
        - [Remove false positives and obvious references](#remove-false-positives-and-obvious-references)
        - [Remove false positives](#remove-false-positives)
      - [Finding Source Repositories](#finding-source-repositories)
      - [General Git References Count](#general-git-references-count)
        - [Git URLs %  (pruned)](#git-urls---pruned)
        - [Git URLs % (pruned) no github.io](#git-urls--pruned-no-githubio)
        - [Git URLs count (pruned)](#git-urls-count-pruned)
        - [GitHub term use %](#github-term-use-)
        - [GitHub term use % (no github.io)](#github-term-use--no-githubio)
        - [github.io use %](#githubio-use-)
        - [Open Source term use %](#open-source-term-use-)
        - [Git term use count](#git-term-use-count)
        - [Git and SourceForge count](#git-and-sourceforge-count)
        - [SourceForge only count](#sourceforge-only-count)
        - [Total Reference per year / paper](#total-reference-per-year--paper)
        - [Exclusive Github](#exclusive-github)
        - [Count NIME Papers](#count-nime-papers)
    - [Reference Counting](#reference-counting)
      - [List Reference](#list-reference)
      - [Count References (Python)](#count-references-python)
      - [Frequency (Python)](#frequency-python)
  - [NIME Stats](#nime-stats)
    - [Number of Papers](#number-of-papers)
    - [Source Material URL Context Distribution](#source-material-url-context-distribution)
    - [Average Number of References per Paper](#average-number-of-references-per-paper)
    - [Reference Distributions](#reference-distributions)
  - [Lessons Learned](#lessons-learned)
    - [Recommendations](#recommendations)


## Abstract

Since its inception, NIME has been committed to open research, with a strong tradition of open source practice running through its history. In the context of the NIME 2026 theme of communities, this paper examines current open research practices at NIME and explores how they might be developed to better engage a new generation of creators beyond the conference itself.
Through an analysis of NIME 2025 proceedings, we assess how source materials—including software, hardware designs, data, and documentation—are shared, discovered, and cited. The analysis reveals a growing familiarity with open source tools, alongside persistent barriers to discoverability, reuse, and long-term access.
Drawing on the documentation and dissemination process of a recent NIME, the paper outlines a deliberate and visible open methodology that treats Digital Musical Interfaces as evolving, reusable research objects for a wider community rather than closed artefacts tied solely to a publication. 
The paper concludes by reflecting on current limitations and proposes practical ways to lower barriers to reusing and recreating NIMEs, framing ``good-enough'' open research as a catalyst for further participation, knowledge exchange, and impact beyond the current NIME community.

## Important Dates:
All dates are 23:59 AoE (Anywhere on Earth).

- [x] 4 December 2025: Submission CMT Site opens
- [x] 5 February 2026: Papers and Music - Titles, abstracts and author lists due
- [x] 12 February 2026: Papers and Music - Final submissions due
- [x] 5 March 2026: Workshop, alt.NIME and Student Consortium submissions due
- [x] 3 April 2026: Acceptance decisions and reviews released
- [ ] 30 April 2026: Camera ready and presenter registration deadline
- [ ] 23 June 2026: NIME Workshops and Student Consortium
- [ ] 24-26 June 2026: NIME Conference

## Data

See [`./data`](./data) directory for set of `.csv` and markdown tables listing papers, their repos and the link context.

> [!NOTE]
> **Data Format**
>
> The "placement" field for the repository data referes to where in the paper the link was shared. In some cases there is an additional value in round braces denoting if the link was shared using link shortening, a hyperlink (obfuscating the URL from text search) or `missing`. In the `missing` case, this typically means that the URL leads to some kind of server error or to an authentication page. For the `data/cite-methods.csv`, `missing` takes precedence e.g., `footnote (missing)` would be counted as `missing` not as `footnote`.
>
> The data is also not yet fully standardised. Originally there was an `inferred` category for extant repositories that were not linked to in the paper. The `inferred` case should will be consolidated into the `missing` category.
>
> For instances where the source material link is shared more than once, a semicolon is used to delimit.
>
> `reference` and `citation` have been used interchangeably. This will be consolidated into `citation` in a future update.

### NIME 2025 Zenodo Archives with Additional Files

All additional files are video

- https://zenodo.org/records/15699550
- https://zenodo.org/records/15699591
- https://zenodo.org/records/15699598
- https://zenodo.org/records/15699614
- https://zenodo.org/records/15699626
- https://zenodo.org/records/15699633
- https://zenodo.org/records/15699645
- https://zenodo.org/records/15699652
- https://zenodo.org/records/15698912
- https://zenodo.org/records/15699656
- https://zenodo.org/records/15698936
- https://zenodo.org/records/15699662
- https://zenodo.org/records/15698970
- https://zenodo.org/records/15698972
- https://zenodo.org/records/15698986
- https://zenodo.org/records/15699671

## Audit

Below are a collection of script snippets and notes used for analysing the NIME proceedings archive.

### Download NIME papers

```sh
for year in {2001..2025}; do  
  curl https://www.nime.org/proceedings/ZIPs/${year}.zip -O
done

tar_years=(2011 2013 2014 2017)
zip_years=(2001 2002 2003 2004 2005 2006 2007 2008 2009 2010 2012 2016 2019 2020 2021 2022 2023 2024 2025)

for year in "${zip_years[@]}"; do
  unzip "${year}.zip" -d ./
done

for year in "${tar_years[@]}"; do
  tar -xf "${year}.zip" -C ./
done

unzip "2015.zip" -d ./2015/

for year in {2001..2025}; do  
  rm "${year}.zip"
done
```

### Grepping

Grepping of PDFs achieved  with [`pdfgrep`](https://gitlab.com/pdfgrep/pdfgrep).

```sh
pdfgrep -P '\Wgit' -rli . | wc -l   
```

### Searching for URLs

Assuming the NIME archive has been downloaded [using the directory structure above](#download-nime-papers), you can run these zshell snippets to get some data.

#### Prune Search

Search results are pruned for false positives using a gradual developed regular expression.

##### Remove false positives and obvious references

This was used to more easily identify false positives as github and gitlab made up the bulk of references.

This helped find cases such as gitorious and smaller institute git repositories.

It still captures github / gitlab URLs ending in `.git` but there were far fewer instances and could be removed manually.

```sh
pdfgrep -P '\Wgit(?!hub|lab|ch|imation|ter|udinal|arr|al|aroo|a\b)' -ri .
```

##### Remove false positives

Final pruned search term so only git and git urls were captured.

```sh
pdfgrep -P '\Wgit(?!ch|imation|ter|udinal|arr|al|aroo|a\b)' -ri .
```

#### Finding Source Repositories

This was used as starting point to identify a pool of papers most likely to provide a source material repo.
papers not on this list were subsequently searched for `http` and `www` then skim read manually in case hyper links were used.

```sh
for i in {2001..2025}; do
  cd "${i}"
  echo Searching $i
  pdfgrep -P '(\Wgit(?!ch|imation|ter|udinal|arr|al|aroo|a\b)|open source|open-source)' -rli . | sort > "../repo_search_${i}.txt"
  cd - > /dev/null
done
```

#### General Git References Count

Most of these are fomratted for direct use in a [tikz pgfplot](https://tikz.dev/pgfplots/). The article uses the same data in CSV format from [`data/opensource-use.csv`](./data/opensource-use.csv).

##### Git URLs %  (pruned)

```sh
for i in {2001..2025}; do
  cd "${i}"
  percent=$(echo "scale=2; $(pdfgrep -P '\Wgit(?!ch|imation|ter|udinal|arr|al|aroo|a\b)' -rli . | wc -l) * 100 / $(ls | wc -l)" | bc)
  echo "(${i: -2},${percent})"
  cd - > /dev/null
done
```

##### Git URLs % (pruned) no github.io

```sh
for i in {2001..2025}; do
  cd "${i}"
  percent=$(echo "scale=2; $(pdfgrep -P '\Wgit(?!ch|imation|ter|udinal|arr|al|aroo|a\b|hub\.io)' -rli . | wc -l) * 100 / $(ls | wc -l)" | bc)
  echo "(${i: -2},${percent})"
  cd - > /dev/null
done
```

##### Git URLs count (pruned)

```sh
for i in {2001..2025}; do
  cd "${i}"
  echo "(${i: -2}",$(pdfgrep -P '\Wgit(?!ch|imation|ter|udinal|arr|al|aroo|a\b)' -rli . | wc -l)")"
  cd - > /dev/null
done
```

##### GitHub term use %

```sh
for i in {2001..2025}; do
  cd "${i}"
  percent=$(echo "scale=2; $(pdfgrep -P 'github' -rli . | wc -l) * 100 / $(ls | wc -l)" | bc)
  echo "(${i: -2},${percent})"
  cd - > /dev/null
done
```

##### GitHub term use % (no github.io)

```sh
for i in {2001..2025}; do
  cd "${i}"
  percent=$(echo "scale=2; $(pdfgrep -P 'github(?!\.io)' -rli . | wc -l) * 100 / $(ls | wc -l)" | bc)
  echo "(${i: -2},${percent})"
  cd - > /dev/null
done
```

##### github.io use %

```sh
for i in {2001..2025}; do
  cd "${i}"
  percent=$(echo "scale=2; $(pdfgrep -P 'github\.io' -rli . | wc -l) * 100 / $(ls | wc -l)" | bc)
  echo "(${i: -2},${percent})"
  cd - > /dev/null
done
```

##### Open Source term use %

```sh
for i in {2001..2025}; do
  cd "${i}"
  percent=$(echo "scale=2; $(pdfgrep -P '(open source|open-source)' -rli . | wc -l) * 100 / $(ls | wc -l)" | bc)
  echo "(${i: -2},${percent})"
  cd - > /dev/null
done
```

##### Git term use count

```sh
for i in {2001..2025}; do
  cd "${i}"
  echo "(${i: -2}", $(pdfgrep -P '\Wgit(?!ch|imation|ter|udinal|arr|al|aroo|a\b)' -ri . | wc -l)")"
  cd - > /dev/null
done
```

##### Git and SourceForge count

```sh
for i in {2001..2025}; do
  cd "${i}"
  echo "(${i: -2}", $(pdfgrep -P '(\Wgit(?!ch|imation|ter|udinal|arr|al|aroo|a)|sourceforge\.)' -rli . | wc -l), $(ls | wc -l)  ")"
  cd - > /dev/null
done
```

##### SourceForge only count

```sh
for i in {2001..2025}; do
  cd "${i}"
  echo "(${i: -2}", $(pdfgrep -P 'sourceforge\.' -rli . | wc -l), $(ls | wc -l)  ")"
  cd - > /dev/null
done
```


##### Total Reference per year / paper

List the total count of git reference each year. Help identify instances of high term usage in a paper / year.

```sh
for i in {2001..2025}; do
  cd "${i}"
  echo "${i}" $(pdfgrep -P '\Wgit(?!ch|imation|ter|udinal|arr|al|aroo|a\b)' -rciH . | grep -v ':0$' | sort -t: -k2,2nr | head -3)
  echo ""
  cd - > /dev/null
done
```

##### Exclusive Github

Papers that have exclusively used github and no other git service or source forge repository.

```sh
for i in {2001..2025}; do
  cd "${i}"
  echo "(${i: -2}", $(pdfgrep -P 'github' -rli ./ | wc -l),  $(pdfgrep -P 'github' -rli . | xargs  pdfgrep -P '((^|\W)git(?!ch|imation|ter|udinal|arr|al|aroo|a|hub\b)|sourceforge\.)' -rli | wc -l),$(ls | wc -l)  ")"
  cd - > /dev/null
done
```


##### Count NIME Papers

```sh
for i in {2001..2025}; do
  cd "${i}"
  echo "(${i: -2}", $(ls *.pdf | wc -l)")"
  cd - > /dev/null
done
```

### Reference Counting

#### List Reference

```sh
for i in {2001..2025}; do
  cd "${i}"
  pdfgrep -P '\[\d{1,3}\]' -ri . > "../references_${i}.txt"
  cd - > /dev/null
done
```

#### Count References (Python)

```py
import re 

ref_counts_by_year = {}

for year in range(2001,2026):
  if year not in ref_counts_by_year:
    ref_counts_by_year[year] = {}
  with open(f"references_{year}.txt") as ref_file:
    for line in ref_file:
      if not line.startswith('./'):
        continue
      id = line[2:line.find(":")]
      if id not in ref_counts_by_year[year]:        
        ref_counts_by_year[year][id] = 0;
      ref_num = int(re.search('\[(\d{1,3})\]', line)[1])
      if ref_num < 200:
        ref_counts_by_year[year][id] = ref_num if ref_num > ref_counts_by_year[year][id] else ref_counts_by_year[year][id];

print(f"year,total,mean,median")

for year in range(2001,2026):
  ref_list = []
  year_total = 0;
  year_mean = 0;
  
  for key in ref_counts_by_year[year]:
    year_total += ref_counts_by_year[year][key]
    ref_list.append(ref_counts_by_year[year][key])
  
  ref_list.sort()
  year_mean = year_total / len(ref_counts_by_year[year].items())
  year_median = ref_list[len(ref_list)//2]
  print(f"{year},{year_total},{year_mean:.1f},{year_median}")

```

#### Frequency (Python)


```py
ref_counts_by_year = {}

for year in range(2001,2026):
  if year not in ref_counts_by_year:
    ref_counts_by_year[year] = {}
  with open(f"references_{year}.txt") as ref_file:
    for line in ref_file:
      if not line.startswith('./'):
        continue
      id = line[2:line.find(":")]
      if id not in ref_counts_by_year[year]:        
        ref_counts_by_year[year][id] = 0;
      ref_num = int(re.search('\[(\d{1,3})\]', line)[1])
      if ref_num < 200:
        ref_counts_by_year[year][id] = ref_num if ref_num > ref_counts_by_year[year][id] else ref_counts_by_year[year][id];

# min, max
bins = ((0,5),(5,10),(10,15),(15,20),(20,30),(30,40),(40,50),(50,60),(60,70),(70,1000))

freq_dist = {year:{bin:0 for bin  in bins} for year in ref_counts_by_year}

for year in ref_counts_by_year:
  
  for paper in ref_counts_by_year[year]:
      num_refs = ref_counts_by_year[year][paper]
      for bin in bins:
        if num_refs >= bin[0] and num_refs < bin[1]:
          freq_dist[year][bin] += 1
          continue

for year in range(2001,2026):
  num_papers = len(ref_counts_by_year[year].keys())
  for bin in bins:
    freq_dist[year][bin] /= num_papers
    freq_dist[year][bin] *= 100.0



for year in range(2001,2026):
    a = """
    ```mermaid
    xychart
        title "{}"
        x-axis ["0-5", "5-10", "10-15", "15-20", "20-30", "30-40", "40-50", "50-60", "60-70", "70+"]
        y-axis "Freq. Reference Percent" 0 --> 100
        bar {}
    ```    
    """.format(year,list(freq_dist[year].values()))
    print(a)  
```

## NIME Stats
### Number of Papers

```mermaid
xychart
    title "NIME Proceedings (Total Papers: 2269)"
    x-axis ["'01", "'02", "'03", "'04", "'05", "'06", "'07", "'08", "'09", "'10", "'11", "'12", "'13", "'14", "'15", "'16", "'17", "'18", "'19", "'20", "'21", "'22", "'23", "'24", "'25"]
    y-axis "Total Papers" 0 --> 160
    bar [14, 48, 48, 54, 77, 86, 104, 87, 110, 111, 130, 129, 118, 148, 103, 84, 105, 92, 88, 100, 88, 56, 99, 94, 96] 
```

### Source Material URL Context Distribution

```mermaid
xychart
title "URL Context Percentage Distribution"
x-axis "Year" ["'17", "'18", "'19", "'20", "'21", "'22", "'23", "'24", "'25"]
y-axis "Overall %" 0 --> 100
%% Blue
bar [100.00, 100.00, 100.00, 100.00, 100.00, 100.00, 100.00, 100.00, 100.00]
%% Green
bar [100.00, 88.89, 95.24, 100.00, 100.00, 86.67, 96.55, 95.83, 90.00]
%% Red
bar [100.00, 88.89, 71.43, 100.00, 90.00, 80.00, 93.10, 83.33, 83.33]
%% Yellow
bar [70.00, 66.67, 57.14, 47.06, 65.00, 40.00, 55.17, 58.33, 60.00]
```

- 🟨 Footnote
- 🟥 Body
- 🟩 Citation
- 🟦 Appendix

### Average Number of References per Paper

```mermaid
xychart
    title "Average References"
    x-axis ["'01", "'02", "'03", "'04", "'05", "'06", "'07", "'08", "'09", "'10", "'11", "'12", "'13", "'14", "'15", "'16", "'17", "'18", "'19", "'20", "'21", "'22", "'23", "'24", "'25"]
    y-axis "num references" 0 --> 35    
    line [10.6, 9.0, 16.7, 12.0, 13.0, 15.2, 14.7, 13.8, 10.9, 14.5, 13.8, 14.4, 15.8, 15.9, 15.3, 19.8, 17.3, 19.7, 19.9, 20.5, 25.0, 31.9, 28.9, 30.2, 31.7]
    line [13, 8, 13, 11, 11, 16, 14, 13, 10, 13, 13, 13, 15, 15, 14, 19, 17, 18, 17, 19, 22, 28, 23, 27, 28]
```

- 🟦 Mean
- 🟩 Median

### Reference Distributions

```mermaid
xychart
    title "2001"
    x-axis ["0-5", "5-10", "10-15", "15-20", "20-30", "30-40", "40-50", "50-60", "60-70", "70+"]
    y-axis "Freq. Reference Percent" 0 --> 40
    bar [20.0, 30.0, 20.0, 30.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0]
```    


```mermaid
xychart
    title "2002"
    x-axis ["0-5", "5-10", "10-15", "15-20", "20-30", "30-40", "40-50", "50-60", "60-70", "70+"]
    y-axis "Freq. Reference Percent" 0 --> 40
    bar [21.951219512195124, 34.146341463414636, 24.390243902439025, 19.51219512195122, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0]
```    


```mermaid
xychart
    title "2003"
    x-axis ["0-5", "5-10", "10-15", "15-20", "20-30", "30-40", "40-50", "50-60", "60-70", "70+"]
    y-axis "Freq. Reference Percent" 0 --> 40
    bar [8.51063829787234, 25.53191489361702, 17.02127659574468, 14.893617021276595, 23.404255319148938, 4.25531914893617, 2.127659574468085, 4.25531914893617, 0.0, 0.0]
```    


```mermaid
xychart
    title "2004"
    x-axis ["0-5", "5-10", "10-15", "15-20", "20-30", "30-40", "40-50", "50-60", "60-70", "70+"]
    y-axis "Freq. Reference Percent" 0 --> 40
    bar [11.538461538461538, 34.61538461538461, 25.0, 13.461538461538462, 11.538461538461538, 3.8461538461538463, 0.0, 0.0, 0.0, 0.0]
```    


```mermaid
xychart
    title "2005"
    x-axis ["0-5", "5-10", "10-15", "15-20", "20-30", "30-40", "40-50", "50-60", "60-70", "70+"]
    y-axis "Freq. Reference Percent" 0 --> 40
    bar [11.428571428571429, 20.0, 35.714285714285715, 20.0, 11.428571428571429, 0.0, 0.0, 0.0, 1.4285714285714286, 0.0]
```    


```mermaid
xychart
    title "2006"
    x-axis ["0-5", "5-10", "10-15", "15-20", "20-30", "30-40", "40-50", "50-60", "60-70", "70+"]
    y-axis "Freq. Reference Percent" 0 --> 40
    bar [4.054054054054054, 21.62162162162162, 22.972972972972975, 28.37837837837838, 18.91891891891892, 4.054054054054054, 0.0, 0.0, 0.0, 0.0]
```    


```mermaid
xychart
    title "2007"
    x-axis ["0-5", "5-10", "10-15", "15-20", "20-30", "30-40", "40-50", "50-60", "60-70", "70+"]
    y-axis "Freq. Reference Percent" 0 --> 40
    bar [10.344827586206897, 17.24137931034483, 29.88505747126437, 18.39080459770115, 19.54022988505747, 2.2988505747126435, 2.2988505747126435, 0.0, 0.0, 0.0]
```    


```mermaid
xychart
    title "2008"
    x-axis ["0-5", "5-10", "10-15", "15-20", "20-30", "30-40", "40-50", "50-60", "60-70", "70+"]
    y-axis "Freq. Reference Percent" 0 --> 40
    bar [6.097560975609756, 28.04878048780488, 24.390243902439025, 25.609756097560975, 12.195121951219512, 3.6585365853658534, 0.0, 0.0, 0.0, 0.0]
```    


```mermaid
xychart
    title "2009"
    x-axis ["0-5", "5-10", "10-15", "15-20", "20-30", "30-40", "40-50", "50-60", "60-70", "70+"]
    y-axis "Freq. Reference Percent" 0 --> 40
    bar [12.5, 36.36363636363637, 28.40909090909091, 13.636363636363635, 7.954545454545454, 1.1363636363636365, 0.0, 0.0, 0.0, 0.0]
```    


```mermaid
xychart
    title "2010"
    x-axis ["0-5", "5-10", "10-15", "15-20", "20-30", "30-40", "40-50", "50-60", "60-70", "70+"]
    y-axis "Freq. Reference Percent" 0 --> 40
    bar [2.727272727272727, 22.727272727272727, 30.909090909090907, 24.545454545454547, 16.363636363636363, 1.8181818181818181, 0.9090909090909091, 0.0, 0.0, 0.0]
```    


```mermaid
xychart
    title "2011"
    x-axis ["0-5", "5-10", "10-15", "15-20", "20-30", "30-40", "40-50", "50-60", "60-70", "70+"]
    y-axis "Freq. Reference Percent" 0 --> 40
    bar [3.875968992248062, 26.356589147286826, 31.782945736434108, 20.155038759689923, 15.503875968992247, 1.550387596899225, 0.7751937984496124, 0.0, 0.0, 0.0]
```    


```mermaid
xychart
    title "2012"
    x-axis ["0-5", "5-10", "10-15", "15-20", "20-30", "30-40", "40-50", "50-60", "60-70", "70+"]
    y-axis "Freq. Reference Percent" 0 --> 40
    bar [5.46875, 14.0625, 36.71875, 25.0, 17.1875, 0.78125, 0.0, 0.0, 0.78125, 0.0]
```    


```mermaid
xychart
    title "2013"
    x-axis ["0-5", "5-10", "10-15", "15-20", "20-30", "30-40", "40-50", "50-60", "60-70", "70+"]
    y-axis "Freq. Reference Percent" 0 --> 40
    bar [3.4482758620689653, 18.103448275862068, 25.862068965517242, 28.448275862068968, 15.517241379310345, 7.758620689655173, 0.8620689655172413, 0.0, 0.0, 0.0]
```    


```mermaid
xychart
    title "2014"
    x-axis ["0-5", "5-10", "10-15", "15-20", "20-30", "30-40", "40-50", "50-60", "60-70", "70+"]
    y-axis "Freq. Reference Percent" 0 --> 40
    bar [2.7027027027027026, 18.91891891891892, 28.37837837837838, 17.56756756756757, 29.054054054054053, 2.7027027027027026, 0.0, 0.0, 0.6756756756756757, 0.0]
```    


```mermaid
xychart
    title "2015"
    x-axis ["0-5", "5-10", "10-15", "15-20", "20-30", "30-40", "40-50", "50-60", "60-70", "70+"]
    y-axis "Freq. Reference Percent" 0 --> 40
    bar [2.941176470588235, 23.52941176470588, 25.49019607843137, 27.450980392156865, 12.745098039215685, 5.88235294117647, 0.9803921568627451, 0.9803921568627451, 0.0, 0.0]
```    


```mermaid
xychart
    title "2016"
    x-axis ["0-5", "5-10", "10-15", "15-20", "20-30", "30-40", "40-50", "50-60", "60-70", "70+"]
    y-axis "Freq. Reference Percent" 0 --> 40
    bar [0.0, 8.536585365853659, 18.29268292682927, 25.609756097560975, 34.146341463414636, 10.975609756097562, 2.4390243902439024, 0.0, 0.0, 0.0]
```    


```mermaid
xychart
    title "2017"
    x-axis ["0-5", "5-10", "10-15", "15-20", "20-30", "30-40", "40-50", "50-60", "60-70", "70+"]
    y-axis "Freq. Reference Percent" 0 --> 40
    bar [5.769230769230769, 11.538461538461538, 24.03846153846154, 24.03846153846154, 24.03846153846154, 9.615384615384617, 0.9615384615384616, 0.0, 0.0, 0.0]
```    


```mermaid
xychart
    title "2018"
    x-axis ["0-5", "5-10", "10-15", "15-20", "20-30", "30-40", "40-50", "50-60", "60-70", "70+"]
    y-axis "Freq. Reference Percent" 0 --> 40
    bar [4.3478260869565215, 7.608695652173914, 30.434782608695656, 14.130434782608695, 26.08695652173913, 10.869565217391305, 5.434782608695652, 1.0869565217391304, 0.0, 0.0]
```    


```mermaid
xychart
    title "2019"
    x-axis ["0-5", "5-10", "10-15", "15-20", "20-30", "30-40", "40-50", "50-60", "60-70", "70+"]
    y-axis "Freq. Reference Percent" 0 --> 40
    bar [1.1363636363636365, 11.363636363636363, 22.727272727272727, 21.59090909090909, 26.136363636363637, 10.227272727272728, 6.8181818181818175, 0.0, 0.0, 0.0]
```    


```mermaid
xychart
    title "2020"
    x-axis ["0-5", "5-10", "10-15", "15-20", "20-30", "30-40", "40-50", "50-60", "60-70", "70+"]
    y-axis "Freq. Reference Percent" 0 --> 40
    bar [2.0408163265306123, 10.204081632653061, 12.244897959183673, 29.591836734693878, 31.63265306122449, 9.183673469387756, 3.061224489795918, 2.0408163265306123, 0.0, 0.0]
```    


```mermaid
xychart
    title "2021"
    x-axis ["0-5", "5-10", "10-15", "15-20", "20-30", "30-40", "40-50", "50-60", "60-70", "70+"]
    y-axis "Freq. Reference Percent" 0 --> 40
    bar [0.0, 9.090909090909092, 14.772727272727273, 14.772727272727273, 32.95454545454545, 11.363636363636363, 10.227272727272728, 4.545454545454546, 0.0, 2.272727272727273]
```    


```mermaid
xychart
    title "2022"
    x-axis ["0-5", "5-10", "10-15", "15-20", "20-30", "30-40", "40-50", "50-60", "60-70", "70+"]
    y-axis "Freq. Reference Percent" 0 --> 40
    bar [0.0, 1.7857142857142856, 10.714285714285714, 16.071428571428573, 25.0, 25.0, 8.928571428571429, 8.928571428571429, 0.0, 3.571428571428571]
```    


```mermaid
xychart
    title "2023"
    x-axis ["0-5", "5-10", "10-15", "15-20", "20-30", "30-40", "40-50", "50-60", "60-70", "70+"]
    y-axis "Freq. Reference Percent" 0 --> 40
    bar [0.0, 4.081632653061225, 15.306122448979592, 18.367346938775512, 27.55102040816326, 13.26530612244898, 10.204081632653061, 5.1020408163265305, 2.0408163265306123, 4.081632653061225]
```    


```mermaid
xychart
    title "2024"
    x-axis ["0-5", "5-10", "10-15", "15-20", "20-30", "30-40", "40-50", "50-60", "60-70", "70+"]
    y-axis "Freq. Reference Percent" 0 --> 40
    bar [0.0, 4.25531914893617, 13.829787234042554, 10.638297872340425, 27.659574468085108, 19.148936170212767, 10.638297872340425, 3.1914893617021276, 8.51063829787234, 2.127659574468085]
```    


```mermaid
xychart
    title "2025"
    x-axis ["0-5", "5-10", "10-15", "15-20", "20-30", "30-40", "40-50", "50-60", "60-70", "70+"]
    y-axis "Freq. Reference Percent" 0 --> 40
    bar [0.0, 4.166666666666666, 10.416666666666668, 15.625, 27.083333333333332, 15.625, 10.416666666666668, 7.291666666666667, 4.166666666666666, 5.208333333333334]
```

## Lessons Learned

- PDFs aren't great for this kind of analysis
  - Finding specific text can have some interesting edge cases 
  - finding the context (body, footnote, appendix &c.) requires looking at something like fontsize.
- TeX is better for this kind of analysis
  - PubPub offers a LaTeX export.
  - currently can't `curl` PDFs from PubPub where you could previously. Instead, the download URL can be opened programatically.
  - identifying footnotes, URLs and citation is far easier
  - reference contained in bib entries need to be accounted for
- A markup language, like HTML, is even better
  - Still blocked by PubPub
- Using TinyUrl and bit.ly might not be a good idea
  - also hyperlinks
- Perhaps still some confusion as the meaning of "open source"
  - e.g. free binaries are not open source
  - also, ideally the source is presented
- Latex loves to break links in the PDF
- pgf-tikz's pgfplots is great
  - Data stays with the document (unlike images or vector graphics)
  - in fact any plotting system, like mermaid, that provides both the visual representation and underlying raw data is preferable

### Recommendations

- Adding a repo link field in the paper template and metadata would make it much easier to find
  - it would also make it easier to flag 'openwashing'
- A markup language version of NIME papers would be more permissive to analysis
  - it would also avoid links breaking by insertion of spaces and line breaks
  - it would allow unwieldy links to be hyperlinked, avoiding the need for link shortening services, the use of which should be discouraged
- If NIME welcomes analysis, need to make sure the text can be accessed programatically
