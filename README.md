
# Towards a FAIR and open methodology at NIME [working title]

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


## Audit

Below are a collection of script snippets and notes used for analysing the NIME proceedings archive.

### Download NIME papers

>[!NOTE]
> NIME 2021 and 2022 are a little more involved to pull the pdfs.
> You ~can~ could `curl` a PubPub article with 
> 
> ```
> https://nime.pubpub.org/pub/<PAPER_ID>/download/pdf
> ```
>
> This is currently broken. Pulling pdfs for these years will require another approach.


```sh
for year in {2002..2025}; do  
  mkdir "${year}"
  for paper in $(curl "https://raw.githubusercontent.com/NIME-conference/NIME-bibliography/refs/heads/master/paper_proceedings/nime${year}.bib"| grep -E "url\s+=\s+{" | grep -o -E "http.*"); do    
  paper="${paper:0:-2}"
  [[ $paper != https://* ]] && paper="https${paper:4}"    
    if [[ ${paper} == *"pubpub"* ]]; then
      curl "${paper}/download/pdf" -o "${paper:28}.pdf" --output-dir "${year}"
    elif [[ ${paper} == *"doi.org"* ]]; then         
      paperurl="$(curl -s ${paper} | grep -m 1 -o -E "https://nime.pubpub.org/pub/\w+" | tail -1)/download/pdf" 
      curl "${paperurl}" -o "${paperurl:28:-13}.pdf" --output-dir "${year}"
    else
      curl "${paper}" -O --output-dir "${year}"
    fi
  done  
done
```

## Data

See [`./data`](./data) directory for set of `.csv` and markdown tables listing papers, their repos and the link context.

### Zenodo Archives with Video files

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

## Grepping

Grepping of PDFs achieved  with [`pdfgrep`](https://gitlab.com/pdfgrep/pdfgrep).

```sh
pdfgrep -P '\Wgit' -rli . | wc -l   
```

which return a result the same as 

```sh
# (Year, GitHub, GitHub+sth., total)
for i in {2001..2025}; do
  cd "${i}"
  echo "(${i: -2}", $(pdfgrep -P 'github' -rli ./ | wc -l),  $(pdfgrep -P 'github' -rli . | xargs  pdfgrep -P '(^|\W)git(?!ch|imation|ter|udinal|arr|al|aroo|a|hub\b)' -rli | wc -l), $(ls | wc -l)  ")"
  cd - > /dev/null
done
```

### Trim Search

```sh
pdfgrep -P '\Wgit(?!hub|lab|ch|imation|ter|udinal|arr|al|aroo|a\b)' -ri .
pdfgrep -P '\Wgit(?!ch|imation|ter|udinal|arr|al|aroo|a\b)' -ri .
```

### Counting URLs

#### General Git References


```sh
for i in {2001..2025}; do
  cd "${i}"
  echo "(${i: -2}",$(( $(pdfgrep -P '\Wgit(?!ch|imation|ter|udinal|arr|al|aroo|a\b)' -rli . | wc -l) * 100 / $(ls | wc -l) ))")"
  cd - > /dev/null
done
```

```sh
for i in {2001..2025}; do
  cd "${i}"
  echo "(${i: -2}",$(( $(pdfgrep -P '\Wgit(?!ch|imation|ter|udinal|arr|al|aroo|a\b|hub\.io)' -rli . | wc -l) * 100 / $(ls | wc -l) ))")"
  cd - > /dev/null
done
```

```sh
for i in {2001..2025}; do
  cd "${i}"
  echo "(${i: -2}",$(pdfgrep -P '\Wgit(?!ch|imation|ter|udinal|arr|al|aroo|a\b)' -rli . | wc -l)")"
  cd - > /dev/null
done
```

For GitHub reference

```sh
for i in {2001..2025}; do
  cd "${i}"
  echo "(${i: -2}",$(( $(pdfgrep -P 'github' -rli . | wc -l) * 100 / $(ls | wc -l) ))")"
  cd - > /dev/null
done
```

```sh
for i in {2001..2025}; do
  cd "${i}"
  echo "(${i: -2}",$(( $(pdfgrep -P 'github(?!\.io)' -rli . | wc -l) * 100 / $(ls | wc -l) ))")"
  cd - > /dev/null
done
```

```sh
for i in {2001..2025}; do
  cd "${i}"
  echo "(${i: -2}",$(( $(pdfgrep -P 'github\.io' -rli . | wc -l) * 100 / $(ls | wc -l) ))")"
  cd - > /dev/null
done
```

```sh
for i in {2001..2025}; do
  cd "${i}"
  echo "(${i: -2}",$(( $(pdfgrep -P '(open source|open-source)' -rli . | wc -l) * 100 / $(ls | wc -l) ))")"
  cd - > /dev/null
done
```

#### Git occurences

```sh
for i in {2001..2025}; do
  cd "${i}"
  echo "(${i: -2}", $(pdfgrep -P '\Wgit(?!ch|imation|ter|udinal|arr|al|aroo|a\b)' -ri . | wc -l)")"
  cd - > /dev/null
done
```

#### Including sourceforge

```sh
for i in {2001..2025}; do
  cd "${i}"
  echo "(${i: -2}", $(pdfgrep -P '(\Wgit(?!ch|imation|ter|udinal|arr|al|aroo|a|sourceforge\.))' -rli . | wc -l), $(ls | wc -l)  ")"
  cd - > /dev/null
done
```


#### Just SourceForge


```sh
for i in {2001..2025}; do
  cd "${i}"
  echo "(${i: -2}", $(pdfgrep -P 'sourceforge\.' -rli . | wc -l), $(ls | wc -l)  ")"
  cd - > /dev/null
done
```

```sh
for i in {2001..2025}; do
  cd "${i}"
  echo "${i}" $(pdfgrep -P '\Wgit(?!ch|imation|ter|udinal|arr|al|aroo|a\b)' -rciH . | grep -v ':0$' | sort -t: -k2,2nr | head -3)
  echo ""
  cd - > /dev/null
done
```

#### Exclusive Github

```sh
for i in {2001..2025}; do
  cd "${i}"
  echo "(${i: -2}", $(pdfgrep -P 'github' -rli ./ | wc -l),  $(pdfgrep -P 'github' -rli . | xargs  pdfgrep -P '((^|\W)git(?!ch|imation|ter|udinal|arr|al|aroo|a|hub\b)|sourceforge\.)' -rli | wc -l),$(ls | wc -l)  ")"
  cd - > /dev/null
done
```