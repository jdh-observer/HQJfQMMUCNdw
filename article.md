---
jupyter:
  jupytext:
    formats: ipynb,md
    text_representation:
      extension: .md
      format_name: markdown
      format_version: '1.3'
      jupytext_version: 1.19.1
  kernelspec:
    display_name: Python 3 (ipykernel)
    language: python
    name: python3
---

```python
#!pip install -r ohtm_pipeline/requirements.txt
#!pip install -r requirements.txt
!pip install -e ohtm_pipeline
```

```python editable=true slideshow={"slide_type": ""}
from ohtm_pipeline.ohtm_pipeline.basic_functions.save_load import load_json_function
import matplotlib.pyplot as plt
import plotly.express as px
import pandas as pd
import pickle
```

<!-- #region editable=true slideshow={"slide_type": ""} tags=["title"] -->
# Topic Modeling “Beheimatung”
## With an oral history topic modeling pipeline (OHTM)

<!-- #endregion -->

<!-- #region editable=true slideshow={"slide_type": ""} tags=["contributor"] -->
 ### Philipp  Bayerschmidt [![orcid](https://orcid.org/sites/default/files/images/orcid_16x16.png)](https://orcid.org/0009-0002-2743-2455) 
Institution
<!-- #endregion -->

<!-- #region tags=["copyright"] -->
[![cc-by](https://licensebuttons.net/l/by/4.0/88x31.png)](https://creativecommons.org/licenses/by/4.0/) 
©<AUTHOR or ORGANIZATION / FUNDER>. Published by De Gruyter in cooperation with the University of Luxembourg Centre for Contemporary and Digital History. This is an Open Access article distributed under the terms of the [Creative Commons Attribution License CC-BY](https://creativecommons.org/licenses/by/4.0/)

<!-- #endregion -->

<!-- #region tags=["copyright"] -->
[![cc-by-nc-nd](https://licensebuttons.net/l/by-nc-nd/4.0/88x31.png)](https://creativecommons.org/licenses/by-nc-nd/4.0/) 
©<AUTHOR or ORGANIZATION / FUNDER>. Published by De Gruyter in cooperation with the University of Luxembourg Centre for Contemporary and Digital History. This is an Open Access article distributed under the terms of the [Creative Commons Attribution License CC-BY-NC-ND](https://creativecommons.org/licenses/by-nc-nd/4.0/)

<!-- #endregion -->

<!-- #region editable=true slideshow={"slide_type": ""} tags=["abstract"] -->
This is an abstract (...)
<!-- #endregion -->

<!-- #region citation-manager={"citations": {"0ixik": [{"id": "20217732/74QRKYPZ", "source": "zotero"}], "11p8r": [{"id": "20217732/GYVTICFJ", "source": "zotero"}], "35qmk": [{"id": "20217732/GFCUEUX2", "source": "zotero"}], "3j5oe": [{"id": "20217732/NQPGZC6Z", "source": "zotero"}], "8ep5t": [{"id": "20217732/LFIR4DFN", "source": "zotero"}], "a443a": [{"id": "20217732/JDH35IVA", "source": "zotero"}], "d0i4k": [{"id": "20217732/SMT6TLS8", "source": "zotero"}], "dwkif": [{"id": "20217732/72D4T9FI", "source": "zotero"}], "ez9yq": [{"id": "20217732/NGJ3HCW2", "source": "zotero"}], "f9w99": [{"id": "20217732/L7LCZ2SY", "source": "zotero"}], "gegzb": [{"id": "20217732/MYVQS8JW", "source": "zotero"}], "h9s94": [{"id": "20217732/PWDTM7BC", "source": "zotero"}], "j5lhv": [{"id": "20217732/MYVQS8JW", "source": "zotero"}], "krfwq": [{"id": "20217732/GFCUEUX2", "source": "zotero"}], "m05jq": [{"id": "20217732/AV3J3ICJ", "source": "zotero"}], "n2hul": [{"id": "20217732/GFCUEUX2", "source": "zotero"}], "qgfyp": [{"id": "20217732/ZDNGPUF3", "source": "zotero"}], "qvr85": [{"id": "20217732/QIV5MEM4", "source": "zotero"}], "twlqg": [{"id": "20217732/R3FP85YZ", "source": "zotero"}], "vch0l": [{"id": "20217732/MYVQS8JW", "source": "zotero"}]}} editable=true slideshow={"slide_type": ""} -->
## Topicality of “Heimat”

“Heimat” (home) has long been a much-discussed topic in Germany. Not only because of historical shadows, but also more recent events, such as the Reunification, and particularly the burgeoning debate on migration since 2015, have made this a highly topical issue that is shaping not only social but also political debates, that last until today. “Home” was a central element of the speech given by then-Federal President Frank-Walter Steinmeier on German Unity Day 2017. (<cite id="8ep5t"><a href="#zotero%7C20217732%2FLFIR4DFN">(Steinmeier 2017)</a></cite>) The renaming of the “Bundesministerium des Innern (Federal Ministry of the Interior)” to the “Bundesministerium des Innern für Bau und Heimat (Federal Ministry of the Interior, Building and Home)” (2019) and to Bundesministerium des Innern und für Heimat (Federal Ministry of the Interio and Home)” (2021) led to the politicization of the topic of “home” by the federal government, as had already happened in some federal states. (<cite id="35qmk"><a href="#zotero%7C20217732%2FGFCUEUX2">(Binder 2020)</a></cite>, p. 89f.) Various election programs and posters used the term in their election advertising between 2014 and 2021. (<cite id="f9w99"><a href="#zotero%7C20217732%2FL7LCZ2SY">(Oesterhelt 2021)</a></cite>, p. 5; <cite id="qgfyp"><a href="#zotero%7C20217732%2FZDNGPUF3">(Scharnowski 2019)</a></cite>, p. 3-10) Right-wing populist parties such as the AFD have turned the term into a political battle cry that plays a central role in preservation of homeland and in protecting Germany from the outside world and external influences. (<cite id="gegzb"><a href="#zotero%7C20217732%2FMYVQS8JW">(Korfkamp and Steuten 2022)</a></cite>, p. 121–134) In 2023, the far-right NPD party even renamed itself “Die Heimat” (The Homeland). In light of these developments, there is an ongoing debate about whether “Heimat” should still be researched academically, or whether it should be left to far right-wing movements and replaced by new concepts. (<cite id="vch0l"><a href="#zotero%7C20217732%2FMYVQS8JW">(Korfkamp and Steuten 2022)</a></cite>, p. 135–142) It is important to continue to engage with the concept of “Heimat” and to utilize it as an opportunity for coexistence rather than something exclusionary. (<cite id="j5lhv"><a href="#zotero%7C20217732%2FMYVQS8JW">(Korfkamp and Steuten 2022)</a></cite>, p. 140-142; <cite id="0ixik"><a href="#zotero%7C20217732%2F74QRKYPZ">(Mitzscherlich 2019)</a></cite>, p. 193f.) Especially in this age of mobility, migration, displacement, and impending climate catastrophe, it is essential to approach this topic in new ways. Beate Binder therefore reasonably suggested that we should focus less on finding an accurate definition of home and more on the question of “who is allowed to claim home and lay claim to it, and when” (<cite id="n2hul"><a href="#zotero%7C20217732%2FGFCUEUX2">(Binder 2020)</a></cite>, p. 87) and therefore to analyse “where, who, and how people talk about home.” (<cite id="krfwq"><a href="#zotero%7C20217732%2FGFCUEUX2">(Binder 2020)</a></cite>, p. 88). Particularly with regard to flight and migration, a key question is how people cope when they are forced to leave their “Heimat” as a result of violence, war, climate change, or other reasons, and find themselves in a place that is Thus i am researching how the idea of „Heimat” is transformed into the new situation and what forms of help or restrain influence these processes. Such a study needs to rely on the narrative (life-) interviews that are complex and multilayered sources but offer illuminating insights to a concept like home since interviewees refer to their “home-making” processes in many different forms. Oral History Interviews are accordingly a promising source and ideally suited to be re-used as research material. There is already several research that has conducted and analysed a few interviews on this theme. (<cite id="twlqg"><a href="#zotero%7C20217732%2FR3FP85YZ">(Kück 2021)</a></cite>; <cite id="qvr85"><a href="#zotero%7C20217732%2FQIV5MEM4">(Fuchs 2015)</a></cite>) Nevertheless, references to a broad complex like “home” are hard to find just with keywords or other simple search approaches since the concept is seldom referred to directly. It is heuristically challenging to identify and get access to narrative interviews as they are spread across many different archives, research institutions, and researchers. Based on the “Deutsche Forschungsgemeinschaft”(DFG) funded project "Oral-History.Digital" (OHD) (https://portal.oral-history.digital), we can rely on large numbers of interviews from a wide variety of archives and collections that have been digitized and are accessible online. In total, I have access to nearly 1’000 interviews from six different archives, which have been created within various research endeavours. 

Manual analysis of these interviews would not only be enormously time-consuming and therefore factually impossible but also raise methodological questions. Distant reading approaches, such as topic modeling, are accordingly preferred to analyse more or less visible traces and thematic clusters in the interview collections. There are already some research papers that examine the application of digital methods to life history interviews. (<cite id="3j5oe"><a href="#zotero%7C20217732%2FNQPGZC6Z">(Hodel, Möbus, and Serif 2022)</a></cite>; <cite id="d0i4k"><a href="#zotero%7C20217732%2FSMT6TLS8">(Möbus 2020)</a></cite>; <cite id="dwkif"><a href="#zotero%7C20217732%2F72D4T9FI">(Leh 2023)</a></cite>; <cite id="11p8r"><a href="#zotero%7C20217732%2FGYVTICFJ">(Pagenstecher 2017)</a></cite>) My research focuses more on the question of how topic modeling can yield beneficial insights in the study of life history interviews on the topic of “Heimat” (home).
This research falls within the research fields of digital history and oral history. The digital history deals with the analysis of historical source corpora using digital methods. (<cite id="h9s94"><a href="#zotero%7C20217732%2FPWDTM7BC">(Hiltmann 2022)</a></cite>p. 38-40) The interviews used in this study are mostly from oral history projects and were conducted as part of various research projects. In general, when analysing such interviews the approach is based on the premise of the unity of the interview and the interpretation of individual text passages in the overall context of the life story. A quantitative approach such as topic modeling only appears to contradict this premise at first glance. Distant reading, when combined with close reading, allows text passages to be included in the analysis. (<cite id="m05jq"><a href="#zotero%7C20217732%2FAV3J3ICJ">(Müller 2020)</a></cite>; <cite id="a443a"><a href="#zotero%7C20217732%2FJDH35IVA">(Krautter 2023)</a></cite> ) It is also important to emphasize that this form of analysis should not be seen as a replacement for existing methods of analysis, but rather as an additional way of approaching and evaluating source corpora. This is one of the central tasks of the digital humanities.

In order to process the research data using topic modeling, focusing on approaches to “Heimat”, it is key to create a reproducible yet flexible pipeline to process data and re-run the algorithms, if more data (interviews) should become available. Although existing topic modeling packages for Latent Dirichlet Allocation (LDA) (<cite id="ez9yq"><a href="#zotero%7C20217732%2FNGJ3HCW2">(Blei, Ng, and Jordan 2003)</a></cite>) in Python, like Genism, exist, they rely on very limited import forms. To ensure reproducibility, the general import had to be adapted as well as the crucial steps of preprocessing and presentation of the gained results. All of the steps catering to the specificity of the research data are in need of consideration. One of the regards deals with the mediality of the interview setting. It is crucial to determine who uttered the sentence in an interview situation
This essay is part of my doctoral thesis, which focuses on the cross-collection and secondary analyses of life history interviews using topic modeling on the subject of “Heimat” and “Beheimatung” (home-making).
After a brief introduction to the theme of “Heimat” and the topic modeling method, this essay follows the structure of the presented pipeline. After explaining the data structure developed, the various functions of preprocessing, processing, and post-processing of topic modelling, the results are presented and applied to the research question on how topic modeling can help to analyse the corpus on “Heimat” and “Beheimatung”.
 

<!-- #endregion -->

<!-- #region citation-manager={"citations": {"0ernl": [{"id": "20217732/6QS5ZLRL", "source": "zotero"}], "35qhd": [{"id": "20217732/6QS5ZLRL", "source": "zotero"}], "3vd6q": [{"id": "20217732/ZDNGPUF3", "source": "zotero"}], "4a24m": [{"id": "20217732/ZDNGPUF3", "source": "zotero"}], "5st39": [{"id": "20217732/JERKXUDW", "source": "zotero"}], "7hp1f": [{"id": "20217732/6HBPL7EY", "source": "zotero"}], "8tkup": [{"id": "20217732/6QS5ZLRL", "source": "zotero"}], "94har": [{"id": "20217732/74QRKYPZ", "source": "zotero"}], "9v4hi": [{"id": "20217732/CBXIFRVG", "source": "zotero"}], "btrzc": [{"id": "20217732/MYVQS8JW", "source": "zotero"}], "cr9e9": [{"id": "20217732/ZDNGPUF3", "source": "zotero"}], "d158v": [{"id": "20217732/CBXIFRVG", "source": "zotero"}], "ew10d": [{"id": "20217732/2UUDN69T", "source": "zotero"}], "fklpg": [{"id": "20217732/74QRKYPZ", "source": "zotero"}], "fogwm": [{"id": "20217732/ZDNGPUF3", "source": "zotero"}], "gtsw8": [{"id": "20217732/6HBPL7EY", "source": "zotero"}], "hnsex": [{"id": "20217732/CBXIFRVG", "source": "zotero"}], "iquxw": [{"id": "20217732/3ELLUTS7", "source": "zotero"}], "isaya": [{"id": "20217732/R3FP85YZ", "source": "zotero"}], "j938g": [{"id": "20217732/L7LCZ2SY", "source": "zotero"}], "jh24p": [{"id": "20217732/L7LCZ2SY", "source": "zotero"}], "jyika": [{"id": "20217732/MYVQS8JW", "source": "zotero"}], "kn42b": [{"id": "20217732/3ELLUTS7", "source": "zotero"}], "llvfq": [{"id": "20217732/6HBPL7EY", "source": "zotero"}], "netu7": [{"id": "20217732/R3FP85YZ", "source": "zotero"}], "ogaae": [{"id": "20217732/R3FP85YZ", "source": "zotero"}], "p4s0l": [{"id": "20217732/6QS5ZLRL", "source": "zotero"}], "paxql": [{"id": "20217732/MYVQS8JW", "source": "zotero"}], "q1ibd": [{"id": "20217732/L7LCZ2SY", "source": "zotero"}], "q9aa4": [{"id": "20217732/R3FP85YZ", "source": "zotero"}], "qjssf": [{"id": "20217732/2UUDN69T", "source": "zotero"}], "raasf": [{"id": "20217732/L7LCZ2SY", "source": "zotero"}], "s9sj5": [{"id": "20217732/2UUDN69T", "source": "zotero"}], "tungn": [{"id": "20217732/CBXIFRVG", "source": "zotero"}], "tzosg": [{"id": "20217732/6QS5ZLRL", "source": "zotero"}], "v1rcz": [{"id": "20217732/2UUDN69T", "source": "zotero"}], "vm0is": [{"id": "20217732/MYVQS8JW", "source": "zotero"}], "wgn1o": [{"id": "20217732/R3FP85YZ", "source": "zotero"}], "wn03j": [{"id": "20217732/R3FP85YZ", "source": "zotero"}], "x8tag": [{"id": "20217732/74QRKYPZ", "source": "zotero"}], "xktau": [{"id": "20217732/74QRKYPZ", "source": "zotero"}], "yy4xn": [{"id": "20217732/6QS5ZLRL", "source": "zotero"}], "yyw3q": [{"id": "20217732/R3FP85YZ", "source": "zotero"}], "z32m8": [{"id": "20217732/3ELLUTS7", "source": "zotero"}], "ztclk": [{"id": "20217732/ZDNGPUF3", "source": "zotero"}]}} editable=true slideshow={"slide_type": ""} -->
## 2.	What is “Heimat” and how to make it
The scientific study of the German term "Heimat" is a multidisciplinary field that draws upon various academic disciplines, including history, psychology, cultural studies, literary studies, social sciences, and anthropology. The various focal points, approaches, and interpretations of “Heimat” make it impossible to find a clear definition. It is therefore important to emphasize that “Heimat” is a concept that must always be viewed in a political and social context. (<cite id="tzosg"><a href="#zotero%7C20217732%2F6QS5ZLRL">(Jäger 2018)</a></cite>, p. 6; <cite id="wgn1o"><a href="#zotero%7C20217732%2FR3FP85YZ">(Kück 2021)</a></cite>, p. 47) In order to analyze the narratives concerning “Heimat” and the processes of settling in Germany among people who have migrated to Germany, it is first necessary to examine the meaning of the German term “Heimat”. An examination of the etymology of the term “Heimat” illuminates its multifaceted connotations. Nevertheless, it would be imprudent at this juncture to engage in an exhaustive historical debate. Recent works by cultural geographer Svenja Kück (<cite id="isaya"><a href="#zotero%7C20217732%2FR3FP85YZ">(Kück 2021)</a></cite>) and literary scholars Susanne Scharnowski (<cite id="fogwm"><a href="#zotero%7C20217732%2FZDNGPUF3">(Scharnowski 2019)</a></cite>) and Anja Oesterhelt (<cite id="jh24p"><a href="#zotero%7C20217732%2FL7LCZ2SY">(Oesterhelt 2021)</a></cite>) provide a valuable overview of the historical development.

The term "Heimat" first emerged in the 15th century and, until the late 19th century, was invariably linked to a particular geographical location. The legal term "Heimat" is understood to denote the community within which a person is eligible to receive material support in circumstances involving illness, advanced age or indigence. In the 17th century, the term underwent a semantic shift, acquiring an emotional connotation with the advent of the clinical concept of homesickness. This idea was subsequently transferred from the domain of medicine to that of general usage in Romanticism poetry. Conceptions of longing for home, of home as a desired place where the possibility of unrestricted security existed, began to spread. During the 19th century, two significant developments exerted considerable influence on the conceptualization of the notion of home. The processes of industrialization and the mass migration of the population from rural to urban areas, as well as emigration to the United States of America, resulted in a romanticized view of the old homeland. Through the experience of loss and the comparison of the new with the old, home became a central theme. The “Heimatschutzbewegung” (heritage conservation movement) emerged as a countermovement to industrialization, focusing, for example on heritage associations, on the protection of local traditions or the landscape, always with a specific local reference. (<cite id="netu7"><a href="#zotero%7C20217732%2FR3FP85YZ">(Kück 2021)</a></cite>, p. 29-34; <cite id="p4s0l"><a href="#zotero%7C20217732%2F6QS5ZLRL">(Jäger 2018)</a></cite>, p. 6-9).

However, the discourse on homeland, directed against the destruction caused by industrialization and modernization, did not take place exclusively in Germany, but throughout Europe. (<cite id="4a24m"><a href="#zotero%7C20217732%2FZDNGPUF3">(Scharnowski 2019)</a></cite>, p. 75-78) Advances in social legislation are leading to the abolition of the right of domicile and thus to the dissolution of the village or homeland as a concrete area of entitlement. (<cite id="ogaae"><a href="#zotero%7C20217732%2FR3FP85YZ">(Kück 2021)</a></cite>, p. 32-34; <cite id="ztclk"><a href="#zotero%7C20217732%2FZDNGPUF3">(Scharnowski 2019)</a></cite>, p. 34-55, 84) With the rise of nationalism, the concept of homeland gradually developed into an independent phenomenon that became ideologically charged and an element of political propaganda. This reached a terrifying peak during the Nazi era. The concept of homeland was charged with the regime's nationalist ideology and exploited for political ends. The extent to which a direct connection can be drawn here between a romantic notion of homeland and the “blood and soil” ideology is controversial. (<cite id="yyw3q"><a href="#zotero%7C20217732%2FR3FP85YZ">(Kück 2021)</a></cite>, p. 34-36; <cite id="yy4xn"><a href="#zotero%7C20217732%2F6QS5ZLRL">(Jäger 2018)</a></cite>, p. 14-16; <cite id="3vd6q"><a href="#zotero%7C20217732%2FZDNGPUF3">(Scharnowski 2019)</a></cite>, p. 97-99; <cite id="j938g"><a href="#zotero%7C20217732%2FL7LCZ2SY">(Oesterhelt 2021)</a></cite>, p. 47f.) In the aftermath of the Second World War, the concept of 'homeland' assumed a pivotal role in the context of displaced persons and self-perception in Germany. Nevertheless, the historical burden of National Socialism remained attached to the term, leading to calls for its rejection in the 1960s. During the 1970s and 1980s, the environmental movement provided a positive reinterpretation of the concept of Heimat, thereby underscoring the importance of a local and real context once again. (<cite id="wn03j"><a href="#zotero%7C20217732%2FR3FP85YZ">(Kück 2021)</a></cite>, p. 37f.) Parallel to developments in West Germany, the political leadership in East Germany attempted to establish the nation as a socialist homeland. However, there was little willingness to accept this “Heimat” propagated by the party leadership, instead the pre-socialist understanding of homeland, an emotionally charged local area, thrived. (<cite id="q9aa4"><a href="#zotero%7C20217732%2FR3FP85YZ">(Kück 2021)</a></cite>, p. 36; <cite id="raasf"><a href="#zotero%7C20217732%2FL7LCZ2SY">(Oesterhelt 2021)</a></cite>, p. 7; <cite id="jyika"><a href="#zotero%7C20217732%2FMYVQS8JW">(Korfkamp and Steuten 2022)</a></cite>, p. 79-85). The reunification in 1990 brought the issue of loss of homeland and new homeland back into society. (<cite id="ew10d"><a href="#zotero%7C20217732%2F2UUDN69T">(Costadura and Ries 2016)</a></cite>, p. 17; <cite id="btrzc"><a href="#zotero%7C20217732%2FMYVQS8JW">(Korfkamp and Steuten 2022)</a></cite>, p. 93-99)

The concept of Heimat is by no means a purely German phenomenon, even though the term is considered virtually untranslatable. (<cite id="gtsw8"><a href="#zotero%7C20217732%2F6HBPL7EY">(Demantowsky 2021)</a></cite>, p. 179-181; <cite id="s9sj5"><a href="#zotero%7C20217732%2F2UUDN69T">(Costadura and Ries 2016)</a></cite>, p. 9) However, this assumption has been criticized. Words for a similar concept can also be found in other languages: homeland (English), petite patrie (French), thuisland (Dutch), vlast (Czech), rodina (Родина Russian) (<cite id="8tkup"><a href="#zotero%7C20217732%2F6QS5ZLRL">(Jäger 2018)</a></cite>, footnote 7). Although it is always argued that the all-encompassing dimension and emotional depth of Heimat is difficult to translate, the question arises as to whether this is even possible in principle for a term that has no fixed definition itself but encompasses a diverse concept that must always be explained. Scharnowski traces the idea of an untranslatable word back to the rise of nationalism in the 19th century. Thus, the words for homesickness in Czech, Polish, and Russian are also considered untranslatable. (<cite id="cr9e9"><a href="#zotero%7C20217732%2FZDNGPUF3">(Scharnowski 2019)</a></cite>, p. 12) Modern approaches from psychology and cultural anthropology strongly link homeland with one's own human identity, which is thus given to all people and not limited to a specific language area. (<cite id="0ernl"><a href="#zotero%7C20217732%2F6QS5ZLRL">(Jäger 2018)</a></cite>, p. 4; <cite id="kn42b"><a href="#zotero%7C20217732%2F3ELLUTS7">(Mitzscherlich 2000)</a></cite>; <cite id="tungn"><a href="#zotero%7C20217732%2FCBXIFRVG">(Binder 2008)</a></cite> ) Even if the translatability is debatable, Oesterhelt correctly points out in her research that the assumption of untranslatability must not be neglected in the German understanding of Heimat. (<cite id="q1ibd"><a href="#zotero%7C20217732%2FL7LCZ2SY">(Oesterhelt 2021)</a></cite>, p. 66f.) Today, following a traditional understanding, home is still often understood as a connection with a specific local reference: place of origin, place of residence, region, or country. These are real places that can be left behind, but also revisited.

Overall, there are a multitude of different understandings of homeland, which are shaped and represented by various scientific, social, and political actors, and exploited by the latter. (<cite id="v1rcz"><a href="#zotero%7C20217732%2F2UUDN69T">(Costadura and Ries 2016)</a></cite>, p. 19; <cite id="5st39"><a href="#zotero%7C20217732%2FJERKXUDW">(Costadura, Ries, and Wiesenfeldt 2019)</a></cite>, p. 11f.; <cite id="vm0is"><a href="#zotero%7C20217732%2FMYVQS8JW">(Korfkamp and Steuten 2022)</a></cite>, p. 121) A distinction can be made between two fundamental assumptions. On the one hand, there is a static understanding of home, which refers to the immediate environment in the form of one's place of birth, place of residence, region, or country and follows a traditional understanding. The mostly real place can also be replaced by the idealized notion of a homeland and thus become an abstract goal that must first be created or restored. This conveys an understanding of belonging and exclusion. (<cite id="d158v"><a href="#zotero%7C20217732%2FCBXIFRVG">(Binder 2008)</a></cite>, p. 10; <cite id="7hp1f"><a href="#zotero%7C20217732%2F6HBPL7EY">(Demantowsky 2021)</a></cite>, p. 177f.; <cite id="qjssf"><a href="#zotero%7C20217732%2F2UUDN69T">(Costadura and Ries 2016)</a></cite>, p. 17f.) On the other hand, since the 1970s, there has been an increasing number of scientific papers advocating a reorientation of the concept of homeland. The objective of this reorientation is to remove the concept from a rigid, location-based context and historical baggage, and to place a stronger focus on subjective, emotional, and spatio-temporal levels. (<cite id="hnsex"><a href="#zotero%7C20217732%2FCBXIFRVG">(Binder 2008)</a></cite>, p. 177, 179; <cite id="paxql"><a href="#zotero%7C20217732%2FMYVQS8JW">(Korfkamp and Steuten 2022)</a></cite>, p. 100-102) The work of psychologist Beate Mitzscherlich makes an important contribution to the re-examination of the concept of home.  She points to a certain processual nature of home that emphasizes the individual's ongoing engagement “in relation to a (social) space that is considered home or is to be made into home.” (<cite id="xktau"><a href="#zotero%7C20217732%2F74QRKYPZ">(Mitzscherlich 2019)</a></cite>, p. 188; <cite id="iquxw"><a href="#zotero%7C20217732%2F3ELLUTS7">(Mitzscherlich 2000)</a></cite>) The emotional level refers to the feeling of home and is associated with positive feelings of security, safety, and familiarity, detached from the purely local level. She defines three dimensions of the feeling of home: the “sense of community,” which refers to experiences of social belonging; the “sense of control,” which refers to the experience of behavioural security and the ability to act; and the “sense of coherence,” which refers to subjective meaning and the certainty of having arrived at the right place. (<cite id="z32m8"><a href="#zotero%7C20217732%2F3ELLUTS7">(Mitzscherlich 2000)</a></cite>, p. 137f., 228; <cite id="94har"><a href="#zotero%7C20217732%2F74QRKYPZ">(Mitzscherlich 2019)</a></cite>, p. 185-188) She therefore advocates talking less about “Heimat” (home) and more about “Beheimatung” (home-making) in order to emphasize the processual nature of the concept. (<cite id="fklpg"><a href="#zotero%7C20217732%2F74QRKYPZ">(Mitzscherlich 2019)</a></cite>, p. 188) Following this idea, many research projects suggest that when considering home, we should move away from the word “Heimat” and its definition, and instead examine the individual design, the processes of arriving and settling in, and the active creation of a home. (<cite id="35qhd"><a href="#zotero%7C20217732%2F6QS5ZLRL">(Jäger 2018)</a></cite>, p. 26; <cite id="9v4hi"><a href="#zotero%7C20217732%2FCBXIFRVG">(Binder 2008)</a></cite>, p. 12; <cite id="llvfq"><a href="#zotero%7C20217732%2F6HBPL7EY">(Demantowsky 2021)</a></cite>, p. 187; <cite id="x8tag"><a href="#zotero%7C20217732%2F74QRKYPZ">(Mitzscherlich 2019)</a></cite>, p. 188f.)
These approaches can be meaningfully combined with my research interest in investigating the phenomenon of home in life history interviews, because by emphasizing that home is something individual that is strongly linked to one's own identity and can be located as a process of settling in, life history interviews are an ideal research source. People recount their entire life story and reconstruct various actions, thereby revealing strategies and processes.

It is therefore advisable to adopt an open approach to the concept of “Heimat” and to examine the interviews with regard to the strategies and concepts of “Heimat” that are conveyed and constructed there. Furthermore, it is important to acknowledge that the interviewees do not originate from Germany and bring their own or other ideas of “Heimat” from their countries of origin. By examining how the concept of “Heimat” is interpreted in Germany, we can gain insight into the extent to which the interviewees adapt this understanding or the extent to which they integrate their own concepts and address them in their narratives.

However, in order to identify and examine narratives of “Heimat”, it is necessary to first reduce them to a linguistic level. The manner and vocabulary employed in the discourse surrounding the concept of “Heimat” is a subject that merits investigation. A rudimentary search for keywords is of limited utility in this context, as the intricacies of “Heimat” cannot be distilled into easily definable terms, yet resonates with a myriad of disparate concepts. Furthermore, the question arises as to whether the term “Heimat” is employed explicitly, or whether it is instead insinuated implicitly within various narratives. Therefore, we must analyse the individual passages of the corpus based on the words used in them in order to determine whether and how they refer to “Heimat” and “Beheimatung”. Due to the length and volume of the text, it is impossible to analyse these interviews manually. Consequently, alternative approaches had to be identified. Distant reading methods, such as topic modeling, appear to be both promising and sufficiently mature to analyse unrecognized traces and thematic clusters in the approximately 1,000 interviews on the basis of individual words.

The underlying principle of this quantitative approach is to compare individual processes of settling in order to ascertain whether a distant reading approach reveals commonalities or even patterns that yield new insights that would not be possible with an analogue approach. The implementation of this approach is best facilitated by topic modeling.

<!-- #endregion -->

<!-- #region editable=true slideshow={"slide_type": ""} -->
## 3.	OHTM-Pipeline

<!-- #endregion -->

<!-- #region citation-manager={"citations": {"1v38i": [{"id": "20217732/NGJ3HCW2", "source": "zotero"}], "3kgfa": [{"id": "20217732/JVIR76WE", "source": "zotero"}], "48tyg": [{"id": "20217732/DDQTN947", "source": "zotero"}], "4zvbl": [{"id": "20217732/F8E46RVN", "source": "zotero"}], "638gl": [{"id": "20217732/NGJ3HCW2", "source": "zotero"}], "6k9bt": [{"id": "20217732/TZBHMXAR", "source": "zotero"}], "6q5qd": [{"id": "20217732/UM29IRL6", "source": "zotero"}], "70mqd": [{"id": "20217732/D3KBRXUR", "source": "zotero"}], "73l4c": [{"id": "20217732/R5BJGDG4", "source": "zotero"}], "91ls9": [{"id": "20217732/NGJ3HCW2", "source": "zotero"}], "91wwk": [{"id": "20217732/WQIJRWL6", "source": "zotero"}], "cmd3g": [{"id": "20217732/F8E46RVN", "source": "zotero"}], "h333c": [{"id": "20217732/CQ6D4YB5", "source": "zotero"}], "ig8ng": [{"id": "20217732/ELPZAK6U", "source": "zotero"}], "l2y4p": [{"id": "20217732/HGJPHBR2", "source": "zotero"}], "nmyan": [{"id": "20217732/7G6V3JZC", "source": "zotero"}], "nyrhk": [{"id": "20217732/NGJ3HCW2", "source": "zotero"}], "q3ppp": [{"id": "20217732/3JIVN6SY", "source": "zotero"}], "r3kxr": [{"id": "20217732/CQ6D4YB5", "source": "zotero"}], "vllhd": [{"id": "20217732/JDH35IVA", "source": "zotero"}], "wpp4k": [{"id": "20217732/QLLN32IE", "source": "zotero"}], "x3tyq": [{"id": "20217732/IF7BCK5V", "source": "zotero"}], "xtkmj": [{"id": "20217732/YS9UZ9PJ", "source": "zotero"}], "z5db6": [{"id": "20217732/QR5LS2Y7", "source": "zotero"}]}} editable=true slideshow={"slide_type": ""} -->

### 3.1.	Topic Modeling for finding “Beheimatung”
The topic modeling used in this study is based on the Latent Dirichlet Allocation (LDA)(<cite id="91ls9"><a href="#zotero%7C20217732%2FNGJ3HCW2">(Blei, Ng, and Jordan 2003)</a></cite>) method, which calculates the statistical distribution and proximity of the individual words that occur in a document to each other and assigns the words to topics. The resulting word lists of topics can then be interpreted thematically and traced back to the documents via the topic-document distribution. LDA operates under the assumption that each document represents a composition of different topics and consequently assigns a weighting to each topic. (<cite id="nyrhk"><a href="#zotero%7C20217732%2FNGJ3HCW2">(Blei, Ng, and Jordan 2003)</a></cite>) In addition to LDA, there are other algorithms which topic modeling can be calculated with: LSA, BERTopic for example, however, this paper will not go into this further, for a comparison of the different algorithms see Curchill/ Singh 2022. LDA can be used with two different established approaches: Mallet (<cite id="73l4c"><a href="#zotero%7C20217732%2FR5BJGDG4">(“Mallet: MAchine Learning for LanguagE Toolkit” n.d.)</a></cite>) [McCallum 2002]), which runs on Java and is based on Gibbs sampling (<cite id="wpp4k"><a href="#zotero%7C20217732%2FQLLN32IE">(Griffiths and Steyvers 2004)</a></cite>) and Gensim ()[Řehůřek, Sojka 2010], which runs in Python and attempts a statistical approach based on online variational bayes. (<cite id="ig8ng"><a href="#zotero%7C20217732%2FELPZAK6U">(Wang, Paisley, and Blei 2011)</a></cite>) A comparative study of various historical corpora has demonstrated that topic modeling with LDA Mallet achieves optimal outcomes for life history corpora. (<cite id="h333c"><a href="#zotero%7C20217732%2FCQ6D4YB5">(Hodel, Möbus, and Serif 2022a)</a></cite>).
The effectiveness of topic modeling as a methodological approach is attributable to the fact that the statistical calculation of words is based solely on the corpus, without the need for external information. The composition of the documents is calculated exclusively on the words in the corpus using the bag-of-words approach. The order of the words in the documents or linguistic relationships is of no relevancy; it is only a matter of the frequency with which a word occurs in combination with another word in the same unit (<cite id="1v38i"><a href="#zotero%7C20217732%2FNGJ3HCW2">(Blei, Ng, and Jordan 2003)</a></cite>, p. 994f.) The statistical calculation and probability distribution of the words to the topics and of the topics across the documents is conducted in an iterative process, whereby results are corrected and rechecked by repeatedly analysing the documents. Each word is assigned to each topic, and each topic is assigned to a document with a certain probability. Therefore, word lists are obtained for the individual topics, which occur in the documents with decreasing probability. The most notable aspect of this approach is that the word lists, which were calculated exclusively based on statistical composition, frequently exhibit semantic correlations that can be interpreted thematically by researchers and traced back into the texts. This insight signifies that themes can be identified in text passages without the necessity of providing external information to the model (<cite id="638gl"><a href="#zotero%7C20217732%2FNGJ3HCW2">(Blei, Ng, and Jordan 2003)</a></cite>, p. 995-999) However, topic modeling does not function according to a simple "plug and play" principle, as it requires presetting that must be carefully coordinated with each other, as they have a considerable influence on the results. 

This presetting includes determining the number of topics, which represents a preliminary assumption as to how many different topics are contained in a corpus. The number of iterations is determined by the frequency with which the algorithm processes the corpus to calculate results and correct the distribution based on individual documents. However, it is important to note that this value also determines when a model is completed, as topic modeling does not have a fixed end point that is dependent on the quality of the results. Instead, it runs through the number of iterations specified for the calculation. The random seed determines the point in the corpus at which the calculation begins, thereby establishing the initial random distribution of the topics for the first random probability distribution (a priori). A fixed or predefined random seed ensures that the calculation always initiates from the same point, with otherwise constant parameters. Consequently, this enables the investigation of the influence of other parameters with constant factors, and the reproduction of results by other researchers. In addition to these parameters, there are also so-called hyperparameters that have a direct influence on the algorithm and the probability calculation. Alpha influences the distribution of the probability of the topics across the documents, and beta the distribution of the probability of the words in the topics. Optimized Interval is a mechanism that regulates the number of iterations from which an internal adjustment of alpha should take place, based on previous calculations. (<cite id="4zvbl"><a href="#zotero%7C20217732%2FF8E46RVN">(Du 2024)</a></cite>, p. 14f.) The preprocessing of the corpus exerts a considerable influence on the results, a matter that is addressed in greater detail in the relevant chapters of the pipeline. The present challenge is to ascertain the optimal settings for these parameters for the specific research corpus. Given their substantial impact on outcomes, the question of when a model is deemed accurate or of high quality arises. There exist shared methods and metrics designed to describe the quality of topic models, achieved by calculating and comparing these results. (<cite id="cmd3g"><a href="#zotero%7C20217732%2FF8E46RVN">(Du 2024)</a></cite>, p. 34-54) However, our previous research has shown that these methods are not conducive to the evaluation of good quality topic models. (<cite id="q3ppp"><a href="#zotero%7C20217732%2F3JIVN6SY">(Bayerschmidt et al. 2025)</a></cite>, p. 28-36)

It is not possible to predict which parameter settings are useful for which composition of a corpus. The evaluation of the results of a topic model has long been the subject of extensive interdisciplinary debate. (<cite id="z5db6"><a href="#zotero%7C20217732%2FQR5LS2Y7">(Chang et al. 2009)</a></cite>; <cite id="3kgfa"><a href="#zotero%7C20217732%2FJVIR76WE">(Lau, Newman, and Baldwin 2014)</a></cite>; <cite id="6k9bt"><a href="#zotero%7C20217732%2FTZBHMXAR">(Khodorchenko, Butakov, and Nasonov 2022)</a></cite>; <cite id="xtkmj"><a href="#zotero%7C20217732%2FYS9UZ9PJ">(Miner et al. 2023)</a></cite>; <cite id="nmyan"><a href="#zotero%7C20217732%2F7G6V3JZC">(Shi et al. 2019)</a></cite>; <cite id="70mqd"><a href="#zotero%7C20217732%2FD3KBRXUR">(Dobson 2020)</a></cite>) In a previous research project, Dennis Möbus and I chose a qualitative approach to determine the parameters and, above all, the optimal number of topics. A range of models was calculated, incorporating both maximum and minimum values. One model incorporated 50 topics, while another model incorporated 500 topics. The topic-word-lists, individual text passages and the topic-document distribution were then analysed in a cursory manner to ascertain whether the number of topics was excessive or insufficient. The threshold values of the parameter under investigation are then approximated successively, with the results undergoing further analysis and correction until a suitable model is identified (<cite id="l2y4p"><a href="#zotero%7C20217732%2FHGJPHBR2">(Bayerschmidt and Möbus 2025)</a></cite>) The selection of a suitable model is dependent upon the specific nature of the research question or research interest under consideration. This iterative approach to the final topic model signifies that the method does not start with the final model, but rather with the search for the ideal parameters. Topic modeling is not merely a methodological approach; rather, it constitutes an integral component of the analytical process itself.

In the context of my research, I do not employ topic modeling to describe my corpus through the topics, but rather utilize the topic-document distribution to identify relevant text passages on the topic of home. Through the interpretation of topic word lists, it is possible to identify the topics that are thematically relevant to narratives concerning the processes of “Heimat” or “Beheimatung”. These topics can then be identified in text passages with a high degree of reliability. This is particularly advantageous when “Heimat” is discussed implicitly. Moreover, distant reading can be utilized to identify connections and patterns between disparate subjects, as LDA calculates the weighting per text passage for each topic. (<cite id="r3kxr"><a href="#zotero%7C20217732%2FCQ6D4YB5">(Hodel, Möbus, and Serif 2022b)</a></cite>; <cite id="6q5qd"><a href="#zotero%7C20217732%2FUM29IRL6">(König 2019)</a></cite>; <cite id="x3tyq"><a href="#zotero%7C20217732%2FIF7BCK5V">(Althage 2022)</a></cite>; <cite id="vllhd"><a href="#zotero%7C20217732%2FJDH35IVA">(Krautter 2023)</a></cite>; ) [Moretti 2009]
Despite the existence of software solutions in the digital humanities that facilitate topic modeling without the necessity of programming expertise, such as the DARIAH Topic Explorer (<cite id="91wwk"><a href="#zotero%7C20217732%2FWQIJRWL6">(Simmler, Thorsten, and Pielström 2019)</a></cite>) or the Leipzig Corpus Miner (<cite id="48tyg"><a href="#zotero%7C20217732%2FDDQTN947">(Niekler, Wiedemann, and Heyer 2017)</a></cite>), their technical functionality remains constrained, precluding the full manipulation of all pertinent parameters. Furthermore, the software does not offer the option to divide the imported texts into smaller sections, known as 'chunks', which can be advantageous when working with extensive texts. The subject of chunking is addressed in greater depth in the relevant chapter of the pipeline. Another hurdle was importing the data formats available to me, because I would first have had to convert the files for the respective applications. This also applies to existing Python packages for LDA such as Gensim.

Not only the import had to be specially adapted but also some steps of the preprocessing, result presentation and result combination. My research data has special characteristics that need to be considered when analysing the results. Since these are interviews, it always depends on whether a sentence with its content was said by the interviewer or the interviewee and when it was said. For many of my transcripts I have time codes that refer to the respective passage in the original video or audio interview. It is important to link the results of the topic modeling with this relevant metadata, which is not possible in the solutions like Gensim or the DARIAH Topic Explorer. Therefore, with the help of Dennis Möbus and based on his preliminary research, I developed my own topic modeling pipeline for my research, which is specialized for my data and enables all relevant options and settings of topic modeling: the Oral History Topic Modeling pipeline, OHTM pipeline (Bayerschmidt [2025] https://github.com/bayerschphi/ohtm_pipeline). 


<!-- #endregion -->

<!-- #region editable=true slideshow={"slide_type": ""} -->
### 3.2.	OHTM Pipeline Structure:
The OHTM pipeline can be obtained via a GitHub repository (https://github.com/bayerschphi/ohtm_pipeline) and enables users to perform topic modeling based on LDA Mallet locally on their own computer to ensure the work with sensitive and protected data, such as biographical interviews, in a protected working environment. With the pipeline I programmed, all necessary steps of topic modeling, from importing the data to evaluating the results, as well as the numerous configuration options, can be carried out. The pipeline operates via a central python script, main.py, in which all relevant options are set, and the respective functions can be switched on or off using 'True' or 'False'. The functions of the pipeline can be divided into three sections:
Preprocessing, that controls the import of files into the pipeline and the preparation of the texts for topic modeling. Processing, that includes all functions and parameters relating to the calculation of topic models and finally post-processing, that enables the results to be displayed and analysed.
As soon as all the desired functions and parameters have been set, the main.py is executed and the pipeline performs everything automatically.



<!-- #endregion -->

<!-- #region editable=true slideshow={"slide_type": ""} tags=["hermeneutics"] -->
The main.py passes all variables to a main function, which then executes the various sub-functions. In each run, a central file with its own data structure, the so-called OHTM-file, is loaded, processed, saved and passed on to the next function. This allows individual functions to be used independently and the intermediate results to be saved. Thanks to the modular structure of the pipeline, existing functions can be adapted, or new ones can be added without changing the basic structure. Before the first use, the paths leading to the respective save and load locations must be defined. All OHTM-files and models are saved and loaded under output_folder, as is the stop word list. The interviews cannot be accessed directly but must be in a folder that represents the archive, and these archive folders are in a folder to which source_path then refers. The middle area includes all general functions that are relevant for topic modeling and the preparation for it. They can be selected or deselected via “True” or “False”. In the last section, detailed settings can be made for the given functions to enable more control.
<!-- #endregion -->

```python editable=true slideshow={"slide_type": ""} tags=["hermeneutics"]
from ohtm_pipeline.ohtm_pipeline.pipeline_function.pipeline import ohtm_pipeline_function
import os

''' Path Settings: '''
# Path to your mallet folder.
os.environ['MALLET_HOME'] = r'C:\\mallet-2.0.8' # does not work in the demo_main, just leave it, as it is
mallet_path: str = r'C:\mallet-2.0.8\bin\mallet' # does not work in the demo_main, just leave it, as it is


# Path to your output_folder.
output_folder: str = (r"./ohtm_pipeline/Demo")

# Set the path for your stop_word list.
stopword_file_name = "german_stopwords_standard.txt"

# Set the path to your sources. This must be the folder, where your documents are stored in another folder.
source_path: str = (r"Demo\demo_interviews")

source_folder = ["archive_1", "archive_2", "txt_files"]

""" Topic Modeling Settings: """

load_ohtm_file = True
load_file_name = "demo_ohtm_file_trained"

create_ohtm_file = False
save_ohtm_file = False
save_name = "demo_ohtm_file_trained"

# You need to set a save_name and set the option save_json to True to save the model
save_model = False # does not work in the demo_main, just leave it, as it is

use_preprocessing = False

# If you don't want to chunk your documents, set use_chunking to True and chunk_setting to 0
use_chunking = False
chunk_setting = 20

use_topic_modeling = False # does not work in the demo_main, just leave it, as it is
topics = 10 # does not work in the demo_main, just leave it, as it is

save_top_words = True
number_of_words = 20

print_ohtm_file = True
print_ohtm_file_settings = True
show_bar_graph_corpus = True
show_heatmap_corpus = True
```

<!-- #region editable=true slideshow={"slide_type": ""} -->
The pipeline is designed to be easily accessible and does not require in-depth programming knowledge. In this way, the greatest possible accessibility can be offered to enable researchers to independently analyse or view the results and data using the pipeline. The heart of the pipeline is the OHTM-file, which contains a specially developed data structure for storing and using the data. 

<!-- #endregion -->

<!-- #region editable=true slideshow={"slide_type": ""} -->
### OHTM file structure	

The data structure combines interview transcripts, information, and references in one file. The file is re-created when new interviews are imported and forms the research corpus, which can be enriched in an ensuing step with all intermediate results such as stop word removal, lemmatization or chunking. To analyse narratives about “Beheimatung” and the resulting patterns and similarities in the individual text sections, it is important to relate the results of the topic modeling to the interview transcripts in various ways. The fundamental component of the data structure is the individual sentence, which is extracted from each transcript and assigned a unique identifier for the purpose of accurate referencing. This identifier enables the sentence to be correctly allocated to the appropriate interview and position within the transcript. The structure enables the storage and access of additional crucial information and metadata at the sentence level within the same file. The data frame is structured as a nested dictionary to create different levels of depth, to store the information. With the dictionary-keys, all the necessary information can be retrieved and combined. On the highest level, the OHTM file contains five entries. First, the “corpus”, which contains all the imported transcripts. Two entries that contain the results of topic modeling, the distribution of the topics for every chunk in “weight” and the wordlists of the calculated topics in “words”. “Stopwords” contains the list of words, that were removed during preprocessing and in “settings” all metadata, parameters and variables are stored.

<!-- #endregion -->

<!-- #region editable=true slideshow={"slide_type": ""} tags=["hermeneutics"] -->
The following schematic shows the entire structure of the OHTM-file and visualizes the different levels, references, and entries, which are called keys in the following, as it is a dictionary. The keys are divided into two categories: there are fixed keys that are predefined and are created during the import, “key”, and there are variable keys that depend on the file names of the interviews and the names of the archives, \<key\>.
<!-- #endregion -->

```python editable=true jdh={"module": "object", "object": {"source": ["Schematic structure of the OHTM file's data structure"]}} slideshow={"slide_type": ""} tags=["hermeneutics", "figure-ohtm-strcture-*"]
from IPython.display import Image, display
display(Image("./media/ohtm_file data structure.png"))
```

<!-- #region editable=true slideshow={"slide_type": ""} tags=["hermeneutics"] -->
By creating individual keys that are dependent on the archive name and the interview_id/interview name, similar structures and dependencies can be used in the different entries to relate the results to each other between the entries. 
<!-- #endregion -->

```python editable=true slideshow={"slide_type": ""}
from ohtm_pipeline.ohtm_pipeline.basic_functions.save_load import load_json_function
output_folder: str = (r"./media")
load_file_name = "jdh_ohtm_pipeline_final_version"
ohtm_file = load_json_function(load_file_name, output_folder)

interview_id = "adg0620"
archive = "adg"
chunk = 5
topic = 5

print(ohtm_file["weight"][archive][interview_id][str(chunk)][str(topic)])
print(ohtm_file["words"][str(topic)][:10])
print("Chunks")
for sents in ohtm_file["corpus"][archive][interview_id]["sent"]:
    if ohtm_file["corpus"][archive][interview_id]["sent"][sents]["chunk"] == chunk:
        print(ohtm_file["corpus"][archive][interview_id]["sent"][sents]["raw"])

```

<!-- #region editable=true slideshow={"slide_type": ""} -->
#### Corpus-entry

All imported interview transcripts are stored at the “corpus” level, divided according to the archives. The lowest level is formed by individual sentences, which are saved with relevant information and metadata. My research corpus consists of 991 interviews from seven different archives: the archive “Deutsches Gedächtnis” of the Institut für Geschichte und Biographie der FernUniversität in Hagen (ADG), the archive “Forced Labor 1939-1945” (ZWA) and "Colonia Dignidad. Ein chilenisch-deutsches Oral History-Archiv” (CDG) of the Freie Universität Berlin, the interview collection of the “Werkstatt der Erinnerung of the Forschungsstelle für Zeitgeschichte in Hamburg” (WdE), the contemporary witness archive of the “Dokumentationszentrum Flucht, Vertreibung, Versöhnung” (FVV), the collection ”Erzählte Lebensgeschichte" of the Museum Friedland (MFL) and a collection of the Hannah-Arendt Institut on education in the GDR. (HAI) The English-language interviews, where no translation was available, could not be included in the corpus due to the way topic modeling works, so only the German-language interviews and transcripts are used here. The only selection criterion was the availability and accessibility of the transcripts in CSV/ODT or TXT format.
<!-- #endregion -->

<!-- #region jdh={"module": "object", "object": {"source": ["Corpus archives, including the number of interviews"]}} tags=["table-1"] -->
| Archive | Interview |
|----------|----------|
| ADG   | 681   |
| ZWA   | 180   |
| HAI    | 45   |
| WdE    | 38   |
| CDG    | 23   |
| MFL    | 14   |
| FVV   | 10   |
<!-- #endregion -->

<!-- #region editable=true slideshow={"slide_type": ""} tags=["hermeneutics"] -->
The information stored for each sentence includes the "raw" form, as they are found in the transcripts and their "cleaned" form, after preprocessing. It was the goal to trace that the results back to the unprocessed sentences during the analysis. Additionally, the sentences contain a speaker shortcut, if applicable with a CSV transcript from OHD or if the TXT Files were manually restructured to mask the speaker, to ascertain whether the sentence was uttered by the interviewer or the interviewee.
Furthermore, time codes are saved, along with the information regarding the chunk in which the sentence is located. On the level above, a numerical identifier is allocated to each sentence, thereby determining its sequential arrangement within the original document. Based on this, it is possible to create the original text by utilizing the numerical data, whether in its raw or processed state. In this instance, it is important to ascertain whether the interview was included in the original topic model that was trained, or whether it was inferred by a pretrained model. If the interview was anonymized for the OHTM-file, the information is stored at this level that holds the capacity for additional metadata to be added at a later stage. The interview's provenance is the archive, which is situated one level above.
<!-- #endregion -->

```python editable=true slideshow={"slide_type": ""} tags=["hermeneutics", "figure-ohtm-file-corpus-*"]

from IPython.display import Image, display
metadata = {
    "jdh": {
        "module": "object",
        "object": {
            "type": "image",
            "source": [ "File structure of the 'corpus' level"
            ]
        }
    }
}
display(Image("./media/ohtm_file_corpus.png"), metadata=metadata)
```

<!-- #region citation-manager={"citations": {"7adfb": [{"id": "20217732/NGJ3HCW2", "source": "zotero"}], "choa7": [{"id": "20217732/JVIR76WE", "source": "zotero"}], "dakas": [{"id": "20217732/HGJPHBR2", "source": "zotero"}], "djmc3": [{"id": "20217732/699XM8FV", "source": "zotero"}], "iwrpi": [{"id": "20217732/F8E46RVN", "source": "zotero"}], "n0l1r": [{"id": "20217732/ZIGUYY9P", "source": "zotero"}], "v2cgv": [{"id": "20217732/M2QTZUFP", "source": "zotero"}], "y5h5c": [{"id": "20217732/K9PXZS6X", "source": "zotero"}]}} editable=true slideshow={"slide_type": ""} tags=["hermeneutics"] -->
#### Words-entry

The topic word distribution of the individual topics is saved under “words”. In theory, every word of the dictionary is assigned a weight to each topic (<cite id="7adfb"><a href="#zotero%7C20217732%2FNGJ3HCW2">(Blei, Ng, and Jordan 2003)</a></cite>, p. 996). The Mallet wrapper used in this pipeline, originally from the Gensim library, saves the first 1000 words per topic by default. Evaluating the results of this corpus, only a maximum of 500 words have a value above 0. This is due to rounding inside the code. Many research papers interpret the topics based on the first 5-30 words of the topic-word-list. (<cite id="iwrpi"><a href="#zotero%7C20217732%2FF8E46RVN">(Du 2024)</a></cite>, p. 57-59; <cite id="n0l1r"><a href="#zotero%7C20217732%2FZIGUYY9P">(Newman et al. 2010)</a></cite>; <cite id="djmc3"><a href="#zotero%7C20217732%2F699XM8FV">(Mimno et al. 2011)</a></cite>; <cite id="choa7"><a href="#zotero%7C20217732%2FJVIR76WE">(Lau, Newman, and Baldwin 2014)</a></cite>; <cite id="y5h5c"><a href="#zotero%7C20217732%2FK9PXZS6X">(Aletras and Stevenson 2013)</a></cite>; <cite id="v2cgv"><a href="#zotero%7C20217732%2FM2QTZUFP">(Xing, Paul, and Carenini 2019)</a></cite>). My own research has shown that an interpretation based on the first 30 to 100 words, depending on the topic, is useful for a differentiated interpretation. (<cite id="dakas"><a href="#zotero%7C20217732%2FHGJPHBR2">(Bayerschmidt and Möbus 2025)</a></cite>) To keep maximum transparency and scalability, the default option of 1000 words is retained. Since life history interviews contain sensitive information, only the first 50 words of the topics are visible in the file published with this record, due to anonymization.
<!-- #endregion -->

```python editable=true slideshow={"slide_type": ""} tags=["figure-ohtm-file-words-*"]
from IPython.display import Image, display
metadata = {
    "jdh": {
        "module": "object",
        "object": {
            "type": "image",
            "source": [ "File structure of the 'words' level"
            ]
        }
    }
}
display(Image("./media/ohtm_file_words.png"), metadata=metadata)
```

<!-- #region editable=true slideshow={"slide_type": ""} tags=["hermeneutics"] -->
#### Weight-entry

The topic distribution of the individual chunks is saved under “weight”. The structure of this entry follows the structure of “corpus”, so that the keys set for the archives and interviews are identical. In this way, the appropriate entries in “weights” can be clearly assigned to the individual interviews in “corpus”.
<!-- #endregion -->

```python editable=true slideshow={"slide_type": ""} tags=["figure-ohtm-file-weights-*"]
from IPython.display import Image, display
metadata = {
    "jdh": {
        "module": "object",
        "object": {
            "type": "image",
            "source": [ "File structure of the 'weight' level"
            ]
        }
    }
}
display(Image("./media/ohtm_file_weights.png"), metadata=metadata)
```

<!-- #region editable=true slideshow={"slide_type": ""} tags=["hermeneutics"] -->
#### Stopwords-entry

To maintain a record of which stop words have been removed in which model, it is necessary to save the list of all stop words under the "stopwords" entry. The stop words are contained within a customizable TXT file, the content of which is transferred to this entry during the removal process. Consequently, the removed stop words can be retracted. In the case where the stop words are not removed via a predetermined list but through the implementation of a threshold – that is to say, the frequency of how often a word appears in the given corpus – the words can be looked up in this particular entry. Nevertheless, the function for the elimination of stop words by a threshold has not yet been published.
<!-- #endregion -->

```python editable=true slideshow={"slide_type": ""}
from ohtm_pipeline.ohtm_pipeline.basic_functions.save_load import load_json_function
output_folder: str = (r"./media")
load_file_name = "jdh_ohtm_pipeline_final_version"
ohtm_file = load_json_function(load_file_name, output_folder)

#Print the first 50 words of the stopword entry
print(ohtm_file["stopwords"][:50])
```

<!-- #region editable=true slideshow={"slide_type": ""} tags=["hermeneutics"] -->
#### Settings-entry

During preprocessing and processing, many different settings are selected that describe the model in its entirety. These settings must be recorded and visible for transparency so that different models can be distinguished and analysed. This also ensures that when enriching further interviews with this model, the identical preprocessing steps can be carried out, as the settings can be read directly from the OHTM file. These settings are saved in “settings”.
<!-- #endregion -->

```python editable=true slideshow={"slide_type": ""} tags=["figure-othm-file_settings-*"]
from IPython.display import Image, display
metadata = {
    "jdh": {
        "module": "object",
        "object": {
            "type": "image",
            "source": [ "File structure of the 'settings' level"
            ]
        }
    }
}
display(Image("./media/ohtm_file_settings.png"), metadata=metadata)
```

<!-- #region editable=true slideshow={"slide_type": ""} tags=["hermeneutics"] -->
#### Json file
It is important to mention that the OHTM-file is used as a Python dictionary within the single functions in the code and is converted to JSON for saving.  This transformation occurs within each individual function, thereby enabling independent usage of each function. The creation of the OHTM file is accompanied by the generation of a nested dictionary containing all the distinct levels, which is thereafter converted into a JSON file. The file can now be saved. If additional functions have been selected, the JSON file undergoes conversion to a dictionary within the function, processing, and the resultant data is written back to a JSON file. The OHTM file is always saved in its JSON variant. These two different data types are a structural fragment from an earlier development phase, which is unfortunately irreversible. As a result, all keys that were originally integers are no longer changed when they are first converted to strings and when they are converted back to a dictionary. Consequently, the OHTM file contains only strings. This is important if relevant keys, such as topics, are to be accessed, so that they are also transferred as strings within the variable.
<!-- #endregion -->

<!-- #region editable=true slideshow={"slide_type": ""} -->
#### Publish the Data
For the traceability and reproducibility of the research data and the results of topic modeling, it is important to be able to view all steps from the import of the transcripts to the analysis of the results. The selection of variables and settings, especially during preprocessing, does not follow a universal logic, but is strongly dependent on the research question and the composition of the corpus. They are an elementary component of the method critique and must therefore be accessible. This can be ensured by co-publication within the OHTM file.

<!-- #endregion -->

<!-- #region editable=true slideshow={"slide_type": ""} -->
#### Anonymization
However, in my case, publication of the entire OHTM file, including all life history interviews, is not possible due to the sensitivity of the content. Therefore, an anonymized version was created in which all entries in “corpus” were removed from “raw”, “cleaned” and “speaker”. In addition, the number of topic words has been limited to 50. If all the topic words are published, they also include streets or city names, that could lead to a deanonymization. However, all results can be traced back to the interviews. For this purpose, the pipeline offers the function of creating links directing to the interviews in the Oral-History.Digital archive instead of the text and, if timecodes are available, also directly to the corresponding text section.
<!-- #endregion -->

<!-- #region editable=true slideshow={"slide_type": ""} -->
## Preparing the search
<!-- #endregion -->

<!-- #region editable=true slideshow={"slide_type": ""} -->
### Problems with different text files and transcripts 

Before the transcripts can be imported into the pipeline and processed, they still need to be prepared in some cases. This does not mean text cleaning in a narrower sense, rather, it is a matter of text structuring the texts to be able to extract uniform information from the various file formats. In some cases, the transcripts were only available as PDF files and first had to be converted into a machine-readable format such as TXT. Subsequently, archive-specific information in the transcripts, such as information about the archive in the headers and footers, information about the interview before the transcript or, in some cases, time information had to be removed.
<!-- #endregion -->

<!-- #region citation-manager={"citations": {"zkgof": [{"id": "20217732/W3YEPUTB", "source": "zotero"}]}} editable=true slideshow={"slide_type": ""} tags=["hermeneutics"] -->
This is an example of an Interview transcript from Archive Zwangsarbeit. (<cite id="zkgof"><a href="#zotero%7C20217732%2FW3YEPUTB">(za253 2005)</a></cite>, p. 3) When I started my research, some interviews were only available in PDF format, available.
<!-- #endregion -->

```python editable=true slideshow={"slide_type": ""} tags=["hermeneutics", "figure-za253-transcript-*"]
from IPython.display import Image, display
metadata = {
    "jdh": {
        "module": "object",
        "object": {
            "type": "image",
            "source": [ "Transcript excerpt from the interview za253, p. 3"
            ]
        }
    }
}
display(Image("./media/transcripts/za253_transcript_ger.png"), metadata=metadata)
```

<!-- #region citation-manager={"citations": {"pg0cn": [{"id": "20217732/W3YEPUTB", "source": "zotero"}]}} editable=true slideshow={"slide_type": ""} tags=["hermeneutics"] -->
After converting the file from a PDF to TXT, some information, like the footers and headers, timecodes and heading and subheadings had to be removed. The timecodes were not consistent and therefore not usable for my research. To present the different steps clearly, I have merged two different pages of the transcript, p. 3 and p. 61, for the demonstration. (<cite id="pg0cn"><a href="#zotero%7C20217732%2FW3YEPUTB">(za253 2005)</a></cite>, p. 3, 61)
<!-- #endregion -->

```python editable=true slideshow={"slide_type": ""} tags=["hermeneutics"]
text = open("./media/transcripts/za253_transcript_ger_S3_S61.txt", 'r', encoding="utf-8").read()
print(text)
```

<!-- #region editable=true slideshow={"slide_type": ""} tags=["hermeneutics"] -->
All this information must be removed for further processing. We can use the structure of the TXT file, as most of this information is on a separate line and use regex to delete the lines. I performed this procedure in software “Notepad++” using the search and replace function for all open documents at the same time. After the text has been cleaned of unwanted content, I restructured it, so that all sentences until the next speaker change are in one line, with the speaker abbreviation at the start. I masked the abbreviations between two *-symbols so I can read them out in the pipeline.
<!-- #endregion -->

```python editable=true slideshow={"slide_type": ""} tags=["hermeneutics"]
import re
text_1 = re.sub(r"^Band .*$", '',text, flags=re.MULTILINE)
text_2 = re.sub(r"\d{2}:\d{2}:\d{2} ", '',text_1, flags=re.MULTILINE)
text_3 = re.sub(r"^Zitierweise.*$", '',text_2, flags=re.MULTILINE)
text_4 = re.sub(r"^Übersetzung.*$", '',text_3, flags=re.MULTILINE)
text_5 = re.sub(r"^\d+[\., ].*$", '',text_4, flags=re.MULTILINE)
text_6 = (text_5.replace("{", "").replace("}", "").replace("[", "(").replace("]",")"))

print(text_6)
print("-----------------------------------------------")

interviewer = "Czerwiakowski, Ewa"
interviewe = "Bohle-Szacki, Helena"
text_7 = re.sub(interviewer,"*CE*",text_6)
text_8 = re.sub(interviewe,"*HBS*",text_7)
text_9 = re.sub(r"\*HBS:\*","*HBS*:",text_8)
text_10 = re.sub(r"\n","",text_9)
text_11 = re.sub(r"(\*(.*?)\*)", r"\n\1", text_10)

print(text_11)
```

<!-- #region editable=true slideshow={"slide_type": ""} -->
This restructuring is very time-consuming, especially with different archives or layouts. Thanks to OHD's infrastructure, it is possible to obtain most interview transcripts directly from OHD in a standardized data structure. The transcripts in CSV or ODT format were made available to me by individual archives on request. The files are structured in such a way that the first column contains the tape number for older interviews, the second column the time codes, the third column the speaker abbreviation and the fourth column the sentences of the transcript. The files are the time-aligned transcripts that are used as subtitles. These files can be fed directly into the pipeline without prior restructuring.
<!-- #endregion -->

<!-- #region jdh={"module": "object", "object": {"source": ["LABEL TO ADD"]}} tags=["table-2"] -->
| Format | ADG | ZWA | HAI |WdE | CDG |MFL | FVV |
|----------|----------|----------|----------|----------|----------|----------|----------|
| CSV   | 674   | 0   | 0   | 22   | 23   | 0   | 0   |
| TXT   | 7   | 180   | 45   | 16   | 0   | 14   | 10   |
<!-- #endregion -->

<!-- #region editable=true slideshow={"slide_type": ""} -->
### How to pack the pipeline – building the corpus

During the file import, the interviews are imported into the pipeline and, depending on their file format, processed. A distinction is made here between TXT and CSV/ODT.
<!-- #endregion -->

```python editable=true slideshow={"slide_type": ""}
# This code has no function and is for illustration purposes only
def ohtm_file_creation_function(source: list = "", source_path: str = "",
                                speaker_txt: bool = True, folder_as_archive: bool = False):

    # This sections creats the raw dictionary, with the different layers and settings.
    ohtm_file = {"corpus": {}, "weight": {}, "words": {}, "stopwords": {}, "correlation": {}, "settings": {}}
    ohtm_file["settings"]["interviews"] = {}
    ohtm_file["settings"]["interviews"]["total"] = 0
    ohtm_file["settings"]["interviews_trained"] = {}
    ohtm_file["settings"]["interviews_inferred"] = {}
    ohtm_file["settings"]["topic_modeling"] = {}
    ohtm_file["settings"]["topic_modeling"]["trained"] = "False"
    ohtm_file["settings"]["topic_modeling"]["inferred"] = "False"
    ohtm_file["settings"]["preprocessing"] = {}
    ohtm_file["settings"]["preprocessing"]["preprocessed"] = "False"
    ohtm_file["settings"]["preprocessing"]["stopwords_removed"] = "False"
    ohtm_file["settings"]["preprocessing"]["lemma"] = "False"
    ohtm_file["settings"]["preprocessing"]["chunked"] = "False"
    ohtm_file["settings"]["preprocessing"]["chunk_setting"] = "None"
    ohtm_file["settings"]["anonymized"] = {}
    ohtm_file["settings"]["anonymized"]["anonymized"] = "False"
    ohtm_file["settings"]["anonymized"]["exceptions"] = ()
    ohtm_file["settings"]["ohtm_file_version"] = 0.8

    # The documents are loaded from the source_path by creating the path to the folder in the source path.
    # The Iteration loads every single dokument and transforms it into the dictionary.

    for folder in source:   # loads every folder in the source_path folder.
        archive_id_name_folder = (str(folder)).lower()
        folder_path = os.path.join(source_path, folder)  # creating the path to the single folders.
        print(folder_path)
        for file in os.listdir(folder_path):  # creats the path and loads the files within the folders.
            print(file)
            file_path = os.path.join(folder_path, file)

            # The code checks, if the file is a .txt, .ods. or .csv file. The different files are processed differently.
            # load the .txt file. For this code, a .txt file with an interview requires a special processing.
            # Especially for masking the speakers. This is shown in the readme.txt
            # If you only have plan text, without a speaker, set the settings of speaker to False.

```

<!-- #region editable=true slideshow={"slide_type": ""} tags=["hermeneutics"] -->
The interview IDs are formed from the file name in this step. For my research data, the archive name was part of the file name and could be found in the first three characters, due to the name management of OHD. e.g.: “ADG0001.csv” became the Interview “ADG0001” inside the archive “ADG”. Generally, in the algorithm, the information about the archive can be obtained from the folder name. A different sub-function is selected depending on the file extension. The TXT files are first pre-structured during import by replacing all punctuation marks with a “.”, which can later be used to separate the individual sentences. The content of the TXT file is then separated at the line breaks to obtain the individual lines, which consist of a speaker abbreviation and the subsequently spoken sentences. The speaker abbreviation is masked at the “*”, set as a variable, and deleted from the sentence. The subsequent sentences are separated at the “.” and created as a consecutive number under '‘sent" and saved in the “raw” entry. This includes abbreviations. The set speaker variable is then stored in “speaker”. This is only possible by previous restructuring using regex. The masking of the speaker’s abbreviations is set by default but can also be set to “False” if the text does not contain any speakers. This means that sources other than interviews can also be used with this pipeline. If this is set to “False”, the respective line is not scanned, and the variable is created as an empty entry for each sentence. During the import, the total number of interviews and the interviews per archive are saved under "settings".
<!-- #endregion -->

```python editable=true slideshow={"slide_type": ""}
# This code has no function and is for illustration purposes only
file = "test.test"  
if file.split(".")[1] == "txt":
        try:
            text = open(os.path.join(folder_path, file), 'r', encoding='UTF-8').read()
        except UnicodeDecodeError:
            try:
                text = open(os.path.join(folder_path, file), 'r', encoding='UTF-8-sig').read()
            except UnicodeDecodeError:
                try:
                    text = open(os.path.join(folder_path, file), 'r', encoding='UTF-16-le').read()
                except UnicodeDecodeError:
                    try:
                        text = open(os.path.join(folder_path, file), 'r', encoding='UTF-16-be').read()
                    except UnicodeDecodeError:
                        text = open(os.path.join(folder_path, file), 'r', encoding='ANSI').read()
                        text = text.encode('UTF-8')
                        text = text.decode('UTF-8', 'ignore')

        text_unified = (text.replace('!', '. ').replace('?', '. ').replace(';', '. ').replace('...,', ', ').replace(
            '..,', ', ').replace('"', ' ').replace("'", ' ').replace(" - ", " "))

        text_split = text_unified.split('\n')
        interview_id = file.split(".")[0].lower()
        if folder_as_archive:
            archive_id = archive_id_name_folder
        else:
            archive_id = file[:3].lower()
        if archive_id not in ohtm_file["corpus"]:
            ohtm_file["corpus"][archive_id] = {}
            ohtm_file["settings"]["interviews"][archive_id] = 0
        ohtm_file["corpus"][archive_id][interview_id] = {}
        ohtm_file["settings"]["interviews"][archive_id] = (ohtm_file["settings"]["interviews"][archive_id])+1
        ohtm_file["settings"]["interviews"]["total"] = (ohtm_file["settings"]["interviews"]["total"])+1
        ohtm_file["corpus"][archive_id][interview_id]["sent"] = {}
        ohtm_file["corpus"][archive_id][interview_id]["model_base"] = {}
        ohtm_file["corpus"][archive_id][interview_id]["anonymized"] = False
        sent_number = 1
        for line in text_split:
            if len(line) == 1:
                print("line is zero")
            else:
                if speaker_txt:
                    try:
                        line = line.lstrip('\ufeff')
                        speaker = re.findall(r"^\*(.*?)\*[ ]", line)[0]
                    except IndexError:
                        speaker = speaker
                text = re.sub(r"<(.*?)>[ ]", "", line)
                text = re.sub(r"\*(.*?)\*[ ]", "", text)
                sent_split = text.split(". ")
                for sent in sent_split:
                    ohtm_file["corpus"][archive_id][interview_id]["sent"][sent_number] = {}
                    ohtm_file["corpus"][archive_id][interview_id]["sent"][sent_number]["raw"] = str(sent)
                    ohtm_file["corpus"][archive_id][interview_id]["sent"][sent_number]["time"] = {}
                    ohtm_file["corpus"][archive_id][interview_id]["sent"][sent_number]["tape"] = {}
                    ohtm_file["corpus"][archive_id][interview_id]["sent"][sent_number]["cleaned"] = {}
                    ohtm_file["corpus"][archive_id][interview_id]["sent"][sent_number]["speaker"] = {}
                    if speaker_txt:
                        ohtm_file["corpus"][archive_id][interview_id]["sent"][sent_number]["speaker"]\
                            = str(speaker)
                    ohtm_file["corpus"][archive_id][interview_id]["sent"][sent_number]["chunk"] = {}
                    sent_number += 1
```

<!-- #region editable=true slideshow={"slide_type": ""} tags=["hermeneutics"] -->
Importing CSV files does not differ significantly from TXT files. Each line can be processed directly without prior separation and created as a consecutive number under “sents” and saved under “raw”. The speaker’s abbreviations do not have to be masked from the strings but can be set directly from the corresponding column of the file as a variable for the following sentence. The big advantage is that we get another variable via the CSV files, namely the timecodes, which come from the time-aligned transcripts. These are saved under “time”. The difference between the CSV files and TXT files is the definition of one sentence. In the TXT files, a sentence follows the structure of all words between two punctuation marks. In the CSV file, a sentence contains all words and punctuations between two timecodes. This is advantageous, because the timecode defines the start of a sentence and allows us to trace it directly back to the original interview recordings.
<!-- #endregion -->

```python editable=true slideshow={"slide_type": ""}
# This code has no function and is for illustration purposes only
file = "test.test"  
if file.split(".")[1] == "csv":
    with open(file_path, 'r', newline='', encoding='utf-8') as csvfile:
        interview = csv.reader(csvfile, delimiter="\t", quotechar= None)
        next(interview) # Skips the first line, the header line of the file.
        interview_id = (file.split(".")[0].split("_")[0]).lower()
        if folder_as_archive:
            archive_id = archive_id_name_folder
        else:
            archive_id = (file[:3]).lower()
        if archive_id not in ohtm_file["corpus"]:
            ohtm_file["corpus"][archive_id] = {}
            ohtm_file["settings"]["interviews"][archive_id] = 0
        if interview_id not in ohtm_file["corpus"][archive_id]:
            ohtm_file["corpus"][archive_id][interview_id] = {}
            ohtm_file["settings"]["interviews"][archive_id] = (ohtm_file["settings"]["interviews"][archive_id]) + 1
            ohtm_file["settings"]["interviews"]["total"] = (ohtm_file["settings"]["interviews"]["total"]) + 1
            ohtm_file["corpus"][archive_id][interview_id]["sent"] = {}
            ohtm_file["corpus"][archive_id][interview_id]["model_base"] = {}
            sent_number = 1
        for line in interview:
            text = line[3]
            text2 = str(text)
            text_cleaned = re.sub(r"<(.*?)>", " ", text2)
            ohtm_file["corpus"][archive_id][interview_id]["sent"][sent_number] = {}
            ohtm_file["corpus"][archive_id][interview_id]["sent"][sent_number]["raw"] = str(text_cleaned)
            ohtm_file["corpus"][archive_id][interview_id]["sent"][sent_number]["speaker"] = {}
            ohtm_file["corpus"][archive_id][interview_id]["sent"][sent_number]["speaker"] = str(line[2])
            ohtm_file["corpus"][archive_id][interview_id]["sent"][sent_number]["time"] = {}
            ohtm_file["corpus"][archive_id][interview_id]["sent"][sent_number]["time"] = str(line[1])
            if str(line[0]) == "":
                ohtm_file["corpus"][archive_id][interview_id]["sent"][sent_number]["tape"] = "1"
            else:
                ohtm_file["corpus"][archive_id][interview_id]["sent"][sent_number]["tape"] = str(line[0])
            ohtm_file["corpus"][archive_id][interview_id]["sent"][sent_number]["cleaned"] = {}
            ohtm_file["corpus"][archive_id][interview_id]["sent"][sent_number]["chunk"] = {}
            sent_number += 1
```

<!-- #region editable=true slideshow={"slide_type": ""} tags=["hermeneutics"] -->
##### Try it out
The variable source can be used to choose between 3 different example transcripts to see how the import splits the OHTM file text. A distinction can be made here between TXT and CSV files.


<!-- #endregion -->

```python editable=true slideshow={"slide_type": ""}
from ohtm_pipeline.ohtm_pipeline.basic_functions.ohtm_file_creation import ohtm_file_creation_function
source_path = "./media/transcripts/interviews"
source = ["zwa"] # "adg", "wde"

ohtm_file = ohtm_file_creation_function(source = source, source_path = source_path, speaker_txt = True, folder_as_archive = True)
print(ohtm_file)

```

<!-- #region citation-manager={"citations": {"6bt6s": [{"id": "20217732/WHIQW7ZF", "source": "zotero"}], "jr22b": [{"id": "20217732/57DGI79N", "source": "zotero"}], "u1doj": [{"id": "20217732/3JIVN6SY", "source": "zotero"}], "w81g5": [{"id": "20217732/F8E46RVN", "source": "zotero"}]}} editable=true slideshow={"slide_type": ""} -->
### Balancing the package - normalization and shaping the text

Before the actual topic modeling process starts, it has proven useful to preprocess the text in its form as sentences. This involves removing punctuation marks, converting all words to lowercase, removing stop words, and lemmatizing words. The aim of this very strong intervention in the texts is to obtain semantically clear topics that are as easy to interpret as possible (<cite id="w81g5"><a href="#zotero%7C20217732%2FF8E46RVN">(Du 2024)</a></cite>, p. 26f.) Results without this preprocessing can appear very noisy and incomprehensible for human interpretation, as conjunctions and prepositions, for example, are very present in almost all topics. In Bayerschmidt et al 2025, the influence of the individual steps on the results of topic modeling on life history interviews was examined in detail (<cite id="u1doj"><a href="#zotero%7C20217732%2F3JIVN6SY">(Bayerschmidt et al. 2025)</a></cite>, p. 9-14.). However, preprocessing is not uncontroversial (see <cite id="6bt6s"><a href="#zotero%7C20217732%2FWHIQW7ZF">(Rawson and Muñoz 2019)</a></cite>) and there are suggestions not to remove stop words for the calculation of the topics in order not to anticipate these structures, but to filter them from the topic word lists only during interpretation (<cite id="jr22b"><a href="#zotero%7C20217732%2F57DGI79N">(Schofield, Magnusson, and Mimno 2017)</a></cite>). Preprocessing does not follow any set standards, as the individual options depend on the research question and the composition of the corpus. It is important to carefully weigh the individual steps, to evaluate the influences on the results and, in the end, to disclose transparently and comprehensibly why interventions and options were chosen. To foster reusability and replicability, preprocessing steps are saved in “settings”.
<!-- #endregion -->

<!-- #region editable=true slideshow={"slide_type": ""} tags=["hermeneutics"] -->
Within the pipeline, the individual archives and interviews are iterated in the preprocessing function and the records in “raw” are cleaned with the respective selected preprocessing steps and the result is saved in “cleaned”.
<!-- #endregion -->

```python editable=true slideshow={"slide_type": ""} tags=["hermeneutics"]
# This code has no function and is for illustration purposes only
def preprocessing(ohtm_file, stoplist_name: str = "",
                  allowed_postags_settings=None,
                  by_list: bool = False, by_particle: bool = False, by_threshold: bool = False, threshold: int = 0.5,
                  lemma: bool = False, pos_filter_setting: bool = False, stop_words: list = "",
                  infer_new_documents: bool = False, spacy_model: str = "", stopword_removal_by_spacy: bool = False,
                  working_folder: str = ""
                  ):

    if allowed_postags_settings is None:
        allowed_postags_settings = ['NOUN', 'PROPN', 'VERB', 'ADJ', 'NUM', 'ADV']

    ohtm_file = convert_ohtm_file(ohtm_file)

    if lemma:
        try:
            spacy_model_load = spacy.load(spacy_model, disable=['parser', 'ner'])
        except ValueError:
            print("You need a spacy model name")
            exit()
        except OSError:
            print("Your spacy model name is not correct")
            exit()
    if stopword_removal_by_spacy:
        try:
            spacy_model_load = spacy.load(spacy_model, disable=['parser', 'ner'])
            stop_list_spacy = spacy_model_load.Defaults.stop_words
        except ValueError:
            print("You need a spacy model name")
            exit()
        except OSError:
            print("Your spacy model name is not correct")
            exit()
    if by_particle:
        print("Stopwords removal by particle is not included so far")
    if by_list:
        if infer_new_documents:
            stoplist = stop_words
        else:
            stoplist = open(os.path.join(working_folder, stoplist_name), encoding='UTF-16', mode='r').read().split()
        stoplist = [word.lower()for word in stoplist]

    sent_length = []
    processed_interviews = 0
    print("Preprocessing started " + str(ohtm_file["settings"]["interviews"]["total"]) + " interviews")
    for archive in ohtm_file["corpus"]:
        for interview in ohtm_file["corpus"][archive]:
            for sent_nr in ohtm_file["corpus"][archive][interview]["sent"]:
                text = copy.deepcopy(ohtm_file["corpus"][archive][interview]["sent"][sent_nr]["raw"])
                text = str(text)
                pre_line = preprocess_outstr(text)
                data_out = pre_line.split(" ")  # Tokenization
                data_out = [word.lower() for word in data_out]
                if by_list:
                    ohtm_file["settings"]["preprocessing"].update({"stopwords_removed": "True"})
                    ohtm_file["stopwords"] = stoplist
                    data_out = remove_stopwords_by_list(data_out, stoplist)
                if stopword_removal_by_spacy:
                    data_out = [word for word in data_out if word.lower() not in stop_list_spacy]
                    stop_list = [word for word in stop_list_spacy]
                    ohtm_file["stopwords"] = stop_list
                if lemma:
                    goldlist = [""]  # Placeholder for a goldlist, to exclude words from filtering.
                    data_out_lem = lemmatization(data_out,
                                                 spacy_model_load,
                                                 goldlist,
                                                 pos_filter=pos_filter_setting,
                                                 allowed_postags=allowed_postags_settings)
                    data_out = data_out_lem
                    ohtm_file["settings"]["preprocessing"].update({"lemma": "True"})
                    ohtm_file["settings"]["preprocessing"]["pos_filter"] = pos_filter_setting
                    ohtm_file["settings"]["preprocessing"]["allowed_postags"] = allowed_postags_settings
                else:
                    ohtm_file["settings"]["preprocessing"]["pos_filter"] = False
                    ohtm_file["settings"]["preprocessing"]["allowed_postags"] = []
                ohtm_file["corpus"][archive][interview]["sent"][sent_nr]["cleaned"] = data_out
                sent_length.append(len(data_out))
            processed_interviews += 1
            print(str(processed_interviews) + " out of " + str(ohtm_file["settings"]["interviews"]["total"]) +
                  " interviews are processed")

    sent_length = [word for word in sent_length if word != 0]
    sent_length.sort()
    max_length = sent_length[-1]
    min_length = sent_length[0]
    average_length = sum(sent_length) / len(sent_length)

    # Saves the settings in the dictionary.
    ohtm_file["settings"]["preprocessing"]["cleaned_length"] = {}
    ohtm_file["settings"]["preprocessing"]["cleaned_length"]["max_length"] = max_length
    ohtm_file["settings"]["preprocessing"]["cleaned_length"]["min_length"] = min_length
    ohtm_file["settings"]["preprocessing"]["cleaned_length"]["ave_length"] = average_length
    ohtm_file["settings"]["preprocessing"]["stopwords_by_list"] = by_list
    ohtm_file["settings"]["preprocessing"]["stop_words_by_particle"] = by_particle
    ohtm_file["settings"]["preprocessing"]["stop_words_by_threshold"] = by_threshold
    ohtm_file["settings"]["preprocessing"]["stop_words_by_spacy"] = stopword_removal_by_spacy
    ohtm_file["settings"]["preprocessing"]["stop_words_by_threshold"] = threshold
    ohtm_file["settings"]["preprocessing"]["lemmatization"] = lemma
    ohtm_file["settings"]["preprocessing"]["pos_filter_setting"] = pos_filter_setting
    ohtm_file["settings"]["preprocessing"].update({"preprocessed": "True"})

    ohtm_file = json.dumps(ohtm_file, ensure_ascii=False)

    return ohtm_file
```

<!-- #region editable=true slideshow={"slide_type": ""} tags=["hermeneutics"] -->
First, all punctuation marks and unnecessary characters that are neither letters nor numbers are removed. The sentences are then separated into their individual tokens and written in lower case.

<!-- #endregion -->

```python editable=true slideshow={"slide_type": ""} tags=["hermeneutics"]
# This code has no function and is for illustration purposes only
def preprocess_outstr(text):
    text = text.lower()  # lowercasing
    text_alpha = text
    alphabet = ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M', 'N', 'O', 'P', 'Q', 'R', 'S', 'T', 'U',
                'V', 'W', 'X', 'Y', 'Z', 'Ä', 'Ö', 'Ü', 'a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k', 'l', 'm',
                'n', 'o', 'p', 'q', 'r', 's', 't', 'u', 'v', 'w', 'x', 'y', 'z', 'ä', 'ö', 'ü', '0', '1', '2', '3', '4',
                '5', '6', '7', '8', '9', 'ß', ' ', '*']
    punct_a = []   # Liste, in der Interpunktionszeichen gesammelt werden
    punct_b = ['/']   # Liste mit Schrägstrich

    for i in text_alpha:
        if i not in alphabet:
            if i not in punct_a:
                if i != '/' or '\t':
                    punct_a.append(i)
            if i in punct_a:
                continue
    text_norm = text   # Interpunktion entfernen
    for char in text_norm:
        if char in punct_a:
            text_norm = text_norm.replace(char, '')
        if char in punct_b:
            text_norm = text_norm.replace(char, ' ')

    text_clean = text_norm
    while '  ' in text_clean:
        text_clean = text_clean.replace('  ', ' ')   # überschüssige Leerzeichen entfernen

    return text_clean
```

<!-- #region citation-manager={"citations": {"5b70f": [{"id": "20217732/H66J89G4", "source": "zotero"}], "z24yv": [{"id": "20217732/3JIVN6SY", "source": "zotero"}]}} editable=true slideshow={"slide_type": ""} -->
#### Stop words removal

As interviews are a written form of spoken language, the topic-results are very noisy without the removal of stop words (<cite id="z24yv"><a href="#zotero%7C20217732%2F3JIVN6SY">(Bayerschmidt et al. 2025)</a></cite>, p. 9-21). A variety of methodologies exists for the construction of stop word lists (<cite id="5b70f"><a href="#zotero%7C20217732%2FH66J89G4">(Burns 2018)</a></cite>) The selection of words to be removed is dependent on the type of source used and the research interest. A life history interview is characterised by the presence of stop words that would not be considered stop words in other sources. These include words such as "sagen" (to say), "fragen" (to ask), "erinnern" (to remember) and the German words “Mann (man)” and “Frau (women)”. 
<!-- #endregion -->

<!-- #region editable=true slideshow={"slide_type": ""} tags=["hermeneutics"] -->
In German, the form of address for a woman is the same word as for a woman “Frau (Mrs./Ms.)”. In the final model we didn’t consider this problematic, therefore the address for man “Herr (Sir)” was not removed, leading to a possible overrepresentation of “Herr” inside the topics.
This problem highlights a weakness of the method. It is not possible to simply add a word to the stop word list and obtain a similar model. As already mentioned, the individual parameters have a considerable influence on the results. In one test, “Herr (sir)” was added to the stop word list and a model was calculated with otherwise unchanged settings. Even though the content of the topics remained largely constant, the topic allocation (which topic has which ordinal number) has changed insignificantly. In addition, a new “mix” of different topics also results in different distributions. We have carried out various studies to address this problem and couldn’t detect any deviation in content or gender bias with or without these specific words.

<!-- #endregion -->

<!-- #region editable=true slideshow={"slide_type": ""} -->
The creation of the stop word list utilised in this study began with the adaptation of two existing lists. One of these is a list provided by MaxQDA [https://www.maxqda.com/help-mx22-dictio/stop-lists], and the other is a list that was found on a GitHub repository [https://github.com/solariz/german_stopwords], which was created as part of the work with web projects and search engines. Initially, the lists were examined and adapted with respect to the research project. The combined list was used to calculate an initial model, with the first 50 topic words analysed for potential "noise words". These were then added to the stop word list. This procedure was then repeated, and the list was supplemented until a stop word list suitable for the research question was created. 
<!-- #endregion -->

<!-- #region editable=true slideshow={"slide_type": ""} tags=["hermeneutics"] -->
The stop-words can currently be removed in two different ways. One is with a separate stop-word list, which is available in the form of a TXT file and can be easily added, or by using the stop-word removal integrated in the Spacy library.
<!-- #endregion -->

```python editable=true slideshow={"slide_type": ""}
# This code has no function and is for illustration purposes only
# preprocessing
# Select just ONE of those two:
stopword_removal_by_stop_list = False
stopword_removal_by_spacy = False
if stopword_removal_by_stop_list:
    ohtm_file["settings"]["preprocessing"].update({"stopwords_removed": "True"})
    ohtm_file["stopwords"] = stoplist
    data_out = remove_stopwords_by_list(data_out, stoplist)
if stopword_removal_by_spacy:
    data_out = [word for word in data_out if word.lower() not in stop_list_spacy]
    stop_list = [word for word in stop_list_spacy]
    ohtm_file["stopwords"] = stop_list
```

<!-- #region editable=true slideshow={"slide_type": ""} -->
#### Lemmatization

As the algorithm only compares the words with each other using the character strings during the calculation of the topic model, inflected word forms are not recognized as identical but as different words. This means that the same words appear several times in different inflections in the topics. This can be solved with the help of lemmatization by tracing all words back to their basic stem. Furthermore, the words can be cleaned using part-of-speech filters (POS filters) by removing all words of a certain word type from the texts. 
<!-- #endregion -->

<!-- #region editable=true slideshow={"slide_type": ""} tags=["hermeneutics"] -->
Within the OHTM pipeline, lemmatization, as well as part-of-speech (POS) tagging and filtering, is facilitated by the SpaCy library. The aforementioned filtration process could potentially create
potential to result in complications, particularly in the context of dialectical words, which are frequently not recognised by the pipeline, erroneously assigned, and consequently eliminated. The resolution to this issue can be achieved through the establishment of a list of words that should be excluded from the filtering process. The function of an "exception list" is to be implemented in the future. As previously explained, all words are written in lower case within the pipeline. However, the lemmatization reverses this for words that are always capitalized in German. This process of capitalization appears since an update of Spacy, so the final model used for my research does not have this reversed capitalization. Nonetheless, it should be noted that this intervention exerts no influence on the topic calculation, as it was only relevant in cases where lower-case words are capitalized at the beginning of the sentence. A collateral benefit of this capitalization process is that the topic word lists become more legible, as the natural feel of capitalized words is retained. 

<!-- #endregion -->

```python editable=true slideshow={"slide_type": ""}
# This code has no function and is for illustration purposes only
def lemmatization(sentence, nlp_model, goldlist, pos_filter: bool = True,
                  allowed_postags=['NOUN', 'PROPN', 'VERB', 'ADJ', 'ADV', 'PRON','ADP', 'DET', 'AUX', 'NUM', 'SCONJ', 'CCONJ', 'X']):

    doc = nlp_model(" ".join(sentence))
    if pos_filter:
        sentence_lemmatized = [token.lemma_ for token in doc if token.pos_ in allowed_postags or token.lemma_ in goldlist]
    if not pos_filter:
        sentence_lemmatized = [token.lemma_ for token in doc]

    sentence_lemmatized_out = [word for word in sentence_lemmatized]

    return sentence_lemmatized_out
```

<!-- #region editable=true slideshow={"slide_type": ""} -->
It is evident that all the preprocessing functions presented here and contained in the pipeline represent a significant intervention in the actual texts of the corpus. The corpus employed in this study contains a total of 24,244,388 words in its "raw" entries. Following the removal of stop words, the text was lemmatized. Thereafter, the POS filters ('PRON', 'ADP', 'DET', 'AUX', 'SCONJ', 'CCONJ', 'X') were removed, leaving 480,010 words or tokens in total. This indicates that approximately 80% of the words were eliminated. This intervention is of major significance for the calculation of topic modeling to minimize noise, but it should be noted that these cleaned texts would not be suitable for a qualitative analysis of the topic modeling results. Consequently, the individual sentences within the OHTM-file are saved in both variants, once in "raw" and once in "cleaned", so that the results can always be traced back to the actual source texts.
<!-- #endregion -->

<!-- #region citation-manager={"citations": {"vxcsx": [{"id": "20217732/F8E46RVN", "source": "zotero"}]}} editable=true slideshow={"slide_type": ""} -->
### Chunking

The division of very long texts into smaller sections, so-called chunks, has the effect of enabling finer analysis and better topic results. As previously outlined, topic modeling utilizes the “bag-of-words” approach to calculate topics and to compare documents and the co-occurrence of words with each other. Maintaining the texts in their original form would result in a document exceeding 60 pages of transcript as a single bag-of-words. To address the research question, topic-document distribution will be utilized to identify sections of text in which a topic has been assigned a high weighting on “homemaking”. In the absence of chunking, the result would be the extraction of the topic-document distribution for the entire interview transcript. While this may be beneficial for specific research inquiries, it is not applicable within the scope of my own research. Chunking is a useful technique for dividing a text into smaller sections, and the topic-document distribution can provide detailed information about the individual texts and the compilation of the transcript. Chunking is a common practice in other academic disciplines, for example in literary studies. There are a variety of methods by which literary texts may be divided into sections; these include the use of individual chapters, paragraphs or pages. This methodology is predicated on the formation of thematically related units with a view to depicting and preserving specific contexts within each unit. (<cite id="vxcsx"><a href="#zotero%7C20217732%2FF8E46RVN">(Du 2024)</a></cite>, p. 17f., 26f.) Nevertheless, given that life history interviews are unstructured texts capable of containing substantial thematic leaps, there is no inherent logic in the transcripts according to which the texts can be divided. In this respect, a systematic approach is required, whereby organization is based on either a pre-defined number of words or sentences.
<!-- #endregion -->

<!-- #region editable=true slideshow={"slide_type": ""} tags=["hermeneutics"] -->
#### "raw” sentence length

It is evident that the type of chunking and the time at which the texts are chunked have a significant influence on the final chunk length. To better understand the influence, it is necessary to examine the actual length of the sentences that were created as individual "raw" entries within the OHTM file. It is apparent that there is a considerable variation in the lengths. In this graph, all sentences over 100 words have been removed.
<!-- #endregion -->

```python editable=true slideshow={"slide_type": ""} tags=["hermeneutics", "figure-raw-sentence-*"]
cut = True

from IPython.display import Image, display
if cut:
    metadata = {
        "jdh": {
            "module": "object",
            "object": {
                "type": "image",
                "source": [ "Length of each "raw" sentence in the corpus, cut above 100 words"
                ]
            }
        }
    }
    display(Image("./media/fig_raw_length_cut.png"), metadata=metadata)
else:
    metadata = {
        "jdh": {
            "module": "object",
            "object": {
                "type": "image",
                "source": [ "Length of each "raw" sentence in the corpus"
                ]
            }
        }
    }
    display(Image("./media/fig_raw_length.png"), metadata=metadata)
    
```

<!-- #region editable=true slideshow={"slide_type": ""} tags=["hermeneutics"] -->
#### “cleaned” sentence length

A similar variance can be seen in the individual sentences after preprocessing, which were saved in “cleaned”. It should be noted here that the sentences have different numbers of stop words that were previously removed. In the final model 0.46% (8243 of 1,793,325) of the cleaned sentences have more than 20 words and have been removed from the graph.
<!-- #endregion -->

```python editable=true slideshow={"slide_type": ""} tags=["hermeneutics", "figure-cleaned-sentence-*"]
# Change cut = "False" to see the uncut raw sentence length 
cut = True

from IPython.display import Image, display
if cut:
    metadata = {
        "jdh": {
            "module": "object",
            "object": {
                "type": "image",
                "source": [ "Length of each "cleaned" sentence in the corpus, cut above 20 words"
                ]
            }
        }
    }
    display(Image("./media/fig_cleaned_length_cut.png"),metadata=metadata)
else:
    metadata = {
        "jdh": {
            "module": "object",
            "object": {
                "type": "image",
                "source": [ "Length of each "cleaned" sentence in the corpus"
                ]
            }
        }
    }
    display(Image("./media/fig_cleaned_length.png"), metadata=metadata)
```

<!-- #region citation-manager={"citations": {"11eu5": [{"id": "20217732/CQ6D4YB5", "source": "zotero"}]}} editable=true slideshow={"slide_type": ""} tags=["hermeneutics"] -->
#### Chunkin by sentences

The formation of individual chunks according to the number of sentences results in a range of 20 to 300 words, with an average of 25 sentences per chunk. In previous research, it was demonstrated that 25 sentences constituted an optimal number for the subdivision of interviews. (<cite id="11eu5"><a href="#zotero%7C20217732%2FCQ6D4YB5">(Hodel, Möbus, and Serif 2022b)</a></cite>, p. 198) However, this chunking was carried out using the "raw" sentences, i.e. the sentences prior to preprocessing. In order to ensure an ideal calculation of the topic model, it is recommended that the chunks be of similar length. Chunking based on sentences means that the chunks consist of different numbers of tokens. This phenomenon is clearly illustrated in the following graphic, in which chunks containing 25 sentences each were formed. In the final model 0.68% (492 of 72,243) of the chunks consist of more than 300 words and were removed from the graphic (cut = “True”).
<!-- #endregion -->

```python editable=true slideshow={"slide_type": ""} tags=["figure-chunk-*"]
# Change cut = "False" to see the uncut raw sentence length 
cut = True

from IPython.display import Image, display
if cut:
    metadata = {
        "jdh": {
            "module": "object",
            "object": {
                "type": "image",
                "source": [ "Length of each chunk by adding 25 sentences, cut above 300 words"
                ]
            }
        }
    }
    display(Image("./media/fig_chunk_by_sentence_length_cut.png"), metadata=metadata)
else:
    metadata = {
        "jdh": {
            "module": "object",
            "object": {
                "type": "image",
                "source": [ "Length of each chunk by adding 25 sentences"
                ]
            }
        }
    }
    display(Image("./media/fig_chunk_by_sentence_length.png"), metadata=metadata)
```

<!-- #region editable=true slideshow={"slide_type": ""} tags=["hermeneutics"] -->
#### Chunking by words

The preceding considerations and results have resulted in a novel approach to chunking within this pipeline. With the objective of obtaining pre-processed chunks of identical size, thereby facilitating the calculation of topic modeling on chunks of uniform length. Chunking is only performed after preprocessing, which involves the integration of sentences based on their word count. This approach ensures a uniform distribution of words across the chunks. During chunking, complete sentences are always considered and the chunks are only formed within an interview not across multiple interviews.  In addition to the fixed chunk size, a threshold of chunk size plus one-fifth of the chunk size is established. This enables the chunk to contain a greater number of words than specified. This allows fluctuations in sentence length in successive sentences to be balanced out. In the context of a word count of 50, a segment would contain a maximum of 35 words, provided that the subsequent sentence contains more than 15 words. However, given the requirement for sentences to be arranged in a predetermined sequence, these fluctuations must be taken into consideration. It is important to note that the chunks themselves are not saved in the OHTM file; however, each sentence is assigned the number of the chunk as a property in which it is located after compilation. 
<!-- #endregion -->

```python editable=true slideshow={"slide_type": ""} tags=["hermeneutics"]
# This function has no output in this fiedl and 
def chunking(ohtm_file, chunk_setting: int = 0):
    ohtm_file = convert_ohtm_file(ohtm_file)
    if chunk_setting != 0:
        for archive in ohtm_file["corpus"]:
            for interview in ohtm_file["corpus"][archive]:
                chunk_count = 0
                chunk_data = []
                for nr in range(1, (len(ohtm_file["corpus"][archive][interview]["sent"]) + 1)):
                    new_sent = copy.deepcopy(ohtm_file["corpus"][archive][interview]["sent"][str(nr)]["cleaned"])
                    if len(chunk_data) + len(new_sent) >= chunk_setting:
                        if len(chunk_data) + len(new_sent) >= chunk_setting + (chunk_setting/5):
                            chunk_count += 1
                            ohtm_file["corpus"][archive][interview]["sent"][str(nr)]["chunk"] = chunk_count
                            chunk_data = new_sent
                        else:
                            ohtm_file["corpus"][archive][interview]["sent"][str(nr)]["chunk"] = chunk_count
                            chunk_data += ohtm_file["corpus"][archive][interview]["sent"][str(nr)]["cleaned"]
                            chunk_count += 1
                            chunk_data = []
                    else:
                        ohtm_file["corpus"][archive][interview]["sent"][str(nr)]["chunk"] = chunk_count
                        chunk_data += new_sent

        ohtm_file["settings"]["preprocessing"].update({"chunk_setting": chunk_setting})
        ohtm_file["settings"]["preprocessing"].update({"chunked": "True"})

        ohtm_file = json.dumps(ohtm_file, ensure_ascii=False)
    else:
        for archive in ohtm_file["corpus"]:
            for interview in ohtm_file["corpus"][archive]:
                for nr in ohtm_file["corpus"][archive][interview]["sent"]:
                    ohtm_file["corpus"][archive][interview]["sent"][str(nr)]["chunk"] = 0
    return ohtm_file
```

<!-- #region editable=true slideshow={"slide_type": ""} tags=["hermeneutics"] -->
It is possible to achieve an equal distribution of words per chunk, as well as an equal size for all the chunks, through the process of chunking. A mere 0.22% (103 of 47,255) of the chunks have more than 120 words and are therefore above the threshold set in the function. This has been removed from the graph (cut = “True”). The 4.15% (2771 of 47,255) of the chunks that have fewer than the set number of words are a result of the ends of the transcripts. The statistical calculation of co-occurring words and the topic-document distribution of topic modeling results can be calculated with this approach on equally sized chunks or documents. 
<!-- #endregion -->

```python editable=true slideshow={"slide_type": ""} tags=["hermeneutics", "figure-chunk-100-*"]
# Change cut = "False" to see the uncut raw sentence length 
cut = True

from IPython.display import Image, display
if cut:
    metadata = {
        "jdh": {
            "module": "object",
            "object": {
                "type": "image",
                "source": [ "Length of each chunk by adding 100 words, cut above 120 words"
                ]
            }
        }
    }
    display(Image("./media/fig_chunks_by_words_length_cut.png"), metadata=metadata)
else:
    metadata = {
        "jdh": {
            "module": "object",
            "object": {
                "type": "image",
                "source": [ "Length of each chunk by adding 100 words"
                ]
            }
        }
    }
    display(Image("./media/fig_chunks_by_words_length.png"), metadata=metadata)
```

<!-- #region editable=true slideshow={"slide_type": ""} tags=["hermeneutics"] -->
It should be noted that an error occurred during the process of creating the final OHTM-file. This error manifested itself in the import of some transcripts and the subdivision of these transcripts into individual sentences. The error comes from the automatic time alignment, and results in a large number of sentences being assigned to a single time code. Consequently, individual sentences have been known to extend beyond 100 words, with some reaching a maximum length of 3000 words. It is unfortunate that the error became apparent only at a point at which it was no longer possible to remove it from the model. One method of correcting this issue in the analysis is outlined in the chapter entitled "Inferring". However, this phenomenon only impacts 0.37% (6640 of 1,793,325) of all "raw" sentences. Despite the negligible impact of this on the model's calculations, it does have a significant impact on the subsequent explanations, distorting their representation. To ensure the visualization of the respective points was meaningful, the sentences which exceeded the specified threshold value were excluded from the analysis. Nevertheless, to maximize transparency, the graphs are also available in an unaltered form. In this instance, it is sufficient to set the variable cut to "False" in the respective functions.
<!-- #endregion -->

<!-- #region citation-manager={"citations": {"3rsur": [{"id": "20217732/HGJPHBR2", "source": "zotero"}], "5ia7q": [{"id": "20217732/F8E46RVN", "source": "zotero"}], "sp82q": [{"id": "20217732/HGJPHBR2", "source": "zotero"}]}} editable=true slideshow={"slide_type": ""} -->
There is a strong correlation between the size of the chunks and the number of topics selected, since the calculation of topics and their weighting is dependent, whether a coherent narrative – and thus coherent words – occurs in one segment or is divided into several. The appropriate chunk length is equivalent to the configuration of the relevant preprocessing parameters; there is no obvious correct approach. The evaluation of the results and the comparison of the various settings must be conducted. The research question also plays a pivotal role in this consideration. In the context of my research, which focuses on narrative passages on a specific subject, smaller fragments are more convenient to the identification of specific content than larger ones. In the process of calculating the final model, the study compared different chunk sizes (50, 100, 150 words) for 80 topics. It was concluded by the study that the topics remained constant despite varying chunk sizes and that there were no significant changes. Only the mixture of the different topics with each other changed slightly due to the different sizes, but the topics themselves remained the same. (<cite id="3rsur"><a href="#zotero%7C20217732%2FHGJPHBR2">(Bayerschmidt and Möbus 2025)</a></cite>, p. 103-105)

The findings of this study indicated that the chunk size does not have a significant impact on the quality of the topic, and that it should rather be determined by the researcher's area of interest. (<cite id="sp82q"><a href="#zotero%7C20217732%2FHGJPHBR2">(Bayerschmidt and Möbus 2025)</a></cite>) This raises the question of whether the assumption of the presented chunking approach has any measurable influence on the topic modeling results. It is hypothesized that the limits of 50, 100 and 150 words are too similar to enable a reliable assessment.
In his study (chunk lengths ranging from 10 to 1700 words in 23 subdivisions), Keli Du concluded that the evaluation of topic modeling results based on chunk length does not provide a clear answer. Despite the increase in the number of non-coherent topics with the length of the chunks, the most coherent topics were calculated in models with longer chunks. As correctly observed, modifying the chunk size also results in a corresponding alteration in the number of chunks. The reduction in the size of the chunks is directly proportional to the increase in the number of individual chunks. Consequently, the calculation of the topic model is invariably based on a distinct total number of documents or chunks. Du revealed that the observed differences between the models are not yet fully understood, and further research is required to determine whether these differences depend on the size or number of chunks. (<cite id="5ia7q"><a href="#zotero%7C20217732%2FF8E46RVN">(Du 2024)</a></cite>, p. 121f., 195f.)




<!-- #endregion -->

<!-- #region citation-manager={"citations": {"espj4": [{"id": "20217732/HGJPHBR2", "source": "zotero"}]}} editable=true slideshow={"slide_type": ""} -->
## 3.5.	Searching the Corpus – Processing Topic Modeling

A topic model may be calculated within the processing of new documents, or alternatively, an already calculated topic model may be used to enrich the content of new documents (an approach known as "inferring"). As previously indicated in the chapter on topic modeling, there are some significant parameters that must be preset in advance before commencing topic modelling.
For the final model, we used a qualitative approach, as described in the chapter on topic modeling, to determine the various parameters and, above all, the final number of topics. (<cite id="espj4"><a href="#zotero%7C20217732%2FHGJPHBR2">(Bayerschmidt and Möbus 2025)</a></cite>) My final model has the following specifications:
<!-- #endregion -->

<!-- #region jdh={"module": "object", "object": {"source": ["Settings and Specifications of the used topic model"]}} tags=["table-3"] -->
| Setting | Value | 
|----------|----------:|
| Topics   | 100   | 
| Alpha   | 5   | 
| optimize_interval_mallet   | 500   | 
| iterations_mallet   | 5000  | 
| random_seed_mallet   | 100   | 
| stopwords_removed   | yes   | 
| lemmatized   | yes   | 
| allowed_postags   |  'NOUN', 'PROPN', 'VERB', 'ADJ', 'NUM', 'ADV'   | 
| chunking  | 100 Words per Chunks   | 
<!-- #endregion -->

<!-- #region editable=true slideshow={"slide_type": ""} tags=["hermeneutics"] -->
### Topic Training

The function first reads the individual chunks from the OTHM file by iterating the individual records and forming the chunks based on the records and the matching chunk number. To guarantee the capacity to retrieve the results at a later stage, each segment is assigned an identifier comprising the interview name and the chunk number and is furthermore appended to a list as a tuple. In the context of topic modeling, the transfer of data occurs exclusively for the list of tokens, with the ID excluded. It is evident that the order in which the results and the topic document distribution are output corresponds with the order of the transferred list. Consequently, the results can then be reassembled according to their order. All results, such as topic words, topic document distribution, and the parameters, are then saved in the OHTM-file.

<!-- #endregion -->

```python editable=true slideshow={"slide_type": ""} tags=["hermeneutics"]
"""
This function calculates the topic model. The mallet_wrapper is based on the gensim wrapper.
The function was deleted in the Version 10. But the developers allowed to copy the wrapper.
See: https://github.com/piskvorky/gensim/releases/tag/4.0.0

Mallet cant handle spaces in patch strings. That's why I set the os.chdri for this patch with the space, if
the model is saved.
"""
from os import environ
import ohtm_pipeline.ohtm_pipeline.mallet_wrapper.corpora as corpora
from ohtm_pipeline.ohtm_pipeline.mallet_wrapper.ldamallet import LdaMallet
from ohtm_pipeline.ohtm_pipeline.mallet_wrapper.coherencemodel import CoherenceModel
import json
import os
from ohtm_pipeline.ohtm_pipeline.basic_functions.convert_ohtm_file import convert_ohtm_file


def topic_training_mallet(ohtm_file, topics, mallet_path,
                          optimize_interval_mallet: int = 500, iterations_mallet: int = 5000,
                          random_seed_mallet: int = 100, alpha: int = 5,
                          save_model: bool = False, working_folder: str = "",
                          save_name: str = "", save_json: bool = False,
                          ):
    if save_model:
        if save_json:
            if not os.path.exists(os.path.join(working_folder, "Models")):
                os.makedirs(os.path.join(working_folder, "Models"))
            if not os.path.exists(os.path.join(working_folder, "Models", save_name)):
                os.makedirs(os.path.join(working_folder, "Models", save_name))
            os.chdir(os.path.join(working_folder, "Models", save_name))
            prefix_value = save_name + "_"
        else:
            print("You need to set a save_name and set the option save_ohtm_file to True to save the model")
            exit()
    else:
        prefix_value = None

    ohtm_file = convert_ohtm_file(ohtm_file)

    # The single sentences are added together to the preprocessed chunks:
    chunk_data = []
    for a in ohtm_file["corpus"]:
        for i in ohtm_file["corpus"][a]:
            chunk_count = 0
            chunk_text = []
            for n in range(1, (len(ohtm_file["corpus"][a][i]["sent"]) + 1)):
                n = str(n)
                if ohtm_file["corpus"][a][i]["sent"][n]["chunk"] == chunk_count:
                    chunk_text += ohtm_file["corpus"][a][i]["sent"][n]["cleaned"]
                    if n == str((len(ohtm_file["corpus"][a][i]["sent"]))):
                        chunk_data += [[a + "%" + i + " chunk*" + str(chunk_count), chunk_text]]
                else:
                    chunk_data += [[a + "%" + i + " chunk*" + str(chunk_count), chunk_text]]
                    chunk_count += 1
                    chunk_text = []
                    chunk_text += ohtm_file["corpus"][a][i]["sent"][n]["cleaned"]
    print(chunk_data[:10])
    dataset = []
    for i in chunk_data:
        dataset += [i[1]]
    print(dataset[:10])
    print("LDA started")
    id2word = corpora.Dictionary(dataset)
    corpus = [id2word.doc2bow(text) for text in dataset]

    lda_model_mallet = LdaMallet(mallet_path=mallet_path,
                                 corpus=corpus,
                                 id2word=id2word,
                                 num_topics=topics,
                                 alpha=alpha,
                                 iterations=iterations_mallet,
                                 optimize_interval=optimize_interval_mallet,
                                 random_seed=random_seed_mallet,
                                 prefix=prefix_value
                                 )

    if save_model:
        lda_model_mallet.save(os.path.join(working_folder, "Models", save_name, (save_name + "_topic_model")))

    # Converting the results and saving them in the dictionary.
    doc_tops_import = open(lda_model_mallet.fdoctopics(), mode='r', encoding='UTF-8').read()
    doc_tops_mallet = []
    sum_top_weights = 0.0
    top_counter = 0
    min_weight_mallet = 1
    max_weight_mallet = 0
    for line in doc_tops_import.splitlines():
        doc_tops_transfer = []
        for topic_nr, topic in enumerate(line.split()):
            if '.' in topic:
                topic_float = float(topic)
                if topic_float >= 0:  # Threshold for weight
                    sum_top_weights = sum_top_weights + topic_float
                    top_counter += 1
                    doc_tops_transfer.append((topic_nr - 2, topic_float))
                    if topic_float < min_weight_mallet:
                        min_weight_mallet = topic_float
                    if topic_float > max_weight_mallet:
                        max_weight_mallet = topic_float
        doc_tops_mallet.append(doc_tops_transfer)

    average_weight_mallet = sum_top_weights / top_counter

    topwords_mallet = lda_model_mallet.print_topics(num_topics=topics, num_words=1000)

    coherence_model_ldamallet = CoherenceModel(model=lda_model_mallet,
                                               texts=dataset, dictionary=id2word, coherence='c_v')
    coherence_ldamallet = coherence_model_ldamallet.get_coherence()

    # The results are written in the dictionary.
    for i in range(len(doc_tops_mallet)):
        archive = chunk_data[i][0].split("%")[0]
        interview = chunk_data[i][0].split("%")[1].split(" ")[0]
        interview_chunk = chunk_data[i][0].split("*")[1]
        if archive not in ohtm_file["weight"]:
            ohtm_file["weight"][archive] = {}
        if interview not in ohtm_file["weight"][archive]:
            ohtm_file["weight"][archive][interview] = {}
        if interview_chunk not in ohtm_file["weight"][archive][interview]:
            ohtm_file["weight"][archive][interview][interview_chunk] = {}
        for a in doc_tops_mallet[i]:
            ohtm_file["weight"][archive][interview][interview_chunk][a[0]] = a[1]

    # The results from top_words_mallet for every topic are listed as: (0.000*"zetteln" + 0.000*"sozialisten").
    # We have to split the words at "+" and then split the words from the weight to have a tuple (value, word).

    word_list_splitted = []
    for i in topwords_mallet:
        word_list_splitted += [(i[0], i[1].split("+"))]
    for a in word_list_splitted:
        word_weight_splitted = []
        for b in a[1]:
            c = float(b.split("*")[0])
            d = ((b.split("*")[1]).split('"')[1::2])[0]
            word_weight_splitted += [(c, d)]
        ohtm_file["words"][a[0]] = word_weight_splitted

    for archive in ohtm_file["corpus"]:
        for interviews in ohtm_file["corpus"][archive]:
            ohtm_file["corpus"][archive][interviews]["model_base"] = "trained"

    # Saving metadata and variables.
    ohtm_file["settings"]["topic_modeling"].update({"trained": "True"})
    ohtm_file["settings"]["topic_modeling"].update({"model": "mallet"})
    ohtm_file["settings"]["topic_modeling"].update({"topics": topics})
    ohtm_file["settings"]["topic_modeling"].update({"alpha": alpha})
    ohtm_file["settings"]["topic_modeling"].update({"optimize_interval_mallet": optimize_interval_mallet})
    ohtm_file["settings"]["topic_modeling"].update({"iterations_mallet": iterations_mallet})
    ohtm_file["settings"]["topic_modeling"].update({"random_seed_mallet": random_seed_mallet})
    ohtm_file["settings"]["topic_modeling"].update({"coherence": coherence_ldamallet})
    ohtm_file["settings"]["topic_modeling"].update({"average_weight": average_weight_mallet})
    ohtm_file["settings"]["topic_modeling"].update({"min_weight": min_weight_mallet})
    ohtm_file["settings"]["topic_modeling"].update({"max_weight": max_weight_mallet})

    print("Topic modeling and ohtm_file enrichment finished")

    ohtm_file = json.dumps(ohtm_file, ensure_ascii=False)
    return ohtm_file

```

<!-- #region editable=true raw_mimetype="" slideshow={"slide_type": ""} tags=["hermeneutics"] -->
### Topic Inferring

If one wishes to enrich documents or interviews that were not part of the training corpus with the results of a calculated topic model, one may use the inferring function. In this instance, the topics and their respective word distributions, which have been calculated previously, are utilized to determine the topic-document distribution for the new documents. In order to execute this process, it is imperative to consider several factors within the pipeline. Firstly, during the original topic modeling calculation, it is necessary to set the setting save_model to "True". 
Until now, it was not possible to integrate the model itself into the OHTM file, which is why it is stored separately. The mallet_wrapper saves the model files as binary files (.mallet) for the java application “.mallet”. With that inclusion it is not that easy, especially with the guarantee to import the .mallet files again into the application. To infere new interviews, it is necessary to select the option infer_new_documents in main.py and to choose the OHTM-file of the original model. The pipeline is then used as usual by selecting the folders with the interviews. The decision of whether to save new interviews separately or to integrate them into the original OHTM file is also available to the user. Subsequently, the pipeline loads the new interviews and performs all preprocessing steps based on the saved settings of the original topic model, which is read from the OHTM file. To trace whether an individual interview was part of the model calculation or the enrichment for merged OHTM files, this status is added to the interviews as an entry and supplemented in the settings.

<!-- #endregion -->

```python editable=true slideshow={"slide_type": ""} tags=["hermeneutics"]
from ohtm_pipeline.ohtm_pipeline.mallet_wrapper.ldamallet import LdaMallet
from ohtm_pipeline.ohtm_pipeline.basic_functions.convert_ohtm_file import convert_ohtm_file
import json
import os



def topic_inferring(ohtm_file,
                    mallet_path: str = "", model_name: str = "", working_folder: str = "",
                    topics: int = 0, iterations_mallet: int = 5000, random_seed_mallet: int = 100):

    # Load the train model and set all necessary variables.
    model_path = os.path.join(working_folder, "Models", model_name, model_name+"_")
    lda_model_mallet = LdaMallet.load(model_path+"topic_model")
    os.chdir(os.path.join(working_folder, "Models", model_name))
    lda_model_mallet.prefix = model_name + "_"
    lda_model_mallet.random_seed = random_seed_mallet

    # The single sentences are added together to the preprocessed chunks:
    ohtm_file = convert_ohtm_file(ohtm_file)

    chunk_data = []
    for a in ohtm_file["corpus"]:
        for i in ohtm_file["corpus"][a]:
            chunk_count = 0
            chunk_text = []
            for n in range(1, (len(ohtm_file["corpus"][a][i]["sent"]) + 1)):
                n = str(n)
                if ohtm_file["corpus"][a][i]["sent"][n]["chunk"] == chunk_count:
                    chunk_text += ohtm_file["corpus"][a][i]["sent"][n]["cleaned"]
                    if n == str((len(ohtm_file["corpus"][a][i]["sent"]))):
                        chunk_data += [[a + "%" + i + " chunk_" + str(chunk_count), chunk_text]]
                else:
                    chunk_data += [[a + "%" + i + " chunk_" + str(chunk_count), chunk_text]]
                    chunk_count += 1
                    chunk_text = []
                    chunk_text += ohtm_file["corpus"][a][i]["sent"][n]["cleaned"]

    dataset = []
    for i in chunk_data:
        dataset += [i[1]]

    print("Starting inferring")

    corpus = [lda_model_mallet.id2word.doc2bow(text) for text in dataset]
    lda_model_mallet[corpus]
    # Converting the results and saving them in the dictionary.
    doc_tops_import = open(lda_model_mallet.fdoctopics() + ".infer", mode='r', encoding='UTF-8').read()

    doc_tops_mallet = []
    sum_top_weights = 0.0
    top_counter = 0
    min_weight_mallet = 1
    max_weight_mallet = 0
    for line in doc_tops_import.splitlines():
        if line.startswith("#doc"):  # The .infer doc has a headline that starts with #doc and has to be skipped
            continue
        doc_tops_transfer = []
        for topic_nr, topic in enumerate(line.split()):
            if '.' in topic:
                topic_float = float(topic)
                if topic_float >= 0:  # Threshold für Weight
                    sum_top_weights = sum_top_weights + topic_float
                    top_counter += 1
                    doc_tops_transfer.append((topic_nr - 2, topic_float))
                    if topic_float < min_weight_mallet:
                        min_weight_mallet = topic_float
                    if topic_float > max_weight_mallet:
                        max_weight_mallet = topic_float
        doc_tops_mallet.append(doc_tops_transfer)

    average_weight_mallet = sum_top_weights / top_counter

    topwords_mallet = lda_model_mallet.print_topics(num_topics=topics, num_words=1000)

    # The results are written in the dictionary.
    for i in range(len(doc_tops_mallet)):
        archive = chunk_data[i][0].split("%")[0]
        interview = chunk_data[i][0].split("%")[1].split(" ")[0]
        interview_chunk = chunk_data[i][0].split("_")[1]
        if archive not in ohtm_file["weight"]:
            ohtm_file["weight"][archive] = {}
        if interview not in ohtm_file["weight"][archive]:
            ohtm_file["weight"][archive][interview] = {}
        if interview_chunk not in ohtm_file["weight"][archive][interview]:
            ohtm_file["weight"][archive][interview][interview_chunk] = {}
        for a in doc_tops_mallet[i]:
            ohtm_file["weight"][archive][interview][interview_chunk][a[0]] = a[1]

    # The results from top_words_mallet for every topic are listed as: (0.000*"zetteln" + 0.000*"sozialisten").
    # We have to split the words at "+" and then split the words from the weight to have a tuple (value, word).
    word_list_splitted = []
    for i in topwords_mallet:
        word_list_splitted += [(i[0], i[1].split("+"))]
    for a in word_list_splitted:
        word_weight_splitted = []
        for b in a[1]:
            c = float(b.split("*")[0])
            d = ((b.split("*")[1]).split('"')[1::2])[0]
            word_weight_splitted += [(c, d)]
        ohtm_file["words"][a[0]] = word_weight_splitted

    for archive in ohtm_file["corpus"]:
        for interviews in ohtm_file["corpus"][archive]:
            ohtm_file["corpus"][archive][interviews]["model_base"] = "inferred"

    # Saving metadata and variables.
    ohtm_file["settings"]["topic_modeling"]["inferred"] = "True"
    ohtm_file["settings"]["topic_modeling"]["trained"] = "True"
    ohtm_file["settings"]["topic_inferred"] = {}
    ohtm_file["settings"]["topic_inferred"]["infer_model"] = model_name
    ohtm_file["settings"]["topic_inferred"].update({"model": "mallet"})
    ohtm_file["settings"]["topic_inferred"].update({"topics": topics})
    ohtm_file["settings"]["topic_inferred"].update({"iterations_mallet": iterations_mallet})
    ohtm_file["settings"]["topic_inferred"].update({"average_weight": average_weight_mallet})
    ohtm_file["settings"]["topic_inferred"].update({"min_weight": min_weight_mallet})
    ohtm_file["settings"]["topic_inferred"].update({"max_weight": max_weight_mallet})

    ohtm_file = json.dumps(ohtm_file, ensure_ascii=False)
    return ohtm_file

```

<!-- #region editable=true slideshow={"slide_type": ""} tags=["hermeneutics"] -->
A detailed analysis and evaluation of the inference would go beyond the scope of this article, so I would just like to share one observation. For an experiment, I enriched the corpus on which the model was based with the model. The preprocessing remained identical. My assumption was that the enrichment would lead to identical topic-document distributions as in the calculated model. To compare the results, I first added up all the topic values of each individual chunk to obtain the topic distribution for the entire corpus. In the next step, I calculated the percentage deviation of the enriched result from the original result for each topic and plotted it on a line graph. This graph shows that the topic distribution is basically the same, but there are minimal deviations.

<!-- #endregion -->

```python editable=true slideshow={"slide_type": ""} tags=["hermeneutics", "figure-inferring-*"]
from IPython.display import Image, display
metadata = {
    "jdh": {
        "module": "object",
        "object": {
            "type": "image",
            "source": [ "Procentual weightchange of topics after inferring"
            ]
        }
    }
}
display(Image("./media/inferring.png"), metadata=metadata)

```

<!-- #region editable=true slideshow={"slide_type": ""} -->
## Exploring the Results – Topics, Weights and Chunks

Following the calculation of a definitive topic model, the subsequent analysis of the results and the search for narratives on “Heimat” can be conducted with greater precision. This is due to the fact that, as previously outlined, the analysis begins with the identification of appropriate parameters, rather than following the calculation of the final topic model. The iterative evaluation of the various models and the cursory examination of the results in the text passages can already lead to information on the research interest. A few topics and word lists were identified that were thematically related to "Beheimatung". The matching chunks contained text passages of interest, including narratives on the themes of home and homemaking. These could be used as markers to observe the allocation of topics in different models. Furthermore, during the compilation of the corpus, the individual interviews were examined, and several intriguing passages were identified. This information is beneficial for the analysis and has already emerged during the application of topic modeling. For the analysis of the final model, there are various approaches according to which the topics and the topic-document distribution can be analyzed: Interpretation of topic words, corpus distribution of topics, topic-document distribution, and topic distribution within individual chunks.

<!-- #endregion -->

<!-- #region editable=true slideshow={"slide_type": ""} -->
### Finding “Heimat” in Topics

The initial approach involves the interpretation of the topics through the utilization of topic word lists. In order to research my corpus for traces of a specific issue, it is important to interpret not only the thematically appropriate topics, but all 100 topics.
<!-- #endregion -->

<!-- #region editable=true slideshow={"slide_type": ""} tags=["hermeneutics"] -->
The save_topic_words function is designed to read the topic words saved in "words" inside the OHTM file and output them as a TXT file. As the words were saved as tuples with an assigned weight, they can be separated to enhance readability.
<!-- #endregion -->

```python editable=true slideshow={"slide_type": ""} tags=["hermeneutics"]
def save_topic_words(ohtm_file, working_folder: str = "", save_name: str = "", number_of_words: int = 50):
    ohtm_file = convert_ohtm_file(ohtm_file)
    if ohtm_file["settings"]["topic_modeling"]["trained"] == "True":
        out = open(os.path.join(working_folder, save_name + "_topic_words_" + str(number_of_words)
                                + "_words" + '.txt'), 'w', encoding='UTF-8')
        for top_words in ohtm_file["words"]:
            out_line = []
            for i in range(number_of_words):
                out_line.append((ohtm_file["words"][top_words])[i][1])
            out.write(str(top_words) + " ")
            out.write(str(out_line) + "\n")
            out.write("\n")
        out.close()
    else:
        print("No Topic Model trained")
```

<!-- #region editable=true slideshow={"slide_type": ""} tags=["hermeneutics"] -->
##### Try it out:
The variable “topic” can be used to select different topics from 0 to 100, while “word_number” determines how many words from the topic word list are output. If you set the variable ‘weight’ to “True,” the words are output together with their weighting.
Since these are German terms, an English version of the topic word lists was created using Deepl and added to the OHTM file. The research data contains the first 50 words for each topc, which are always displayed together with the English translation. 

<!-- #endregion -->

```python editable=true slideshow={"slide_type": ""} tags=["hermeneutics"]
# Select the topic and the number of words you want to print:
topic = 5
word_number = 20
# Select weight = True if you want so see the weight per word
weight = False

output_folder: str = (r"./media")
load_file_name = "jdh_ohtm_pipeline_final_version"
ohtm_file = load_json_function(load_file_name, output_folder)
if weight: 
    print(ohtm_file["words"][str(topic)][:word_number])
else:
    data_print = []
    word_data = ohtm_file["words"][str(topic)][:word_number]
    for word in word_data:
        data_print.append(word[1])
    print(data_print)

```

<!-- #region citation-manager={"citations": {"909ml": [{"id": "20217732/TRDTP98G", "source": "zotero"}], "tfu9o": [{"id": "20217732/38BJ66LM", "source": "zotero"}]}} editable=true slideshow={"slide_type": ""} -->
The analysis revealed three central topics that correspond with “Heimat” due to their semantic and thematic similarities, as well as the words they use.

Topic 85 [flüchtling (refugee), ort (place), leipzig (Leipzig), berlin (Berlin), dorf (village), dresden (Dresden), westen (west), heimat (homeland), grenze (border), thüringen (Thuringia), wohnen (to live), stadt (city), flucht (escape), bauer (farmer), sachsen (Saxony), kilometer (kilometre), hamburg (Hamburg), 45 (45), hannover (Hanover), drüben (over there), schlesien (Silesia), bad (bath), mutter (mother), tag (day), flüchten (to flee), familie (family), ostpreuß (East Prussia), richtung (direction), rüber (across), woche (week)]

In addition to the term "heimat (home)", Topic 85 also contains words such as "grenze (border)", " flüchtling (refugee)", “flüchten (to flee)", "aufnehmen (include)", "gehören (belong)", "wohnen (living)", which can be contextually understood in relation to flight and expulsion. The numerical value of "45" and the geographical location of East Prussia are indicative of this context at the end of the Second World War. Even if this is not a classic case of migration, it is still possible to find stories about the loss of the old “Heimat” and the finding of a new one. In further analysis and interpretation, the results must be placed in their historical context.

Topic 4 [hamburg (Hamburg), italienisch (Italian), italiener (Italian [person]), italien (Italy), deutsch (German), hamburger (Hamburger), firma (company), arbeiter (worker), bahn (railway), deutschland (Germany), mitarbeiter (employee), spät (late), herr (Mr. / gentleman), altona (Altona), ausländer (foreigner), konsulat (consulate), harburg (Harburg), ausländisch (foreign), lübeck (Lübeck), sogenannter (so-called), gewohnen (to be used to), barmbek (Barmbek), eppendorf (Eppendorf), arbeit (work), bahnhof (train station), kühn (bold / brave), organisieren (to organize), ipuf (ipuf), weltkrieg (world war), tätigkeit (activit)]

The fourth topic is characterised by a strong presence of words related to the city of Hamburg, Italy, and work. The term "gastarbeiter (guest worker)" (Word Nr. 37) suggests that the topic under discussion relates to guest workers from Italy who were employed in Hamburg, potentially during the Italy guestworkers in Germany between the 1960s and 1970s. (<cite id="tfu9o"><a href="#zotero%7C20217732%2F38BJ66LM">(Sala 2007)</a></cite>) By compiling the corpus and asking the individual archives, I know which collection this topic is made up of. The Werkstatt der Erinnerung provided me with interviews from a project involving Italian guest workers in Hamburg. Given that the interviews were conducted in German, it is plausible that these former guest workers have since resided in Germany. This makes it an interesting topic for my research question, even if the word "heimat (home)" is not part of the 1000 topic words.

44 [deutsch (German), polen (Poland), deutschland (Germany), polnisch (Polish), sprache (language), russisch (Russian), pole (Pole [Polish person]), lernen (to learn), land (country), deutsche (German [person]), familie (family), russland (Russia), friedland (Friedland), türkei (Turkey), stadt (city), russe (Russian [person]), heimat (homeland), ausländer (foreigner), türkisch (Turkish), grenze (border), schule (school), türke (Turk [Turkish person]), wohnen (to live), richtig (correct), kennen (to know [someone]), zeit (time), sowjetunion (Soviet Union), litauen (Lithuania), besuchen (to visit), anfang (beginning)]

The subject of Topic 44 involves a multitude of terms that can be contextualised within the themes of migration, arrival and home. In addition to the list of different countries, the words “grenze (border)”, “ausländer (foreigner)" and "staatsbürgerschaft (citizenship)" show that it can be about a movement from the countries mentioned to Germany. The following words can be related to relevant content in the texts under the “Beheimatung” complex: “heimat (homeland)”, “lernen (to learn)”, “wohnen (to live)”, “kennen (to know [someone])”, “anfangen (to begin / to start)”, “gehören (to belong)”, “fühlen (to feel), zuhause (home)”, “Kultur (culture)”, “verschieden (different)” and “problem (problem)”. Part of this topic also seems to be the subject of language in forms of learning or problems. “flüchtling (refugee)” and “friedland (friedland)” indicate a reference to the Friedland border transit camp. (<cite id="909ml"><a href="#zotero%7C20217732%2FTRDTP98G">(Museum Friedland 2017)</a></cite>) This topic could therefore largely relate to people who immigrated to Germany via Friedland as ethnic German repatriates.
Now that we know which topics our model has and which topics are relevant to the research question, it is worth looking at the distribution of the topics across the corpus. The use of a bar chart can facilitate the understanding of the data.

<!-- #endregion -->

<!-- #region editable=true slideshow={"slide_type": ""} -->
#### Visualizing the corpus’ topics 

The bar chart provides a comprehensive overview of the topic distribution across the entire corpus, as well as an analysis of the distribution within the individual archives. The legend can be used to select or deselect individual archives and thus display the topic distribution in individual archives. A more detailed examination of the distribution of the individual archives reveals that Topic 4 is the most prominent within the Werkstatt der Erinnerung archive. The preceding assumption appears to be valid: Topic 4 pertains to the subjects of the interviews in the "Italiener in Hamburg" collection of the Werkstatt der Erinnerung. However, there are also hits in the ADG archive. Topic 85 is strongest within the ADG archive but can also be found in the ZWA archive. The subject of Topic 44 is distributed across the MFL, ADG and ZWA archives, and, to a lesser extent, in WdE. In accordance with the assumption previously outlined, it is evident that this subject is by far the most dominant topic in the MFL archive. However, the overall distribution indicates that the topic is also present in other archives.
<!-- #endregion -->

```python editable=true slideshow={"slide_type": ""} tags=["hidden"]
output_folder: str = (r"./media")
load_file_name = "jdh_ohtm_pipeline_final_version"
ohtm_file = load_json_function(load_file_name, output_folder)
from ohtm_pipeline.ohtm_pipeline.topic_evaluation.bar_graph import bar_graph_corpus
bar_graph_corpus(ohtm_file)
```

<!-- #region editable=true slideshow={"slide_type": ""} tags=["hermeneutics"] -->
The bar chart is calculated on the basis of the topic-document distribution of the individual chunks. To do this, the entries in "weight" are iterated, and an entry containing the topic values for each interview is created for each archive. For each interview, the values for each topic per chunk are aggregated and divided by the total number of chunks in the interview. The calculation of the mean value is a method of preventing an overrepresentation of long interviews. The total values of the interviews are then added together and assigned to the individual archives. In this way, not only the overall distribution of the topics across the corpus can be visualized, but also the individual archives thanks to the hierarchy of archive and interview created in the OHTM file. This is possible using the built-in function of the Plotly Express library. A nested dictionary is created for this purpose, with the respective archive as a key and the number of the respective topic as a further key with the weighting as an entry. The dictionary is then converted into a Pandas DataFrame, the indexes are swapped and transferred to Plotly_Express. The bars are displayed as the sum of the individual archives using different colours. In addition, individual archives can be hidden or shown via the legend.

<!-- #endregion -->

```python editable=true slideshow={"slide_type": ""}
import pandas as pd
import plotly_express as px
from ohtm_pipeline.ohtm_pipeline.basic_functions.convert_ohtm_file import convert_ohtm_file


def bar_graph_corpus(ohtm_file, show_fig: bool = True, return_fig: bool = False):
    ohtm_file = convert_ohtm_file(ohtm_file)
    if ohtm_file["settings"]["topic_modeling"]["trained"] == "True":
        interview_dic = {}
        for archive in ohtm_file["weight"]:
            if archive not in interview_dic:
                interview_dic[archive] = {}
            for interview in ohtm_file["weight"][archive]:
                interview_dic[archive][interview] = {}
                count = 0
                for chunk in ohtm_file["weight"][archive][interview]:
                    count += 1
                    for t in ohtm_file["weight"][archive][interview][chunk]:
                        if t not in interview_dic[archive][interview]:
                            interview_dic[archive][interview].update({t: ohtm_file["weight"][archive][interview][chunk][t]})
                        else:
                            interview_dic[archive][interview].update(
                                {t: interview_dic[archive][interview][t] + ohtm_file["weight"][archive][interview][chunk][t]})
                for entry in interview_dic[archive][interview]:
                     interview_dic[archive][interview].update({entry:interview_dic[archive][interview][entry] / count})

        bar_dic = {}
        for archive in interview_dic:
            bar_dic[archive] = {}
            count = 0
            for interview in interview_dic[archive]:
                count += 1
                for t in interview_dic[archive][interview]:
                    if t not in bar_dic[archive]:
                        bar_dic[archive].update({t: interview_dic[archive][interview][t]})
                    else:
                        bar_dic[archive].update({t: bar_dic[archive][t] + interview_dic[archive][interview][t]})
            for entry in bar_dic[archive]:
                bar_dic[archive].update({entry: bar_dic[archive][entry]})

        df = pd.DataFrame.from_dict(bar_dic)
        df.index = pd.to_numeric(df.index)
        fig = px.bar(df, color_discrete_sequence=px.colors.qualitative.G10)
        fig.update_layout(margin=dict(l=20, r=20, t=20, b=20))
        if show_fig:
            fig.show()
        if return_fig:
            return fig
    else:
        print("No Topic Model trained")
```

<!-- #region editable=true slideshow={"slide_type": ""} -->
### Visualising the interview’s topics

The corpus heatmap provides an overview of the distribution of the individual topics across all interviews in the corpus. However, it should be noted that this representation is not congruent with the topic-document distribution of the corpus; rather, it corresponds to the average topic-document distribution per interview. The user can select individual areas or enlarge them using the mouse. The notable clusters are indicative of interviews that constitute a collective sample. The interviews have been assigned consecutive numbers and are therefore arranged in a consecutive order along the Y-axis. It is interesting to see that the thematic similarities between interviews conducted within the same research project are reflected in the assignment of the same topics. It is evident that topics 4 and 44 dominate in interviews derived from a single research project.

<!-- #endregion -->

```python editable=true slideshow={"slide_type": ""} tags=["figure-heatmap-corpus-ohtm-*"]
archive = "all" #you can filter the heatmap to show single archives just replace "all" with the archive abbreviation "zwa", "adg" etc. 
z_score = True

output_folder: str = (r"./media")
load_file_name = "jdh_ohtm_pipeline_final_version"
ohtm_file = load_json_function(load_file_name, output_folder)
from ohtm_pipeline.ohtm_pipeline.topic_evaluation.heatmaps import heatmap_corpus
heatmap_corpus(ohtm_file, option_selected = archive, z_score = z_score)
```

<!-- #region editable=true slideshow={"slide_type": ""} tags=["hermeneutics"] -->
The average values of the heat map are calculated according to the same principle as the bar chart. The chunks of an interview are then added together with their values and divided by the number of chunks in order to avoid an overrepresentation of longer interviews. The values of all interviews are then added to a nested dictionary. In this dictionary, each interview is a key, and the individual topics are also keys, with the corresponding weights as entries. The dictionary is converted into a Pandas DataFrame and then passed to Plotly_Express. The Plotly-Express library used allows the user to zoom in and select individual areas. This is a significant advantage, because the heatmap rapidly becomes more convoluted as the corpus expands. It is therefore possible to filter the heatmap according to the individual archives.
The colour intensity of the individual cells is contingent on their respective values; the darker the colour, the greater the weight of the topics. The ratio of the colour values to each other is based on the largest and smallest values. Large values have a significant impact on the heatmap, causing the other values to appear paler. This results in a more indistinct display of the distribution of individual topics. The data set was homogenized by calculating a z-score, the standard deviation of the individual values with `z = (x - mean) / std`, to obtain a better overview. The objective of this procedure is not to achieve statistical comparability, but rather to enhance the clarity of the graphical representation. Through z-score normalization, the ratios between the individual values remain preserved. This adjustment serves to minimize the influence of extreme values, thereby ensuring the reliability and validity of the data. However, in order to maintain transparency, the respective calculation can be displayed by setting the variable z-score to "True" or "False".

<!-- #endregion -->

<!-- #region editable=true slideshow={"slide_type": ""} -->
### Arrival in the new “Beheimatung” – First Results

These initial evaluations demonstrate that topics 4, 85 and especially 44 are semantically related to the themes of “Heimat” and “Beheimatung”, with traces in all areas of the corpus. However, the heat map's capacity to reveal the average distribution of topics within interviews is limited, resulting in the invisibility of interviews containing solely the searched topics across a limited number of chunks. In the next step, it is therefore advisable to select a finer level of analysis and to examine the corpus on the basis of the individual chunks. As Topic 44 in particular has proven to be highly relevant, the following steps will be based on this topic.
<!-- #endregion -->

<!-- #region editable=true slideshow={"slide_type": ""} -->
### Finding “Beheimatung” inside the chunks

We use the topic-document distribution to trace Topic 44 back to the individual chunks in order to gain initial insights and information about the actual content of the text passages. This is an important part of the analysis, as it is here that we combine the quantitative and qualitative evaluation. To begin with, we take a close look at the chunks in which Topic 44 has been assigned the greatest weighting. To do this, the setting for the function search_for_topics_in_chunks must be set to “True” in main.py and the variable topic_search must be entered with the number of the topic being searched for, in this case 44. The variable chunk_weight specifies the threshold above which the topic weight of the chunk must lie in order to be displayed. The first five results refer to four different interviews from three different archives: MFL20006, MFL10150, ADG0620, MFL20006, WdE0460. For the following explanations, I will take a closer look at the first, third and fifth results in order to use three different interviews from three different archives. For better readability, the original German chunk texts were translated into English using DeepL, and only the translated texts are provided.

<!-- #endregion -->

```python editable=true slideshow={"slide_type": ""}
output_folder: str = (r"./media")
load_file_name = "jdh_ohtm_pipeline_final_version"
ohtm_file = load_json_function(load_file_name, output_folder)
from ohtm_pipeline.ohtm_pipeline.topic_evaluation.topics_prints import print_chunk_with_weight_search
topic = 44
treshold = 0.5

print_chunk_with_weight_search(ohtm_file=ohtm_file, topic_search = topic, chunk_weight=treshold)
```

```python editable=true slideshow={"slide_type": ""}
# Function to print the chunk 23 of the interview mfl20006
output_folder: str = (r"./media")
load_file_name = "jdh_ohtm_pipeline_final_version"
ohtm_file = load_json_function(load_file_name, output_folder)
from ohtm_pipeline.ohtm_pipeline.topic_evaluation.topics_prints import print_chunk

print_chunk(ohtm_file, interview_id = "mfl20006", chunk_number = 23)
```

<!-- #region citation-manager={"citations": {"lcnng": [{"id": "20217732/3HZ6JKFA", "source": "zotero"}], "p2u7k": [{"id": "20217732/3HZ6JKFA", "source": "zotero"}]}} editable=true slideshow={"slide_type": ""} -->
With a Topic_weight of 0.599, chunk 23 of the interview MFL20006 (<cite id="lcnng"><a href="#zotero%7C20217732%2F3HZ6JKFA">(MFL20006 2021)</a></cite>, p. 39-41) has the highest weighting in the entire corpus for Topic 44. It appears to be a double interview, as we find a total of 3 different speaker abbreviations. In total, three different themes can be identified from this text passage, but they all relate to the subjects of “Heimat” and “Beheimatung”. Firstly, the two talk about their difficulties with the German language and their experiences of rejection or disdain, which they attribute to their language skills and their first impression with it. It is interesting that they are asked directly about their impression of Germany. The interviewee describes that he now feels at home in Germany and that it "[is] the best thing that could happen to us. We are really very, very happy" (<cite id="p2u7k"><a href="#zotero%7C20217732%2F3HZ6JKFA">(MFL20006 2021)</a></cite>, p. 40). However, he uses the word “daheim (home)” once, following a word from the Bavarian dialect “dahoam”. Although this word is not part of the pre-processed corpus (see hermeneutics), it still fits perfectly with our interpretation of the topic.
As topic modeling calculates the composition of words within a given unit, this process can also have an effect on words that are not part of the calculation. If these words are thematically congruent with the topic, it is probable that they will also be used in connection with the calculated words. Consequently, words can constitute a component of the outcome of the close reading, independent of their inclusion as topic words. This finding suggests that topic modeling can also be employed to detect implicit speech. The use of a dialect word already shows a certain form of localization, as the local language usage has been appropriated. However, this self-perception is somewhat put into perspective in the following statements, as they speak of experiences of rejection that have been received from some Germans. Nevertheless, the assumption is not made that these experiences are attributable to nationality per se; rather, they are attributed to the attitudes of individuals.

<!-- #endregion -->

<!-- #region editable=true slideshow={"slide_type": ""} tags=["hermeneutics"] -->
A closer analysis of this process has shown that the word “dahoam” is deleted by the function during lemmatization. As a result, “dahoam” is not part of the corpus used to calculate the topic modeling. However, even without being part of the calculation, the word “dahoam” fits the interpretation of Topic 44, as it is part of “Heimat” (home). As shown, the weighting of the chunk is correct, and the high value results from the fact that both themes contained in Topic 44 language and home, are part of the chunk. Unlike “dahoam,” “daheim” is part of Topic 44, but only at position 621. This shows that the assignment is not wrong because the word “dahoam” is appropriate, as a word related to the subject “Heimat”, it is also used together with the calculated words. However, due to the deletion process, it can only be “found” in close reading. Models with a larger number of topics have split topic 44 into two or three different topics, so that there was a separate topic for “Heimat” and one for language. Even though the weighting of the chunk per topic was lower, the sum was still similar to the values of the model used here. Thus, the finding of “dahoam” is not an error but rather shows the correlation of language that is used with the help of topic modeling.
<!-- #endregion -->

```python
# Function to print the chunk 3 of the interview adg0620
output_folder: str = (r"./media")
load_file_name = "jdh_ohtm_pipeline_final_version"
ohtm_file = load_json_function(load_file_name, output_folder)
from ohtm_pipeline.ohtm_pipeline.topic_evaluation.topics_prints import print_chunk

print_chunk(ohtm_file, interview_id = "adg0620", chunk_number = 3)
```

<!-- #region citation-manager={"citations": {"6s50f": [{"id": "20217732/GEN9HSET", "source": "zotero"}]}} editable=true slideshow={"slide_type": ""} -->
In chunk 3 of the interview ADG0620 (<cite id="6s50f"><a href="#zotero%7C20217732%2FGEN9HSET">(Interview with the A. family, 1981)</a></cite>, p. 3-4), we can find the third largest weight of topic 44. The interviewee reported a lack of acceptance, friendliness and the experience of feeling foreign in Germany. According to the interviewee, she was born in Yugoslavia and is Albanian but describes herself as Mohammedan. She lived in Turkey before arriving in Germany and although she was a foreigner there, she reports greater acceptance, as she found a connection through religion rather than nationality. The passage found here gives a good insight into the perception and feeling of home that seems to be missing because one feels foreign. The interviewees are not perceived “as normal citizens”.
<!-- #endregion -->

```python editable=true slideshow={"slide_type": ""}
# Function to print the chunk 33 of the interview wde0460
output_folder: str = (r"./media")
load_file_name = "jdh_ohtm_pipeline_final_version"
ohtm_file = load_json_function(load_file_name, output_folder)
from ohtm_pipeline.ohtm_pipeline.topic_evaluation.topics_prints import print_chunk

print_chunk(ohtm_file, interview_id = "wde0460", chunk_number = 33)
```

<!-- #region citation-manager={"citations": {"au326": [{"id": "20217732/48CHG28V", "source": "zotero"}], "fzvl3": [{"id": "20217732/48CHG28V", "source": "zotero"}], "n6u13": [{"id": "20217732/48CHG28V", "source": "zotero"}]}} editable=true slideshow={"slide_type": ""} -->
Chunk 33 of interview WDE0460 (<cite id="fzvl3"><a href="#zotero%7C20217732%2F48CHG28V">(Jäschke and Jäschke 1993)</a></cite>, Timecode: Tape 2 - 00:11:09.13 – 00:14:02.01) provides another interesting insight, as the interviewee explains that although she has received a German passport, she still sees herself as Polish and not as German. For her, the passport is something purely formal and practical that allows her to move around Europe. At the beginning, she talks about the problems she had with traveling before the German passport, as she was repeatedly stopped at border controls. She also expresses surprise in her comment on the GDR border guard's question that she had the wrong passport, because Poland is there and yet she is apparently listed as a homeless foreigner. After her statement that she sees herself as Polish, she remarks that “maybe that sounds bad” (<cite id="n6u13"><a href="#zotero%7C20217732%2F48CHG28V">(Jäschke and Jäschke 1993)</a></cite>, Timecode: Tape 2 - 0:13:29) as a defensive statement. She quotes from her daughter, almost as a counterexample to her self-image, that although she speaks Polish, she would not describe herself as Polish: “‘No, I'm not Polish, but I speak Polish’”. (<cite id="au326"><a href="#zotero%7C20217732%2F48CHG28V">(Jäschke and Jäschke 1993)</a></cite>, Timecode: Tape 2 – 0:13:51) She then adds that, according to the teachers, her children also speak perfectly German.
We can also recognize the different topics of this chunk in the topic distribution of the other topics. These are the first four most important topics of the chunk:
<!-- #endregion -->

<!-- #region jdh={"module": "object", "object": {"source": ["First 25 words of the top four topics of chunk 33 interview WDE0460 "]}} tags=["table-4"] -->
| Topic | Weight | First 20 -25 Words | 
|:----------|----------|----------:|
| 44   | 0.5292381995922083   | deutsch (German), polen (Poland), deutschland (Germany), polnisch (Polish), sprache (language), russisch (Russian), pole (Pole [Polish person]), <br> lernen (to learn), land (country), deutsche (German [person]), familie (family), russland (Russia), friedland (Friedland), türkei (Turkey), <br> stadt (city), russe (Russian [person]), heimat (homeland), ausländer (foreigner), türkisch (Turkish), grenze (border)<br>|
| 50   | 0.10913928622513634   | zeit (time), arbeit (work), gerne (gladly / with pleasure), richtig (correct / right), schön (nice / beautiful), beruf (profession / occupation), <br> problem (problem), schwer (difficult / hard), versuchen (to try), schaffen (to manage / to accomplish), schlecht (bad), geld (money), anfang (beginning / start), <br> tag (day), stelle (position / job), möglichkeit (possibility / opportunity), merken (to notice / to remember), helfen (to help), letzter (last), übernehmen (to take over / to assume)<br>| 
| 63   | 0.09044079354817278   |kind (child), tochter (daughter), heiraten (to marry), sohn (son), gebären (to give birth), verheiraten (to marry off), familie (family), mädchen (girl),  <br>zweiter (second), wohnen (to live), schön (beautiful / nice), mutter (mother), wohnung (apartment), haus (house), enkel (grandchild / grandson), <br> kennen (to know [someone]), sterben (to die), eltern (parents), spät (late), lernen (to learn)<br>|
| 89   | 0.09029367764025828   | papier (paper), schicken (to send), tag (day), unterschreiben (to sign), melden (to report / to register), post (mail / post),  <br> wussen (to know – likely meant wissen), telefon (telephone), adresse (address), spät (late), antrag (application / request), anrufen (to call), ausweis (ID card), <br> unterlage (document / record), polizei (police), dokument (document), rot (red), liste (list), zeigen (to show), entlassen (to release / to dismiss), rufen (to call / to shout),<br> pass (passport), warten (to wait), nummer (number), büro (office)|

<!-- #endregion -->

<!-- #region editable=true slideshow={"slide_type": ""} -->
In addition to Topic 44, which led us to this chunk, Topic 50 describes the topic of work and challenges, with the words “problem (problem)”, “schwer (difficult)”, “versuchen (to try)”, “schaffen (to manage)” and “schlecht (bad)”. Topic 63 is about family and Topic 89 describes various forms of bureaucracy. All of these topics can be found in the text of the chunk. What is interesting is that we have the greatest weighting with topic 44 and the other three topics are more or less equally distributed. 
<!-- #endregion -->

<!-- #region editable=true slideshow={"slide_type": ""} tags=["hermeneutics"] -->
The advantage of the OHTM file structure is that we can use identical interview keys to call up related results at several levels. To find the chunks whose topic_weight is above the desired threshold, we first iterate over the different levels archive, interview and chunks of “weight”. If the value is above the threshold, we can insert the set variables directly to call up the entries in “corpus”. There we iterate over the individual sentences of the interview and copy the “raw” entries of the sentences where the chunk number matches the variable chunks, and add them together in chronological order. At the same time, the corresponding speaker abbreviation is added to the “raw” entry once and only changed for the “raw” sentences that also have a different speaker. This combined text is then output in the console. The time code of the first sentence of the chunk and the time code of the last sentence of the chunk are stored in a further variable in order to be able to specify the exact time of the chunk. Some topic weights are so small that they can be compared with an Euler number, for example 3.26924e-4, and would therefore be evaluated as a large weight in the function. For this reason, the numbers containing an e are skipped.
<!-- #endregion -->

```python editable=true slideshow={"slide_type": ""} tags=["hermeneutics"]
def print_chunk_with_weight_search(ohtm_file, topic_search: int = 0, chunk_weight: float = 0.3, show_links: bool = False):
    ohtm_file = convert_ohtm_file(ohtm_file)
    anonymized_status = False
    if ohtm_file["settings"]["topic_modeling"]["trained"] == "True":
        sent_final = []
        link_tape = "1"
        for archive in ohtm_file["weight"]:
            for interview in ohtm_file["weight"][archive]:
                try:
                    if ohtm_file["corpus"][archive][interview]["anonymized"] == "True":
                        anonymized_status = True
                except KeyError:
                    anonymized_status = False
                for chunks in ohtm_file["weight"][archive][interview]:
                    chunk_start_marker = 0
                    speaker = "None"
                    if str(ohtm_file["weight"][archive][interview][chunks][str(topic_search)]) >= str(chunk_weight):
                        if "e" in str(ohtm_file["weight"][archive][interview][chunks][str(topic_search)]):
                            next
                        else:
                            sent_current = []
                            for number in ohtm_file["corpus"][archive][interview]["sent"]:
                                int_sent = copy.deepcopy(ohtm_file["corpus"][archive][interview]["sent"][number]["chunk"])
                                if int(int_sent) == int(chunks):
                                    chunk_start_marker += 1
                                    if chunk_start_marker == 1:  # to mark the beginning of the chunk for the first timecode
                                        if ohtm_file["corpus"][archive][interview]["sent"][number]["time"] != {}:
                                            timcodes_available = True
                                            chunk_start_time = \
                                            ohtm_file["corpus"][archive][interview]["sent"][number]["time"]
                                            link_tape = \
                                            ohtm_file["corpus"][archive][interview]["sent"][number]["tape"]
                                        else:
                                            timcodes_available = False
                                            link_tape = "1"
                                            chunk_start_time = "False"
                                    if ohtm_file["corpus"][archive][interview]["sent"][number]["speaker"] == {}:
                                        sent_current.append(str(ohtm_file["corpus"][archive][interview]["sent"][number]["raw"]) + " ")
                                        chunk_end_time = \
                                        ohtm_file["corpus"][archive][interview]["sent"][number]["time"]
                                    else:
                                        if speaker == ohtm_file["corpus"][archive][interview]["sent"][number]["speaker"]:
                                            sent_current.append(str(
                                                ohtm_file["corpus"][archive][interview]["sent"][number]["raw"]) + " ")
                                            chunk_end_time = \
                                                ohtm_file["corpus"][archive][interview]["sent"][number]["time"]
                                        else:
                                            sent_current.append(str("*" +
                                                ohtm_file["corpus"][archive][interview]["sent"][number]["speaker"]) + ":* ")
                                            sent_current.append(str(
                                                ohtm_file["corpus"][archive][interview]["sent"][number]["raw"]) + " ")
                                            speaker = ohtm_file["corpus"][archive][interview]["sent"][number]["speaker"]
                                            chunk_end_time = \
                                                ohtm_file["corpus"][archive][interview]["sent"][number]["time"]
                            sent_current = " ".join(sent_current)
                            sent_current_2 = (str(ohtm_file["weight"][archive][interview][chunks][str(topic_search)]),
                                              interview, chunks, sent_current, chunk_start_time, chunk_end_time,
                                              timcodes_available, link_tape, archive, anonymized_status
                                              )
                            sent_final.append(sent_current_2)
        print("\n" + "The Topic Nr. " + str(topic_search) + " above " + str(chunk_weight)
              + " was found in this chunks:")
        print("weight | interview-id | chunk | raw-text")
        sent_final.sort(reverse = True)
        for interview in sent_final:
            if interview[-1]:
                if interview[-4]:
                    link = create_link(interview[-2].lower(), interview[1].lower(), interview[4], interview[7])
                    print(interview[0] + " | " + interview[1] + " | " + interview[2] + " | " + interview[4] + "–"
                          + str(interview[5]) + " | " + "This interview is anonymized and can be found: " + link)
                else:
                    link = create_link(interview[-2].lower(), interview[1].lower(), interview[4], interview[7])
                    print(interview[0] + " | " + interview[1] + " | " + interview[2] + " | " + "no timecodes" + " | "
                          + "This interview is anonymized and can be found: " + link)
            else:
                if interview[-4]:
                    print(interview[0] + " | " + interview[1] + " | " + interview[2] + " | " + interview[4] + "–"
                          + str(interview[5]) + " | " + interview[3])
                else:
                    print(interview[0] + " | " + interview[1] + " | " + interview[2] + " | " + "no timecodes" + " | "
                          + interview[3])
                if show_links:
                    link = create_link(interview[-2].lower(), interview[1].lower(), interview[4], interview[7])
                    print(link)
        print("\n")
        print("To view one chunk in a better presentation,"
              " print the chunk you want directly with 'print_interview_chunk'.")
    else:
        print("No Topic Model trained")
```

<!-- #region editable=true slideshow={"slide_type": ""} -->
### Diving Deeper – further insights into the results

In addition to the functions used and presented here, the pipeline offers further options for analysing the results. If the variable search_for_topics_in_interview is set to “True”, the chunk search does not take place within the entire corpus but only within a single interview, which is specified via interview_id. The print_interview_chunk function can be used to access and output specific chunks from interviews. In addition to the other search options for the chunks, the interview chronology heatmap provides a visual representation of the distribution of topics and documents in an individual interview. Developed by Dennis Möbus (Möbus [2025]: https://github.com/moebusd/interview_chronology_analysis), it transfers the corpus heatmap to the level of the individual interview, but with one significant change. Swapping the X and Y axes allows the chronological sequence of the interviews to be transferred to the graph. The X-axis shows the individual chunks in chronological order, while the Y-axis shows the topics. This contextualises the temporal level of an interview in relation to the topics and their weighting. This makes it possible to relate the individual chunks to each other in sequence. For example, are there longer passages (i.e. several chunks occurring one after the other) that have the same topic distribution, indicating a longer passage in terms of content? Or are there interesting changes in topic that become visible through the sequence of two chunks and their corresponding topic weightings? The interview chronology heatmap can be displayed by specifying the desired interview via the interview_id variable and setting the show_heatmap_interview function to “True”.

Here we see the chronological heatmap of interview MFL20006. At first glance, it is clear that Topic 44 runs throughout the interview and plays a significant part in the narrative. Between chunks 14 and 20, however, its role is probably less significant. When Topic 44 appears in the MFL interviews, the topic word list must be taken into account, as Topic 44 does not only refer to migration and homeland, but also to Friedland in particular. 

<!-- #endregion -->

```python editable=true slideshow={"slide_type": ""} tags=["figure-interview-heatmap-*"]
output_folder: str = (r"./media")
load_file_name = "jdh_ohtm_pipeline_final_version"
ohtm_file = load_json_function(load_file_name, output_folder)
from ohtm_pipeline.ohtm_pipeline.topic_evaluation.heatmaps import heatmap_interview
heatmap_interview(ohtm_file, interview_id="mfl20006")
```

<!-- #region editable=true slideshow={"slide_type": ""} -->
Interestingly, in the middle section of the interview, three related segments are repeatedly identified that appear to form a thematic unit. Chunks 14, 15 and 16 show spikes in Topics 15 and 86, in addition to Topic 44. Topic 15 can be summarised as relating to travel and holidays, while Topic 86 describes daily routines. In this section of the interview, the interviewees discuss their arrival in Friedland and how they spent their time there prior to continuing their journey. They discussed the activities they undertook and how they found accommodation. Chunks 17, 18 and 19 have a characteristic of Topic 77 that can be summarised as 'living'. In those three chunks the interviewees discuss their arrival at their next destination after Friedland, how they found an apartment, and their daily lives there. Chunks 19, 20 and 21 have a characteristic in Topic 50 that can be described as 'work' and 'challenges', in which they discuss looking for work and their subsequent employment. Therefore, we can see that the topics can be visualised using this representation and that the sequence of the narratives can also be found. 
<!-- #endregion -->

<!-- #region editable=true slideshow={"slide_type": ""} tags=["hermeneutics"] -->
The Chronology Heatmap function creates a nested dictionary from the individual interview chunks, where the chunks act as the keys for a dictionary in which topics and their corresponding values are assigned to entries. This dictionary is then converted into a Pandas DataFrame and transferred to Plotly_Express. It is also possible to perform a z-score calculation here, but this has a much smaller influence on the display than with the Corpus heatmap. The Plotly Express library used enables you to zoom in and select individual areas
<!-- #endregion -->

```python editable=true slideshow={"slide_type": ""} tags=["hermeneutics"]
from builtins import print
import pandas as pd
import plotly_express as px
from ohtm_pipeline.ohtm_pipeline.basic_functions.convert_ohtm_file import convert_ohtm_file


def heatmap_corpus(ohtm_file, option_selected: str = "all",
                   show_fig: bool = True, return_fig: bool = False, z_score: bool = True):

    ohtm_file = convert_ohtm_file(ohtm_file)

    if ohtm_file["settings"]["topic_modeling"]["trained"] == "True":
        if option_selected == "all":
            heat_dic = {}
            for archive in ohtm_file["weight"]:
                for interview in ohtm_file["weight"][archive]:
                    heat_dic[interview] = {}
                    count = 0
                    for c in ohtm_file["weight"][archive][interview]:
                        count += 1
                        for t in ohtm_file["weight"][archive][interview][c]:
                            if t not in heat_dic[interview]:
                                heat_dic[interview].update({t: ohtm_file["weight"][archive][interview][c][t]})
                            else:
                                heat_dic[interview].update(
                                    {t: heat_dic[interview][t] + ohtm_file["weight"][archive][interview][c][t]})
                    for entry in heat_dic[interview]:
                        heat_dic[interview].update({entry: heat_dic[interview][entry] / count})
            df = pd.DataFrame.from_dict(heat_dic)
        else:
            archive = option_selected
            heat_dic = {}
            for interview in ohtm_file["weight"][archive]:
                heat_dic[interview] = {}
                count = 0
                for c in ohtm_file["weight"][archive][interview]:
                    count += 1
                    for t in ohtm_file["weight"][archive][interview][c]:
                        if t not in heat_dic[interview]:
                            heat_dic[interview].update({t: ohtm_file["weight"][archive][interview][c][t]})
                        else:
                            heat_dic[interview].update(
                                {t: heat_dic[interview][t] + ohtm_file["weight"][archive][interview][c][t]})
                for entry in heat_dic[interview]:
                    heat_dic[interview].update({entry: heat_dic[interview][entry] / count})

            df = pd.DataFrame.from_dict(heat_dic)
        if z_score:
            mean = df.mean()
            std_dev = df.std()
            z_scores = ((df - mean) / std_dev)
            df = z_scores
        df = df.transpose()
        fig = px.imshow(df, color_continuous_scale='dense', aspect='auto')
        fig.update_traces(hovertemplate="Interview: %{y}" "<br>Topic: %{x}" "<br>Weight: %{z}<extra></extra>")
        fig.update_layout(clickmode='event+select')
        fig.update_layout(clickmode='event+select')
        fig.update(layout_coloraxis_showscale=False)
        fig.update_layout(margin=dict(l=20, r=20, t=20, b=20))
        if show_fig:
            fig.show()
        if return_fig:
            return fig
    else:
        print("No Topic Model trained")

```

<!-- #region citation-manager={"citations": {"idhk5": [{"id": "20217732/74QRKYPZ", "source": "zotero"}]}} editable=true slideshow={"slide_type": ""} -->
## First Steps of “Beheimatung” – A successful pipeline  

The OHTM pipeline presented here provides an ideal environment for analysing life history interviews with regard to research on “Heimat” and “Beheimatung” narratives. The application facilitates the processing of interview transcripts and the calculation of topic models, including the configuration of all requisite parameters. Notwithstanding the fact that the pipeline has been designed for use with OHD's CSV/ODT formats, it is nevertheless possible for researchers to utilize the pipeline with simple TXT files. The utilization of the pipeline, characterized by its low-threshold application and open access, thus facilitates the application of topic modeling for the purpose of further research.
The employment of topic modeling allowed for the identification of passages within an almost unknown research corpus on topic-document distribution that addressed the subjects of home and belonging. With the question in mind, what helps or restrains the process of “home-making” we found passages that gave a hint of circumstances that hinder this process. In MFL20006 we found a clear statement of a successful “beheimatung”, that happened although they experienced rejection and the feeling of unwanted. This feeling of not feeling welcomed was also found in ADG0620. Mitzscherlich stated that a positive feeling and social connections are important components. (<cite id="idhk5"><a href="#zotero%7C20217732%2F74QRKYPZ">(Mitzscherlich 2019)</a></cite>, p. 185) Using the insights gained in the creation and first analysation of the final model further evaluations will be made. These will include an examination of the combination of different topics with the topics of “Heimat” and “Beheimatung” and then verifying the findings in a close reading. The analysis of chunk 33 of interview WDE0460 revealed an intersection between topics 44 “Beheimatung” and 89 bureaucracies, which correspond to the concepts of bureaucracy. This finding can now be further investigated by searching for correlations between these two topics and searching for combinations of other topics in the respective chunks in order to learn more about the connections between home and bureaucracy. It is imperative to observe the extent to which the connections manifest in relation to the individual archives and the various forms of migration, mobility, and arrival, and whether similarities or differences emerge. An explanation of these correlations can then be attempted by using the historical context.
However, the approach has shown that the actual dynamic analysis process (the mutual combination of the various result levels), loses its dynamic attribute and becomes static by entering the variables manually in the console. For this reason, an interactive dashboard is being developed based on the functions of the OHTM pipeline, which iteratively links the various levels and thus solves the static problem. The OHTM file is to serve as input. Depending on the sensitivity of the research data, the OHTM file is an ideal way to publish the results in a transparent, traceable, and reproducible manner.


<!-- #endregion -->
