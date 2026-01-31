## NIME 2025 Audit

### Downloading NIME papers
```sh
# 2025
for i in {1..96}; do
  curl "https://nime.org/proceedings/2025/nime2025_${i}.pdf" -O
done

# 2024
for i in {1..94}; do
  curl "https://nime.org/proceedings/2024/nime2024_${i}.pdf" -O  
done

# 2023
for i in {1..99}; do
  curl "https://nime.org/proceedings/2023/nime2023_${i}.pdf" -O  
done

# 2020
for i in {1..99}; do
  curl "https://www.nime.org/proceedings/2020/nime2020_paper${i}.pdf" -O
done

# 2019
for i in {1..88}; do
  curl "https://www.nime.org/proceedings/2019/nime2019_paper${(l:3::0:)i}.pdf" -O
done

# 2018
for i in {1..92}; do
  curl "https://www.nime.org/proceedings/2018/nime2018_paper${(l:4::0:)i}.pdf" -O
done

# 2017
for i in {1..105}; do
  curl "https://www.nime.org/proceedings/2017/nime2017_paper${(l:4::0:)i}.pdf" -O  
done

# 2016
for i in {1..87}; do
  curl "https://www.nime.org/proceedings/2016/nime2016_paper${(l:4::0:)i}.pdf" -O  
done
```
```
for file in $(cat nime2015.csv); do
  curl "https://www.nime.org/proceedings/2015/${file}" -o "2015/${file}"
done
for file in $(cat nime2014.csv); do
  curl "https://www.nime.org/proceedings/2014/${file}" -o "2014/${file}"
done

for file in $(cat nime2013.csv); do
  curl "https://www.nime.org/proceedings/2013/${file}" -o "2013/${file}"
done

for file in $(cat nime2012.csv); do
  curl "https://www.nime.org/proceedings/2012/${file}" -o "2012/${file}"
done

for file in $(cat nime2011.csv); do
  curl "https://www.nime.org/proceedings/2011/${file}" -o "2011/${file}"
done

for file in $(cat nime2010.csv); do
  curl "https://www.nime.org/proceedings/2010/${file}" -o "2010/${file}"
done

for file in $(cat nime2009.csv); do
  curl "https://www.nime.org/proceedings/2009/${file}" -o "2009/${file}"
done

for file in $(cat nime2008.csv); do
  curl "https://www.nime.org/proceedings/2008/${file}" -o "2008/${file}"
done


for file in $(cat nime2008.csv); do
  curl "https://www.nime.org/proceedings/2008/${file}" -o "2008/${file}"
done

mkdir 2007
for file in $(cat nime2007.csv); do
  curl "https://www.nime.org/proceedings/2007/${file}" -o "2007/${file}"
done

mkdir 2006
for file in $(cat nime2006.csv); do
  curl "https://www.nime.org/proceedings/2006/${file}" -o "2006/${file}"
done

mkdir 2006
for file in $(cat nime2006.csv); do
  curl "https://www.nime.org/proceedings/2006/${file}" -o "2006/${file}"
done

mkdir 2005
for file in $(cat nime2005.csv); do
  curl "https://www.nime.org/proceedings/2005/${file}" -o "2005/${file}"
done

mkdir 2004
for file in $(cat nime2004.csv); do
  curl "https://www.nime.org/proceedings/2004/${file}" -o "2004/${file}"
done

mkdir 2003
for file in $(cat nime2003.csv); do
  curl "https://www.nime.org/proceedings/2003/${file}" -o "2003/${file}"
done

mkdir 2002
for file in $(cat nime2002.csv); do
  curl "https://www.nime.org/proceedings/2002/${file}" -o "2002/${file}"
done

mkdir 2001
for file in $(cat nime2001.csv); do
  curl "https://www.nime.org/proceedings/2001/${file}" -o "2001/${file}"
done
```

### Counting for plot
```
for i in {2001..2025}; do
  cd "${i}"
  echo "${i}",$(( $(pdfgrep -P 'github' -rli . | wc -l) * 100 / $(ls | wc -l) ))
  cd - > /dev/null
done
```

NIME 2021 and 2022 are a little more involved to pull the pdfs.
Can `curl` a PubPub article with 

```
https://nime.pubpub.org/pub/<PAPER_ID>/download/pdf
```

The list of PAPER_IDs was pulled from the bib files on the [NIME bibliography git](https://github.com/NIME-conference/NIME-bibliography/tree/master)

### Grepping

```sh
pdfgrep -P '\Wgit' -rli . | wc -l   
```

which return a result the same as 

```sh
pdfgrep -P '\b(git|github|gitlab)\b|(https?://|www\.)\S*(git|github|gitlab)\S*' -rli ./ | wc -l
```

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

### Papers with Repo or Archive link

See [`./data/papers_with_repos.csv`](./data/papers_with_repos.csv), a pipe separated list of papers, repos and their context.

- nime2025_9
- nime2025_10
- nime2025_14
- nime2025_15
- nime2025_16
- nime2025_21
- nime2025_32
- nime2025_36
- nime2025_37
- nime2025_39
- nime2025_40
- nime2025_42
- nime2025_48
- nime2025_54
- nime2025_57
- nime2025_58
- nime2025_59
- nime2025_61
- nime2025_62
- nime2025_64
- nime2025_65
- nime2025_67
- nime2025_69
- nime2025_73
- nime2025_75
- nime2025_81
- nime2025_84
- nime2025_90
- nime2025_93

### Missing Repos

All of these _have_ repositories, just not accessible

| id          | paper      | State   | reason     | url                                                     | page | placement | context                                                    |
| ----------- | ---------- | ------- | ---------- | ------------------------------------------------------- | ---- | --------- | ---------------------------------------------------------- |
| nime2025_60 | Cicadas    | auth    |            | http://gitea.offig.com/lfsadmin/Cicadas                 | 2    | body      | Full code for the generative algorithm is available at     |
| nime2025_79 | Drum Tao   | empty   |            | https://red-x-silver.github.io/the-drum-machine-of-tao/ | 1    | footnote  | Results from a prototype are available for listening1      |
| nime2025_74 | Mindcube   | empty   | wrong repo | https://github.com/mitmedialab/mindcube- rave           | 3    | footnote  | An implementation of this mapping can be found on GitHub1. |
| nime2025_91 | glitchgate | private |            | https://github.com/ijc8/glitchgate                      | 1    | footnote  | The source code for glitchgate is available at             |
| nime2025_92 | Smuck      | missing | extant     | https://github.com/ccrma/smuck                          |      |           |                                                            |

###  Repos inaccessible in References
	
| id          | paper              | State   | reason          | url                                 | page | placement  | context                                                                                |
| ----------- | ------------------ | ------- | --------------- | ----------------------------------- | ---- | ---------- | -------------------------------------------------------------------------------------- |
| nime2025_69 | Global drum circle | private | "unpublishable" | https://github.com/rbdannenberg/gdc |      | references | Roger Dannenberg and Ari Liloia. 2022. Global Drum Circle (Private Github Repository). |

