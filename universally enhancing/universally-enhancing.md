# Universally enhancing math on the web

##  Research Plan

Since its inception in 2008 MathJax has become the gold standard for rendering math on the web, greatly impacting the dissemination of mathematics and scientific content. Whether student or teacher, researcher or professional, start-up or established publisher, MathJax enables people to put mathematics on the web easily and flawlessly using TeX, AsciiMath or MathML markup. The MathJax CDN alone serves well over 100 million visitors per month and the latest release contains a number of advanced assistive technology features that make mathematics on the web accessible to everyone [2].

We propose research that will fundamentally improve this technology for mathematical content as well as extend and broaden its applicability, in particular to physics and chemistry on the web.


## Year 1: Refined semantic analysis

So far, our approach to semantic analysis was focused on pragmatically dealing with mathematics as found in the wild, no matter the original notation or its markup quality [4].

### Improved heuristics

First, we have already identified several approaches to enhancing our existing heuristics which we could not implement in our preceding work. In particular, the analysis of tabular structures such as equation arrays, matrices, and commutative diagrams poses an important and difficult area. Currently, our semantic analysis is limited to individual table cells rather than the much more complex task of analyzing the structure of the table, i.e., analyzing the relationship between the cells. To make progress here is especially important since most mathematics is still authored for print, and thus tabular layout is not just used as a natural part of the layout (as in the case of matrices) but also for tweaking (print) layout (e.g., line-breaking, arranging longer derivations of equations). Analyzing the table as a whole will allow us to provide more refined analysis of the parts. For example, identifying a table as an equation array allows us to provide more information about the relationship of its elements.

### Leveraging input formats

As a natural next step beyond heuristics, we want to leverage additional information whenever we can. Since MathJax is able to process a wide variety of input formats (converting everything to MathML internally), it is natural to leverage the information on the input side on a semantic level. For example, LaTeX or AsciiMath notation is often used for authoring and even if it is converted to MathML ahead of time (instead of on-the-fly using MathJax), most converters leave the original source embedded in the MathML. While not as well structured as MathML, these notational formats are often semantically richer. For example, where LaTeX users would choose a matrix or equation environment, both of these structures would be marked up as merely a table in MathML; the original markup can be used to distinguish the two uses.

This will also be a natural starting point for leveraging information from other scientific fields. For example, MathJax already provides several extensions for LaTeX input that are focused on particular subject areas, e.g., mhchem (chemistry), physics (physics), siunitx (international units) etc. Leveraging such information will allow us to improve our heuristics significantly.

## Year 2: Broadening the scope
### Leveraging contextual information

As a fundamentally new approach to our heuristics, we want to exploit whole-document information. Currently, our heuristics focus on individual equations; that is, single formulas are interpreted with respect to a default semantic [1,4]. This is naturally limiting as, on the one hand, the same expression can be interpreted differently depending on its position in a formula, and on the other hand, it can yield interpretations that are semantically incorrect in the context of a document. The problem is compounded by the fact that mathematical notation is often ambiguous. For example, “$(a,b)$” could describe a point in the Euclidean plane, a dot product in a Hilbert space, or an interval of the real line. Without deducing the right meaning, either from a previous interpretation of a similar formula or from the subject area of the document containing the formula, it is impossible to obtain the correct interpretation automatically.

We therefore will focus initially on using two types of contextual information in a document: other equations and non-equational context. For the former, we will try to homogenise the interpretation of mathematical expressions across an entire document. For the latter we want to extend our tools to allow for the use of context-specific heuristics. For example, a heuristic to detect BraKet notation is necessary in many areas of Physics, but can have negative effects in other contexts. Being able to “toggle” heuristics depending on the context will greatly increase the quality of the semantic enrichment, cf. [Figure 1]. Towards automation, we want to investigate leveraging information generated by tools for full-text natural-language processing exposed in documents as metadata. While a serious challenge, we believe contextual information would help us push the envelope of semantic information for mathematical fragments dramatically and we want to focus particularly on physics, theoretical computer science, and logic.

### Extended output options

To increase the impact of our work, we want to research how our currently highly dynamic tools for semantic enrichment and universal rendering [5] can be extended to provide additional output methods as well as options for less dynamic user environments. An example of a new output mechanism is tactile output (e.g., Braille), where various notational systems exist yet are significantly different from both visual and aural representation. Such outputs are not only important for universal rendering, but, as we experienced with aural rendering, are also critical for understanding semantic interpretations overall. The crucial use case for less dynamic environments are ebooks without JavaScript support, which require server-side pre-rendering of equations. We need to address the computational challenge to embed efficiently all information into expressions that MathJax normally re-computes dynamically on the fly.

This relates to MathJax’s mission to enable long-term improvement of the web platform, thinking beyond the scope of an individual tool like MathJax [3]. This research would directly connect with our efforts in the W3C where Peter Krautzberger and Volker Sorge are invited experts (Digital Publishing Interest Group, SVG accessibility task force, Math-on-web Community Group). We believe we are in an excellent position to feed the results of our research back into the standards process and let our results have the widest possible impact.

## Figure 1


<img src="./graphic.png" alt="Interpretations of the bra-ket notation under current and specialized heuristics, as semantic tree and derived voicing">

## References

1. Davide Cervone, Peter Krautzberger, and Volker Sorge. Employing semantic analysis for enhanced accessibility features in MathJax. In 13th IEEE Annual Consumer Communications & Networking Conference (CCNC 2016), volume 2, pages 1129-1134, Las Vegas, Nevada, USA, 2016. IEEE Computer Society Press.
2. Davide Cervone, Peter Krautzberger, and Volker Sorge. New accessibility features in MathJax. Journal on Technology & Persons with Disabilities, 4, 2016.
3. Davide Cervone, Peter Krautzberger, and Volker Sorge. Towards aria standards for mathematical markup. In The 3rd International Workshop on "Digitization and E-Inclusion in Mathematics and Science 2016" (DEIMS2016), pages 125-130, Shonan Village Center, Kanagawa, Japan, 2016.
4. Davide Cervone, Peter Krautzberger, and Volker Sorge. Towards meaningful visual abstraction of mathematical notation. In Proceedings of 10th Workshop on Mathematical User Interfaces, 2015.
5. Davide Cervone, Peter Krautzberger, and Volker Sorge. Towards universal rendering in MathJax. In Gregory R. Gay and Tiago Joao Guerreiro, editors, Proceedings of the 13th Web for All Conference, W4A'16, pages 4:1-4:4, Montreal, Canada, 2016. ACM.
