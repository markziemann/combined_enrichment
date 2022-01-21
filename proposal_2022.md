# Proposal: Should functional enrichment analysis be conducted irrespective of gene fold change direction?

Lead Investigator: TBA

Supervisor: Mark Ziemann

## Background

Gene set enrichment analyses are a widely used and powerful class of analytical tools for summarising omics data [1](Khatri et al, 2012).
There are two main classes of enrichment analysis, these are functional class scoring (FCS) and over-representation analysis (ORA), which are both in common use.
Despite the power of these tools, when performed improperly it can lead to biases and incorrect conclusions [2](Timmons et al, 2015).
One issue that has been raised is that some investigators consider the up- and down-regulated genes to be considered separately in ORA, 
while others perform ORA irrespective of the fold change direction.

In 2014, Hong et al [3] described that genes of the same pathway tend to be strongly correlated with one another, and so those gene sets will more
sensitivey detected as differentially regulated if the direction was considered in the enrichment analysis.
Therefore they suggest that ORA is better performed with separate ORA tests as compared to combined.
Despite this guidance, it appears that combined analysis is performed twice as often as separate analysis [4] (see Fig 3K).

Clearly there is a rift between the performance of methods and what researchers actually do.
This phenomenon was observed by Xie et al [5], which could be explained by first-mover advantage and ease of use.
Xie et al also discuss that popularity and performance are not associated because there are is not a well established set of performance criteria,
and there is some discordance in the community about the validity of benchmarks using real data or simulations.

Regarding the question of separate versus combined gene lists, there are other explanations.
There is a popular view in the molecular biology and genomics community that ORA should always be conducted combining up- and down-regulated genes as 
pathways consist of negative and positive regulators.
For example take this anonymous reviewer's comment we received about our draft [4]:

> There is one main and easy to solve flaw in their article and that pertains to an argument about combining or otherwise up and down-regulated genes.
> There is no logic or rule for this and in biological pathways combining is completely acceptable, as you can have both positive and negative regulators in
> a list from one pathway, differentially expressed in the opposite direction. 
> Thus the interpretation of the statistical work by Hong G et al 2014 is wrong – unsurprisingly as they understand little biology based on a reading of their article. 
> Thus an up-regulation of a positive actor or down-regulated of a negative actor – in the same pathway - can equate to the same biochemical outcome.
> Splitting lists also actually leads to two other problem.
> First is that with some technologies detecting down-regulation is more difficult (signal related) and second is that related to gene list size.
> Its well appreciated that small lists, especially if enrichment ratios + pvalues, and/or boot strapping are considered, are not sensitively profiled.
> Splitting a biologically relevant list into up and down impacts on this issue in an unpredictable manner, depending on gene list size and content.
> This particular section needs re-written or deleted as its wrong. Your results – see below – actually stumble on this issue.

In this proposed project, we will be further examining the basis for separated or combined enrichment analysis, and hopefully come to a consensus on this question 
based on data and simulations which addresses the concerns of those on both sides of this debate.

## Aims:

1. Using seven real gene expression data sets we have on hand, we will compare the results obtained with ORA using combined and separate lists.

2. These analyses will be performed with FCS as well, using the standard direction informed analysis as well as the direction agnostic method.
This will enable us to determine whether there is any benefit of using ORA.

3. We will quantify the number of pathways that demonstrate the "mixed" regulation pattern as discussed by the reviewer.
We will compare those pathways to the expected physiology of the system and speculate on their biological relevance.

4. Conduct a simulation study where we alter gene sets with "mixed" and "directional" patterns in accordance with (3).
We then run ORA and FCS benchmarks to calculate the accuracy of both algorithms with "separate", "combined" and "both" profiles.

5. Based on the data from (4) we will formulate some recommendations on whether "separate" or "combined" analysis is better, 
or perhaps it is necessary to perform both types of enrichment analysis to have a fuller picture of pathways dysregulated.
We can also make some recommendations on whether ORA or FCS gives better performance overall.

## Research methods

The gene expression datasets we will use are shown in the table below:

| Dataset | SRA accesion | genes in annotation set | genes detected | genes differentially expressed | Ref |
| :---: | :---: | :---: | :---: | :---: | :--: |
| 1. | SRP128998 | 39297 | 15635 | 3472 | 6 |
| 2. | SRP038101 | 39297 | 13926 | 3589 | 7 |
| 3. | SRP096178 | 39297 | 15477 | 9488 | 8 |
| 4. | SRP038101 | 39297 | 15607 | 5150 | 9 |
| 5. | SRP247621 | 39297 | 14288 | 230 | 10 |
| 6. | SRP253951 | 39297 | 15182 | 8588 | 11 |
| 7. | SRP068733 | 39297 | 14255 | 7365 | 12 |

We have already got scripts to perform differential expression analysis of these with DESeq2 [13].
From those differential profiles, we will conduct ORA with clusterprofiler [14] using separated and combined approaches.
FCS will also be conducted using the mitch package [15] using the standard direction informed apprach which is analogous to the "separate" ORA approach,
as well as the direction agnostic approch which is similar to the "combined" approach.

The gene sets we will use will most likely be Reactome [16].

The simulation study will be similar to one we previously conducted - shown in [15] Figures 7.

This analysis will be conducted entirely using R/Rstudio using Rmarkdown script on our cloud bioinformatics server.
All code will be maintained in a public github repository.
The entire study will be reproducible.
This means an interested reader will be able to download the code and completely replicate this analysis using a single command.

Rmarkdown will be used to draft the manuscript, using images and data that are dynamically generated.
The manuscript will describe all necessary details regarding the methods such as the type of input gene sets and when they were downloaded,
the version of softwares used and the basis for deciding upon methods used.

## Expected results and significance

Our previous work identified that methodological problems and lack of detail were extremely common in published articles.
During that study we noticed that it was very common for ORA to be conducted combining up and downregulated genes.
We thought this was odd and described it in a draft manuscript [4], although a reviewer didn't agree with our view.
This, together with conversations with other bioinformaticians and molecular biologists indicates that there are two different views regarding ORA.
We decided not to address the "separate/combined" issue in that article, by omitting those analyses in a subsequent version.
This raises the possibility of addressing this question in a new project.
Our hope is to resolve this rift using solid evidence and data.
We are also open to the possibility that both types of analysis are required to get a full picture of dysregulated pathways.

Our draft manuscript [4] also indicates that there are more severe problems occurring with regard to enrichment analysis which indicates
that overall, adequate statistical and bioinformatics training is lacking, and that current guides for enrichment analysis are failing.
There is a need for an authoritative document to outline best practices in enrichment analysis that is designed for novice bioinformaticians.

However these recommendations can only be endorsed by the community if they are supported by the data.
This study will help to resolve the controversy around the "separate/combined" question and put us one step further toward our goal of a definitive
set of best practices for enrichment analysis.
Such a set of best practices will be referred to by researchers and reviewers and will help raise the standard of published enrichment analysis.
This is an important goal because shoddy research undermines public confidence in the scientific enterprise.

## Timeline

Coding and analysis: Feb 2022 - May 2022

Article write-up : Jun - July 2022

## Logistics

Lead investigator has already conducted a pilot study and can share scripts used.
It is the student’s responsibility to be up to speed on the background information on enrichment analysis, general R/Rstudio coding and using version control with git.

Target Journal: PLoS One, F1000 Research

## Future directions

To develop a set of best practices which can be referred to by researchers and peer-reviewers.

## References

1. Khatri P, Sirota M, Butte AJ. Ten years of pathway analysis: current approaches and outstanding challenges. PLoS Comput Biol. 2012;8(2):e1002375. doi:10.1371/journal.pcbi.1002375

2. Timmons JA, Szkop KJ, Gallagher IJ. Multiple sources of bias confound functional enrichment analysis of global -omics data. Genome Biol. 2015;16(1):186. Published 2015 Sep 7. doi:10.1186/s13059-015-0761-7

3. Hong G, Zhang W, Li H, Shen X, Guo Z. Separate enrichment analysis of pathways for up- and downregulated genes. J R Soc Interface. 2013 Dec 18;11(92):20130950. doi: 10.1098/rsif.2013.0950.

4. Wijesooriya K, Jadaan SA, Perera KL, Kaur T, Ziemann M. Guidelines for reliable and reproducible functional enrichment analysis. bioRxiv 2021.09.06.459114; doi: https://doi.org/10.1101/2021.09.06.459114

5. Xie C, Jauhari S, Mora A. Popularity and performance of bioinformatics software: the case of gene set analysis. BMC Bioinformatics. 2021 Apr 15;22(1):191. doi: 10.1186/s12859-021-04124-5.

6. Felisbino MB, Ziemann M, Khurana I, Okabe J, Al-Hasani K, Maxwell S, et al. Valproic acid influences the expression of genes implicated with hyperglycaemia-induced complement and coagulation pathways. Sci Rep. 2021;11: 2163.

7. Lund K, Cole JJ, VanderKraats ND, McBryan T, Pchelintsev NA, Clark W, et al. DNMT inhibitors reverse a specific signature of aberrant promoter DNA methylation and associated gene silen>

8. Rafehi H, Balcerczyk A, Lunke S, Kaspi A, Ziemann M, Kn H, et al. Vascular histone deacetylation by pharmacological HDAC inhibition. Genome Res. 2014;24: 1271–1284.

9. Keating ST, Ziemann M, Okabe J, Khan AW, Balcerczyk A, El-Osta A. Deep sequencing reveals novel Set7 networks. Cell Mol Life Sci. 2014;71: 4471–486.

10. Lopez Sanchez MIG, Van Bergen NJ, Kearns LS, Ziemann M, Liang H, Hewitt AW, et al. OXPHOS bioenergetic compensation does not explain disease penetrance in Leber hereditary optic neurop>

11. Blanco-Melo D, Nilsson-Payant BE, Liu WC, Uhl S, Hoagland D, Møller R, et al. Imbalanced Host Response to SARS-CoV-2 Drives Development of COVID-19. Cell. 2020;181: 1036–1045.e9.

12. Rafehi H, Kaspi A, Ziemann M, Okabe J, Karagiannis TC, El-Osta A. Systems approach to the pharmacological actions of HDAC inhibitors reveals EP300 activities and convergent mechanisms >

13. Love MI, Huber W, Anders S. Moderated estimation of fold change and dispersion for RNA-seq data with DESeq2. Genome Biol. 2014;15: 550.

14. Yu G, Wang L-G, Han Y, He Q-Y. clusterProfiler: an R package for comparing biological themes among gene clusters. OMICS. 2012;16: 284–287.

15. Kaspi A, Ziemann M. mitch: multi-contrast pathway enrichment for multi-omics and single-cell profiling data. BMC Genomics. 2020 Jun 29;21(1):447. doi: 10.1186/s12864-020-06856-9.

16. Jassal B, Matthews L, Viteri G, Gong C, Lorente P, Fabregat A, et al. The reactome pathway knowledgebase. Nucleic Acids Res. 2020;48: D498–D503.

