## intro


## prev research

follwoing up or recreating previous nies becomes archival research. tryin to find the coorect resources, dusting off the old links or querying the way back machine for now dead links.

This becomes digital archaelogy fast, and this not the unearthing of resources long forgotten for hundreds of year, but research barely into double figures of years old.

This is not a way to approach resarch, this is not how all other research would be expected to behave.

(maybe from the old journal system of buying journals and charging for back issues, but that was to meet the overheads in labour required to facilitate those issues which in a digigtal world should be entirely trivial, this was on the face not meant to be a for profit academic system, so the idea that digital research can be held to the same standard as what it was to find old research from a pre-digital age is disingenuous.)

## modular methodology

rather an prescriptive approach of a single template repository or collective repository, a modular system is proposed.

DMI's can be considered to be made from multiple components. Be that materials, process, software / firmware.

ratherthan a template repository, a DMI's components, if the DMI is not ephemeral, have some version control

Not a central repository, but the inclusion of a DMI should be the default.


For the NEMUS project haptic interface [], a modular approach was taken.

The device was split into three rpositorys, a central meta-repository
each element could very piossibly be swapped if another interface design was used, a separate firmware system created or a different sensor system employed. But there still a record of what the instrument was at the point with each component capable of being supplanted without being discarded and records lost.


\subsection{Open Methods}\label{sec:open-methods}

Addressing digital musical instrument conservation requires frameworks that
account for preservation, access, and reuse. Open Science
\cite{unesco_open_2021} provides a foundation by promoting the open sharing not
only of results%
\footnote{Examples include original research outputs, research data, software,
source code, workflows and protocols, and digital representations of pictorial
and graphical materials \cite{unesco_open_2021}.} but also of the processes
through which those results are obtained. Digital technologies make such
openness feasible, yet they also necessitate structure. The FAIR
principles---Findable, Accessible, Interoperable, Reusable---offer a practical
framework for managing digital assets \cite{wilkinson_fair_2016}:

\begin{itemize}
	\item \textbf{Findability:} digital assets should include rich metadata and
	      persistent identifiers.
	\item \textbf{Accessibility:} access protocols should be open, free, and
	      universally implementable.
	\item \textbf{Interoperability:} data and tools should integrate seamlessly
	      across heterogeneous systems with minimal effort.
	\item \textbf{Reusability:} assets should be released with clear, accessible
	      licensing and provenance.
\end{itemize}

For software, FAIR also implies citability \cite{soito_citations_2016}. This
requires coordinated action by authors \cite{smith_software_2016}, by those
citing software \cite{katz_recognizing_2021}, and by journals that must
cross-reference software artefacts \cite{stall_journal_2023}. Open software is
ideally ``living,'' yet research demands that specific versions remain
discoverable and stable. Version control systems (e.g., \texttt{git}) allow
releases to be tagged, while public repositories (e.g., GitHub) enhance
discoverability. For long-term reference, archival deposition (e.g., Zenodo)
provides persistent identifiers (DOIs) \cite{smith_software_2016,
stall_journal_2023}.

Persistence is one dimension of sustainability; reproducibility is the other
\cite{perkel_challenge_2020}. Software should remain functional in the future
despite changes in languages, libraries, and hardware---and despite more mundane
obstacles such as incomplete documentation \cite{robert_reproducibility_2020}.

\subsection{Reproducibility}\label{hardware-reproducibility}

Digitally designed `hardware' introduces additional challenges. In digital
musical instrument (DMI) design, long-term reuse remains difficult
\cite{fiordelmondo_towards_2025}. Hardware projects typically combine electronic
schematics, CAD/CAM assets, bills of materials, and assembly or operation
documentation; these components must be archived together within a
well-structured repository \cite{calegario_documentation_2021}. CAD formats and
toolchains themselves pose preservation risks. During the course of this thesis,
Autodesk announced the discontinuation of the EAGLE EDA tool
\cite{autodesk_eagle_2024}, effective July~2026. A deliberate decision was made
to continue using EAGLE’s XML-based format: much as the end-of-life of Python~2
``calcified'' that environment for archival purposes \cite{rougier_loupe_2020},
EAGLE’s stable format remains processable by other tools such as KiCad
\cite{kicad_eagle_2024}.

\textcite{perkel_challenge_2020} aggregates guidance from the ReScience~C
ten-year challenge on reviving decade-old research software. Its key
recommendations---version control, archival deposition, and explicit
documentation---align with broader best practices \cite{smith_software_2016,
stall_journal_2023}.

All digital assets associated with this thesis are released under the GPLv3
licence, following recommendations to grant permissions as openly as possible
\cite{stall_journal_2023}. GPLv3 permits copying, distribution, and
modification, with the stipulation that derivatives remain under the same
licence \cite{gplv3}. Repositories were structured in accordance with guidance
from the Software Sustainability Institute and were subsequently reviewed by the
Institute at the University of Edinburgh \cite{ssi_online_2025}.


##

## 2025 Audit

From the 96 papers

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

All of these _have_ repositories

| id          | paper              | State   | reason          | url                                                           | page | placement | context                                                    |
| ----------- | ------------------ | ------- | --------------- | ------------------------------------------------------------- | ---- | --------- | ---------------------------------------------------------- |
| nime2025_60 | Cicadas            | auth    |                 | http://gitea.offig.com/lfsadmin/Cicadas                       | 2    | body      | Full code for the generative algorithm is available at     |
| nime2025_79 | Drum Tao           | empty   |                 | https://red- x- silver.github.io/the- drum- machine- of- tao/ | 1    | footnote  | Results from a prototype are available for listening1      |
| nime2025_74 | Mindcube           | empty   | wrong repo      | https://github.com/mitmedialab/mindcube- rave                 | 3    | footnote  | An implementation of this mapping can be found on GitHub1. |
| nime2025_91 | glitchgate         | private |                 | https://github.com/ijc8/glitchgate                            | 1    | footnote  | The source code for glitchgate is available at             |
|             | Global drum circle | private | "unpublishable" | https://github.com/rbdannenberg/gdc                           |      |           |                                                            |
| nime2025_92 |                    | missing | extant          | https://github.com/ccrma/smuck                                |      |           |                                                            |