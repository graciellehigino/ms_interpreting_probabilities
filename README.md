# Introduction

Cataloging ecological interactions is a gargantuan task. Regardless of sampling
effort, there are practical and biological constraints that hinder our ability
to observe all interactions in nature, such as the spatial and temporal
uncoupling of species and the large number of potential interactions in a
community, of which the vast majority are rare [@Jordano2016Samplingb].
Documenting the location and timing of interactions becomes even more
challenging when accounting for the spatiotemporal variability of ecological
networks [@Poisot2012Dissimilaritya; @Poisot2015Speciesa]. Indeed, it is now
recognized that knowing the biological capacity of two species to interact is
necessary but not sufficient for inferring their interaction at a specific time
and space. For example, @Golubski2011ModMod presented many cases where trophic
interactions in food webs depend on the presence or abundance of a third species
(e.g., of a more profitable prey species). More generally, a handful of
conditions must be satisfied for an interaction to be observed locally. First,
both species must have overlapping geographic ranges, i.e. they must co-occur
within the region of interest [@Blanchet2020Cooccurrencea]. Then, they must
encounter locally. Probabilities of interspecific encounters are typically low,
especially for rare species with low relative abundances
[@Canard2012Emergencea]. Finally, their traits must be locally compatible
[@Poisot2015Speciesa]. This includes their phenology [@Olesen2010Missing;
@Singer2012GeoMos], behavioral choices [@Pulliam1974Theory; @Choh2012PreRol] and
phenotypes [Bolnick2011WhyInt; @Stouffer2011RolBod; Gravel2013InfFooa].
Environmental factors, such as temperature [@Angilletta2004TemGro], drought
[@Woodward2012CliCha], climate change [@Gilman2010FraCom; @Woodward2010ChaEco;
@Araujo2011Usinga], and habitat modifications [@Tylianakis2007HabMod],
contribute to this spatiotemporal variability of interactions by impacting
species abundance and traits. In this context, it is unsurprising that our
knowledge of ecological interactions remains limited [@Hortal2015SevSho] despite
extensive biodiversity data collection [@Schmeller2015GloTer].

The recognition of the intrinsic variability of species interactions has led
ecologists to expand their representation of ecological networks to include a
probabilistic view of interactions [@Poisot2016Structure]. As opposed to binary
deterministic networks, in which interactions are either observed or not,
probabilistic networks represent our degree of belief about the realization or
feasibility of pairwise interactions at the local or regional scale,
respectively. In other words, representing interactions probabilistically
considers inherent uncertainties and observation errors associated with
ecological data. In the broadest sense, binary networks are also a type of
probabilistic networks, in which the value of interactions is restrained to $0$
(non-observed) or $1$ (observed). In probabilistic networks, only forbidden
interactions [@Jordano2003Invarianta; @Olesen2010Missing] would have a
probability value of zero [but see @Gonzalez-Varo2016Labilea]. However,
*neutral* forbidden interactions [i.e., improbable interactions between rare
species, @Canard2012Emergencea] could have low probability values in a local
network but high probability in a regional network (metaweb) describing the
biological capacity of species to interact.

By accounting for the uncertainty of interactions, probabilistic networks
provide a more realistic portrait of species interactions and of their emerging
structure. This is important given that network structure is one of the major
drivers of the functioning, dynamics, and resilience of ecosystems worldwide
[@Proulx2005Networka; @McCann2007ProBio; @McCann2011FooWeb; @Rooney2012IntFoo].
Moreover, the application and development of computational methods in network
ecology, which are often based on a probabilistic representation of
interactions, can help alleviate the colossal sampling efforts required to
document species interactions [@Strydom2021Roadmapa]. For example, statistical
models can be used to estimate the uncertainty of pairwise interactions
[@Cirtwill2019QuaFra] and the probability of missing (false negatives) and
spurious (false positives) interactions [@Guimera2009MisSpu]. Considering the
high rate of false negatives in species interaction data due to the difficulty
of witnessing rare interactions [@Catchen2023Missinga], these models can inform
the identification of priority sampling locations of ecological networks [e.g.,
@Andrade-Pacheco2020Finding present an approach to identify priority sampling
locations of disease hotspots]. Statistical models can also be used to generate
network predictions without prior knowledge about their pairwise interactions,
for instance using body size [@Petchey2008SizFor; @Gravel2013InfFooa], phylogeny
[@Elmasri2020HieBay; @Strydom2022Food], or a combination of niche and neutral
processes [@Bartomeus2016ComFra; @Pomeranz2019InfPre] for inference. Topological
null models [e.g., @Bascompte2003NesAss; @Fortuna2006HabLos], which can be used
to generate underlying distributions of network measures for null hypothesis
significance testing, are other examples of common probabilistic network models.
Many measures have been developed to describe the structure
[@Poisot2016Structure] and diversity [@Ohlmann2019Diversity; @Godsoe2022Species]
of probabilistic networks. These models and measures support the use of this
approach for the study of a wide range of ecological questions, from making
better predictions of species distribution [@Cazelles2016Theorya] to forecasting
the impact of climate change on ecological networks [@Gilman2010FraCom].

Despite these advances and opportunities, the lack of clear guidelines on the
use of probabilistic interaction data is worrisome, especially for field and
computational ecologists who manipulate and generate these numbers. Indeed,
beyond methodological challenges encountered when evaluating them, there are
important and perhaps more fundamental conceptual challenges when it comes to
defining them. To the best of our knowledge, there is currently no data standard
that could guide the estimation and documentation of interaction probabilities
[@Salim2022Data discuss data standards for deterministic mutualistic networks].
General guidelines could support a more adequate integration and manipulation of
interaction data from different sources and prevent ecologists from being misled
by ambiguous and often diverging interpretations of probabilistic networks. In
this contribution, we aim to take a step back by outlining different ways in
which they were defined and used in network ecology and propose an approach to
thinking about them. We distinguish two broad categories of probabilistic
networks that have different statistical behaviors when applied to key
ecological questions: local networks of realized interactions and regional
networks (metawebs) of potential interactions. We show that these
representations have different ecological and statistical implications,
especially regarding the spatial and temporal scaling of interactions and the
prediction of binary networks across space. Although we focus on food webs, our
observations and advice can be applied to most types of ecological networks,
from plant-pollinator to host-parasite networks. Indeed, with the exception of
networks of indirect interactions such as competition and facilitation networks
[@Kefi2015NetStr; @Kefi2016HowStr], most ecological networks describe
probabilities of direct interactions, which are conceptually and mathematically
analogous to each other regardless of their biological type (e.g., trophic and
parasitic interactions). Overall, we argue that probabilistic networks should be
better documented, clearly defined in mathematical terms, and used with caution
when analyzing ecological interactions. 

# Probabilistic representations of ecological interactions

One of the first aspects to take into consideration when estimating or
interpreting probabilities of interactions is knowing if they describe potential
or realized interactions. A potential interaction is defined as the biological
capacity of two species to interact (i.e., the probability that they *can*
theoretically interact) whereas a realized interaction refers to the
materialization or observation of this interaction in a delineated space and
time period (i.e., the probability that they interact locally). Here, we use the
terms *metaweb* to designate networks of potential interactions and *local
networks* for those of realized interactions. Metawebs are the network analogue
of the species pool, where local networks originate from a subset of both
species (nodes) and interactions (edges) of the regional metaweb
[@Saravia2022Ecological]. Frequent confusion arises among ecologists over the
use of these two terms, especially in a probabilistic context. Indeed, it is
often unclear when authors describe potential or realized interactions in their
studies, or when so-called probabilities are actually *interaction scores*.
Likewise, probabilistic potential interactions are often used and interpreted as
realized interactions (and conversely), even when the type of interaction is
specified, which may generate misleading findings when analyzing these data. We
believe that a better understanding of the differences and relationships between
these probabilistic representations of ecological networks would alleviate
interpretation errors and help ecologists use these numbers more appropriately. 

## Pairwise interactions: the building blocks of ecological networks

Local ecological networks and metawebs, like any type of networks, are made of
nodes and edges that can be represented at different levels of organization and
precision. The basic unit of food webs and other ecological networks are
individuals that interact with each others (e.g., by predation,
@Elton2001Animal), forming individual-based networks. The aggregation of these
individuals into more or less homogeneous groups (e.g., populations, species,
trophic species, families) allows us to represent nodes at broader taxonomic
scales, which impacts our interpretation of the properties and behaviour of
these systems [@Guimaraes2020Structurea]. Moreover, edges linking these nodes
can describe a variety of interaction measures. Ecologists have traditionally
represented interactions as binary objects that were considered realized after
observing at least one individual from group $i$ interact with at least another
individual from group $j$. Boolean interactions are actually the result of a
Bernoulli process $A_{i,j} \sim {\rm Bernoulli}(p_{i,j})$, with $p_{i,j}$ being
the probability of interaction that characterizes our limited knowledge of
interactions and their intrinsic spatiotemporal variability. Depending on the
type of networks (local or metaweb), the mathematical formulation and
interpretation of stochastic parameters like $p_{i,j}$ are inextricably linked
to environmental and biological factors such as species relative abundance,
traits, area, and time (@tbl:prob). In this probabilistic network representation
in which $p_{i,j}$ are edge values, the only two possible outcomes are the
presence ($A_{i,j} = 1$) or absence ($A_{i,j} = 0$) of an interaction between
each pair of nodes. Observing an interaction between two taxa at a given
location and time provides important information that can be used to update
previous estimates of $p_{i,j}$, informing us on the biological capacity of both
taxa to interact and the environmental conditions that enable the realization of
their interaction in space and time. 

Even though binary networks constitute a highly valuable source of ecological
information [@Pascual2006Ecologicala], they overlook important factors regarding
interaction strengths. These are represented using quantitative interactions,
which better describe the energy flows, demographic impacts or frequencies of
interactions between nodes [@Berlow2004Interaction; @Borrett2019Walk], with
$A_{i,j}$ being a natural number $\mathbb{N}$ or a real number $\mathbb{R}$
depending on the measure. For example, they can represent the average number of
prey individuals consumed by a predator in a given time period (e.g., the
average number of fish in the stomach of a piscivorous species). Because
quantitative interactions can describe predation pressure on prey taxa, they can
be good estimators of the parameters describing species interactions in a
Lotka-Volterra model [e.g., @Emmerson2004Predatora]. However, this extra amount
of ecological information typically comes at a cost of greater sampling effort
or data requirement in predictive models [@Strydom2021Roadmapa], which can lead
to relatively high levels of uncertainties when inferring quantitative networks
with limited data. Just like binary networks, the uncertainty and spatiotemporal
variability of quantitative interactions can be represented probabilistically.
However, quantitative interactions can follow various probability distributions
depending on the measure used, with the event's outcome being the value of
interaction strength. For instance, quantitative interactions can be distributed
as a Poisson distribution $A_{i,j} \sim {\rm Poisson}(\lambda_{i,j})$ when
predicting frequencies of interactions between pairs of nodes, with
$\lambda_{i,j}$ being the expected rate at which individuals of taxa $i$ and $j$
interact (e.g., the average number of prey $j$ consumed per unit time by all
predators $i$). The Poisson distribution can also be 0-inflated when considering
non-interacting taxa, which constitute the majority of taxa pairs in most local
networks due to their typically high sparseness [@Jordano2016Samplingb]. Because
of the methodological difficulties typically encountered when building
deterministic quantitative networks, they have been little used in ecology. As a
result, binary interactions, which are more easy to sample, are much more
documented and modelled in the literature. Moreover, most published
probabilistic networks and methods describe Bernoulli interactions (@tbl:prob),
which emphasizes the need for better guidelines regarding their interpretation
and manipulation. For these reasons, our primary focus in this contribution will
be on addressing the challenges in estimating and using the probability that two
taxa interact locally or that they *can* biologically interact.

## Local networks: communities interacting in space and time

As opposed to metawebs, probabilistic local food webs represent the likelihood
that two species will interact at a specific location and within a given time
period; in other words, they are context dependant. They could also represent
the likelihood of observing these interactions within a given area and time. To
be specific, space is defined here as the geographic coordinates $(x, y)$ of the
spatial boundaries delineating the system, whereas time is the time interval $t$
during which interactions were sampled or for which they were predicted. We want
to point out that they are not single values, but rather continued dimensions
that could be outlined differently depending on the study system. Regardless of
how they were defined, they always delineate a specific area $A$ and duration
$t$. These could refer to the sampled area and duration or to the targeted
location and time period.  

Many factors could be taken into consideration when estimating the probability
that a predator species $i$ interacts with a given prey species $j$ locally. One
of the most important is species co-occurrence $C$, which is a Boolean
describing if both species can be found at location and time ($x$, $y$, $t$).
Surely, the probability that the interaction is realized must be $0$ when
species do not co-occur ($C = 0$). Interaction probabilities can also be
conditional on other biological and environmental variables, such as
temperature, precipitation, presence of shelters, phenotypic plasticity,
phenology, and presence of other interacting species in the network. These
conditions can affect species traits, which greatly impact the capacity of
species to interact [@Poisot2015Speciesa]. Similarly, species relative abundance
is another important predictor of the probability of interaction, because it
impacts the probability that species will randomly encounter
[@Canard2012Emergencea; @Canard2014Empiricala; @Poisot2015Speciesa]. Here, we
will use the variable $\Omega$ as a substitute for the biological and ecological
context in which interaction probabilities were estimated, including the
presence of higher-order interactions. This gives us the following equation for
the probability of realized interaction between species (or taxa) $i$ and $j$ in
a local network $N$:

$$P_{N}(i \rightarrow j | A, t, C, \Omega),$$
{#eq:local}

which can be read as the probability of local interaction between the two
species in an area $A$ and time interval $t$, given their co-occurrence $C$ and
specific environmental and biological conditions $\Omega$. These conditions do
not systematically need to be specified for all studies. However, when they are,
they should be made explicit in the metadada. 

Multiple difficulties of interpretation arise when the conditions are not
clearly specified, which we found is often the case in the literature. For
example, if $P_{N}(i \rightarrow j | C = 1)$ represents the probability that two
co-occurring species interact (i.e., the edge's probability value), $P_{N}(i
\rightarrow j)$ denotes instead the probability of interaction without knowing
if they co-occur (i.e., the product of the nodes and edge's probability values).
For practical reasons, probabilistic ecological networks are generally
represented as matrices of probabilities (i.e., matrices of edges without node
values), whose elements are thus hard to interpret without clear indications
about $C$. Overall, when probabilities of interactions are estimated using
specific values of $A$, $t$, $C$, and $\Omega$, ecologists should make them
explicit in their metadata, preferably using mathematical equations to avoid any
ambiguity. Below, we will see examples of why this matters when it comes to
spatial, temporal, and taxonomic scaling of biotic interactions.

Table: Articles using probabilistic interactions and the
definitions and variables they considered. {#tbl:prob}

Quantitative interactions can be converted to probabilistic interactions by normalizing. 

## Metawebs: regional catalogs of interactions

Metawebs are networks of potential interactions, representing the probability
that two taxa can interact regardless of biological plasticity, environmental
variability or co-occurrence. Instead of describing stochastic biological
processes occurring in nature, probabilistic potential interactions can be
thought of as a measure of imperfect knowledge about the capacity of two taxa to
interact. For this reason, they have been initially designed for broad spatial,
temporal, and taxonomic scales (e.g, species food webs at the continental
scale). 

We can express the probability that two taxa $i$ and $j$ can interact in a
metaweb $M$ as 

$$P_{M}(i \rightarrow j),$$ {#eq:metaweb}

which is context independent. In other words, the probability that two species
can interact is not contingent on location, time, and environmental factors.
Nevertheless, one aspect of a metaweb that could be conditional on these factors
is the list of species (or taxa) it is built from when assembled for a specific
region.

Starting from a selected set of species, metawebs can be built using different
data sources, including literature review, field work, and predictive models
[e.g., the metaweb of Canadian mammals inferred by @Strydom2022Food]. Every pair
of species that has been observed to interact at least once can be given a
probability of interaction of $1$; we know that they *can* interact. This means
that rare interactions can technically be given high probabilities in the
metaweb. Unobserved interactions, on the other hand, are given lower
probabilities, going as low as $0$ for forbidden links. Two important nuances
must however be made here. Because of observation errors due to taxonomic
misidentifications and ecological misinterpretations [e.g., due to cryptic
species and interactions; @Pringle2020Resolving], many observations of
interactions are actually false positives. Similarly, forbidden interactions can
be false negatives if e.g. they have been assessed for specific phenotypes,
locations or time. Implementing a Bayesian framework, which updates prior
probabilities of interactions with empirical data, could lessen these errors.

# Statistical behaviour of networks in key ecological applications

## Taxonomic agglomeration and division of nodes

The properties of ecological networks depend on their level of organization
[@Guimaraes2020Structurea]. Indeed, at different taxonomic scales, different
behaviours and dynamics can be observed and distinct ecological questions can be
answered (e.g., exploring evolutionary dynamics at broad taxonomic scales).
Because of these reasons, it could be important to analyse the same network at
different taxonomic scales. However, we want to emphasize here that many
networks do not have an homogenous level of organisation
[@VazquezSS2022Ecological]. Indeed, different nodes within the same network can
be represented at different taxonomic scales (e.g., a network composed of
species and trophic species). This becomes important when we consider that the
biological interpretation of interaction probabilities depends on the nodes'
resolution. For example, in individual-based networks, the probability that two
individuals interact could represent the degree of belief that one will actually
consume the other. In species-based networks, the probability that two species
interact could rather represent the degree of belief that *at least* one
individual from the predator species will eat *at least* another individual from
the prey species. This distinction in interpretation impacts the way probability
values change with taxonomic scale. 

There are a lot of similarities between taxonomic and spatiotemporal scaling of
probabilistic interactions. Fundamentally, these types of scaling are just
different ways to aggregate individuals into broader nodes, either spatially,
temporally, or taxonomically. However, there are also important differences
between them. First, in metawebs, if we know that two species have the capacity
to interact, we can infer that their respective genus should also be able to
interact (i.e., there should be at least two individuals within these genus that
can interact). On the contrary, knowing that two genus can interact does not
mean that all pairwise combinations of species within these genus can also
interact among themselves. This observation also applies to local networks. When
it comes to probabilistic networks, interaction probabilities at broader
taxonomic scales can be directly obtained from probabilities at finer scales
when aggregating nodes. For example, if we have in a network $n_A$ species from
genus $A$ and $n_B$ species from genus $B$, we can calculate the probability
that the two genus interact as $P_N(A \rightarrow B) = 1 - \prod_{i =
1}^{n_A}\prod_{j = 1}^{n_B}(1 - P_N(A_i \rightarrow B_j))$, where $A_i$ and
$B_j$ are the species of the corresponding genus. However, more sophisticated
models need to be used when building probabilistic networks at smaller taxonomic
resolutions (e.g., when building a species-level network from a genus-level
network). One could, for example, estimate the probabilities of all pairwise
species interactions by using a Beta distribution parametrised by the
broader-scale network.

[Figure 3 about here]. Conceptual figure of how a scale up of the nodes from an
individual to a population to any higher taxonomic group change our
interpretation of the probability of interaction.

## Spatial and temporal scaling of probabilistic interactions

Metawebs and local networks intrinsically differ in their relation to scale. On
one hand, as mentioned above, probabilistic metawebs are context independent,
i.e., probabilistic pairwise interactions do not scale with space and time
because they depend solely on the biological capacity of the two taxa to
interact. This implies that the estimated likelihood that two species can
potentially interact should be the same among all metawebs in which they are
present. In practice, this is rarely the case because ecologists use different
methods and data to estimate these probabilities of interactions (e.g.,
different sampling area and time period). However, in the case where local
metawebs $M_{x,y}$ are subsampled from their regional counterpart $M_0$, we
should expect edge values to be identical among all networks, regardless of
their spatial scale, i.e. $P_{M_{x,y}}(i \rightarrow j) = P_{M_0}(i \rightarrow
j)$. On the other hand, local probabilistic networks are indissociable from
their spatial and temporal contexts because there are more opportunities of
interactions (e.g., more individuals, more trait variations, more chance of
encounter) in a larger area and longer time period [@McLeod2020EffSpe]. Let
$N_0$ be a local probabilistic food web delineated in an area $A_0$ and $N_1$ a
network of area $A_1 < A_0$ within $A_0$. We should expect the probability that
$i$ and $j$ interacts to scale spatially, i.e. $P_{N_1}(i \rightarrow j | A <
A_0) \le P_{N_0}(i \rightarrow j | A = A_0)$. Similarly, the temporal scaling of
probabilistic local food webs could be manifested through the effect of sampling
effort on the observation of interactions [@Jordano2016Samplingb;
@McLeod2021Sampling] or of time itself on their realization
[@Poisot2012Dissimilaritya]. There are many network-area relationships [e.g.,
@Wood2015Effects; @Galiana2018Spatiala] and interaction accumulation curves
[e.g, @Jordano2016Samplingb] explored in the literature. These could inspire the
development and testing of different equations describing the spatiotemporal
scaling of probabilistic pairwise interactions in local networks, which are over
the scope of this manuscript. 

[Figure 2 about here]. Conceptual figure showing (1) the spatiotemporal scaling
of probabilistic metawebs and local food webs and (2) the spatial sampling of
metawebs and local food webs into Boolean networks. 

## Spatiotemporally explicit model of probabilistic interactions

The variability of species interactions spurred the development of methods
aiming at predicting ecological networks at fine spatial and temporal scales.
For example, @Bohan2017Nextgenerationa proposed a framework to reconstruct
networks in real time using continuous biomonitoring. Here, we will build on
these studies by proposing a simple model to make probabilistic local networks
spatiotemporally explicit. These types of models could prove useful when
inferring food webs across time and space from sparse data. However, they are
not suitable for metawebs, which are static objects.

One way that probabilistic food webs can be made spatiotemporally explicit is by
modelling interactions between co-occurring species as a Poisson process with
rate $\lambda$. Specifically, if the total observation time for a location is
$t_0$, the probability that two co-occurring species $i$ and $j$ will interact
during this time period is $P_N(i \rightarrow j | C_{i,j} = 1, t = t_0) =
1-e^{-\lambda t_0}$, which approaches $1$ when $t \to \infty$. The value of the
parameter $\lambda$ could be estimated using prior data on interaction
strengths, if available. Additionally, we can estimate the probability of
co-occurrence at location $(x,y)$ with $P_{x,y}(C_{i,j} = 1) = P_{x,y}(i)
P_{x,y}(j)\gamma$, where $P_{x,y}(i)$ and $P_{x,y}(j)$ are respectively the
probabilities of occurrence of species $i$ and $j$ and $\gamma$ is the strength
of association between occurrence and co-occurrence, as defined in
@Cazelles2016Theorya. Note that in empirical networks, $\gamma$ is typically $>
1$ [@Catchen2023Missinga]. The observation of this interaction would thus follow
a Bernoulli distribution with parameter $p =
p_A(x,y)p_B(x,y)\gamma(1-e^{-\lambda t_0})$. This simple model could be
customized in many ways, e.g. by linking $\lambda$ with given environmental
variables or by adding in observation errors (i.e., probability of false
negatives and false positives; @Catchen2023Missinga).

## Binary conversion of probabilistic networks through random draws

Another conceptual challenge encountered when using probabilistic food webs is
the prediction of Boolean networks across space. Lets take $n \times n$ grid
cells each representing a probabilistic food web. If they contain potential
interactions, a single random trial must be conducted for each pairwise
interaction across the region (i.e., we should have only one random realization
of the regional metaweb). On the contrary, if they represent probabilities of
realized interactions, each food web must be independently sampled (i.e., $n^2$
independent random draws). This has direct implications on the spatial scaling
of interactions. For example, let $N_1$ and $N_2$ be networks of area $< A_0$
within a bigger area $A_0$ and disjoint from each other, such as $N_1$ and $N_2$
form $N_0$ (think of two contiguous cells that together delineate $N_0$). All
other things being equal, we should expect the probability that $i$ and $j$
interacts in $A_0$ to be $P_{N_0}(i \rightarrow j) = 1 - (1 - P_{N_1}(i
\rightarrow j)) \times (1 - P_{N_2}(i \rightarrow j))$ if $N_1$ and $N_2$ are
independently sampled. This also implies that we should expect interactions to
be realized in a certain number of local networks depending on the probability
value, which is not the case with metawebs. Note that spatial auto-correlation
and the concept of meta-network (i.e., networks of networks) could invalidate
the statistical assumption of independence. Nevertheless, the fundamental
difference in sampling metawebs and local networks stands even when considering
these factors. This difference in sampling further sheds light on the importance
of clearly defining interaction probabilities. What we consider as a *Bernoulli
trial*, when randomly drawing deterministic networks from probabilistic food
webs, depends on our biological interpretation of these probabilities. 

## Prediction of local networks from probabilistic metawebs

Even though the spatiotemporal variability of interactions is not considered in
metawebs, they can still be useful to reconstruct local networks of realized
interactions. Indeed, local networks are formed from subsets of their metaweb
(called subnetworks), which are obtained by selecting a subset of both species
and interactions [@Dunne2006Network]. Because a community's composition is
arguably easier to sample (or predict) than its interactions, the biggest
challenge is to sample links from the metaweb. This becomes a conceptual issue
when we consider how potential and realized interactions differ. Despite these
concerns, metawebs remain an important source of ecological information that can
be leveraged for realistically predicting spatially explicit networks. First,
metawebs set the upper limit of species interactions [@McLeod2021Sampling], i.e.
the probability that two species interact at a specific location is always lower
or equal to the probability of their potential interaction: 

$$P_{N}(i \rightarrow j | A, t, C, \Omega) \le
P_M(i \rightarrow j).$$ {#eq:switch}

Therefore, inferring local networks from their metaweb keeping the same values
of interaction probability would generate systematic biases in the prediction.
In that case, these networks would instead be called *spatially explicit* or
*local* metawebs (i.e., smaller-scale networks of potential interactions).
Second, the structure of local networks is constrained by the one of their
metaweb [@Saravia2022Ecological]. This suggests that a metaweb not only
constrains the pairwise interactions of its corresponding local networks, but
also their emerging properties. Inferring the structure of local networks from
the metaweb could thus help estimate more realistically the likelihood that
potential interactions are realized and observed locally [@Strydom2021Roadmapa]. 

[Figure 1 about here]. Empirical example of the association between the number
of interactions in realized local food webs and the number of interactions in
the corresponding subnetworks of their regional metaweb. We should expect the
association to be linear below the 1:1 line, illustrating @eq:switch.

# Conclusion

The emergence of probabilistic thinking in network ecology has paved the way to
a better assessment of the spatiotemporal variability and uncertainty of biotic
interactions. However, measuring probabilities empirically can be strenuous
given the difficulties of deciphering species and interactions
[@Pringle2020Resolving]. In this context, the development of computational
methods makes it possible to estimate interaction probabilities at large scales,
which in turn can pinpoint where we should go to optimise our sampling effort
for better resolving local food webs.

In this contribution, we showed that network metadata are perhaps as important
as interaction data themselves when it comes to interpreting probabilistic food
webs in ecological terms. First, the type of probabilistic interaction
(potential or realized) impacts the importance of scale, with interactions in
metawebs being scale independent, both spatially and temporally. Second, the
conditions in which local networks were estimated (e.g., area, time, biological
and environmental factors) and the attributes of the interacting species that
were considered (e.g., species co-occurrence) are essential contextual factors
that impact the mathematical representation of probabilities and their resulting
behaviour. Third, the biological interpretation of probabilities changes with
the level of organization of the network due to the aggregation of individuals
into broader groups. All these information should be available as clear metadata
so that ecologists can use probabilistic network data appropriately. 

Moreover, many statistical models in ecology that yield accurate predictions of
biotic interactions are black boxes difficult to interpret. Ecologists should be
careful before using the output of these models as probabilistic objects, since
there is often a thin line between a real probability and a non-probabilistic
predictive number (or score). Probabilities are numbers between $0$ and $1$ that
sum to $1$ and either represent the expected frequency of a phenomenon or the
degree of belief that it will be realized. Non-probabilistic scores, which are
more akin to interaction strengths, have different mathematical properties,
which impacts how we should handle these numbers in a spatially or temporally
explicit context. Therefore, researchers should use their expertise to assess if
their interaction data are actually probabilities or scores. This should also be
added to the metadata before sharing them, as well as the methods used to build
the networks. 

Better metadata documentation would allow researchers to use and manipulate
probabilistic ecological interactions according to how they were actually
defined and obtained. This would support better scientific practices, in
particular when these data are used for ecological prediction and forecasting.
For instance, we showed that building a rigorous workflow to predict local
networks from a probabilistic metaweb requires a good understanding of the data
at hand. Similarly, explicitly stating the context in which probabilistic data
were estimated would help using forecasting food-web models more rigorously
under specific climate change and habitat use scenarios. Regardless of the
method and application, fostering a better foundation for probabilistic
reasonings in network ecology, from the very nature of probabilities and biotic
interactions, is essential. 

# Acknowledgement

We acknowledge that this study was conducted on land within the traditional
unceded territory of the Saint Lawrence Iroquoian, Anishinabewaki, Mohawk,
Huron-Wendat, and Omàmiwininiwak nations. This work was supported by the
Institute for Data Valorisation (IVADO) and the Natural Sciences and Engineering
Research Council of Canada (NSERC) Collaborative Research and Training
Experience (CREATE) program, through the Computational Biodiversity Science and
Services (BIOS²) program. A special thank to all members of the Black Holes and
Revelations working group (organized by BIOS²) for their insightful discussions
and valuable feedback on this manuscript.

# References
