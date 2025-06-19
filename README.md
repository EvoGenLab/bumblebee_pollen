# bumblebee_pollen
Data and R codes for analyzing pollen load composition of bumble bee (Apidae: Bombus) queens in Virginia. Contributed by Kelsey Schoenemann.

## Abstract:
The nest-founding stage represents an especially vulnerable period of the bumble bee (Bombus) life cycle, requiring solitary queens locate and acquire sufficient floral pollen to feed herself and her brood. Yet, we lack contemporary information about foraging resources used by queens in early spring. Here, we use next generation sequencing to characterize the floral species used by queens for pollen for provisioning during early nest establishment. The following data and analyses describe patterns of pollen collection from over 100 wild bumble bee queens at 26 working farms, rural and city parks, and nature preserves captured between 21 March to 25 May, 2022 in northern and central Virginia, USA.

## Contents:
### [`scripts/`](scripts/)
The [`scripts/analysis`](scripts/analysis) directory contains the code for combining, analyzing, and plotting the data from the datasets directory, and the [`scripts/preprocessing`](scripts/preprocessing/) directory contains the code and HTML output for the bioinformatics pipelines used to generate amplicon sequence variant tables for rbcL and ITS2 barcode sequence reads
### [`datasets/`](datasets/)
This directory contains the original data from field surveys and the amplicon sequence variant tables generated from the ITS2 and rbcL bioinformatics pipelines.
The seven (7) datasets comprise: i) records from surveys of wild bumble bee (Apidae: Bombus) queens across 26 sites; ii) floral species presence incidentally recorded during a portion of those surveys; iii) amplicon sequence variants assigned to plant taxonomy resulting from metabarcoding of pollen samples collected from Bombus queens; and iv) extracted land cover composition within 1km of all survey sites

### Dataset Descriptions:

i) Teams of 1-4 searched for queens at 15 public parks and 10 private properties, visited twice about 22 days apart, while  a single surveyor (DEC) searched for pollen-bearing queens at Blandy Experimental Farm in Boyce, VA, 26 times about 2 days apart. Surveyors attempted to capture every queen encountered. From this, three datasets were generated:

#### CaptureLog.csv
records of individual Bombus queens captured during timed surveys in 2022
| Column Name |Data Type|Description|
|:-------|:-------|:-------|
| `Date` |Date|Date when Bombus queens were captured, mm/dd/yy|
| `SiteID` |Text|Unique identifier for survey site visits (abbreviated site name and visit number) during which Bombus queens were captured|
| `BeeID` |Text|Unique identifier for Bombus queens captured as part of the study|
| `Bombus_spp` |Text|Taxonomic species of Bombus queens captured|
| `CapTimeH` |Numeric|Time of day when queens were captured, 24-hour|
| `CapTimeM` |Numeric|Time of day when queens were captured, minute|
| `CarryPollen` |Binary|Indicates whether or not Bombus queens carried a pollen load at time of capture (1 = yes, 0 = no)|
| `SampleID` |Text|Name of pollen sample (i.e., as BeeID) used for metabarcoding, or "0" if no sample exists|
| `HostCommon` |Text|As applicable (for queens caught while foraging), lists the common name of the floral host on which the queens were foraging at time of capture|
| `HostFamily` |Text|As applicable (for queens caught while foraging), lists the taxonomic family of the floral host on which the queens were foraging at time of capture|
| `HostGenus` |Text|As applicable (for queens caught while foraging), lists the taxonomic genus of the floral host on which the queens were foraging at time of capture|
| `HostSpecies` |Text|As applicable (for queens caught while foraging), lists the taxonomic species of the floral host on which the queens were foraging at time of capture|
| `Flying` |Binary|Indicates whether or not Bombus queens were captured while flying (1 = yes, 0 = no)|
| `Forage` |Binary|Indicates whether or not Bombus queens were captured while foraging (1 = yes, 0 = no)|
| `NestSeek` |Binary|Indicates whether or not Bombus queens were captured while nest-seeking (1 = yes, 0 = no)|
| `ReleaseTimeH` |Numeric|Time of day when queens were released, 24-hour|
| `ReleaseTimeM` |Numeric|Time of day when queens were released, minute|
| `InHandM` |Numeric|Total duration that queens were restrained, minutes|
| `BeeNotes` |Text|Additional commentary about the captured queens|

#### SiteData.csv
records of site conditions during site visits
| Column Name |Data Type|Description|
|:-------|:-------|:-------|
| `SiteID` |Text|Unique identifier for survey sites (abbreviated site name) at which Bombus queen surveys were performed|
| `Name` |Text|Full name of survey sites at which Bombus queen surveys were performed|
| `Date` |Date|Date of Bombus queens survey|
| `StartTimeH` |Numeric|Time of day when survey started, 24-hour|
| `StartTimeM` |Numeric|Time of day when survey started, minute|
| `EndTimeH` |Numeric|Time of day when survey ended, 24-hour|
| `EndTimeM` |Numeric|Time of day when survey ended, minute|
| `EndTempC` |Numeric|Air temperature at the end of the survey, degrees celsius|
| `DurationM` |Numeric|Total duration of Bombus queen surveys, minutes|
| `CountFlying` |Numeric|Count of Bombus queens observed flying (but not captured) at sites during surveys|
| `CountForaging` |Numeric|Count of Bombus queens observed foraging (but not captured) at sites during surveys|
| `CountNestSeeking` |Numeric|Count of Bombus queens observed nest-seeking (but not captured) at sites during surveys|
| `TotalObserved` |Numeric|Sum of Bombus queens observed (but not captured) at sites during surveys|

#### SurveyEffort.csv
records of surveyor search times during surveys
| Column Name |Data Type|Description|
|:-------|:-------|:-------|
| `SiteID` |Text|Unique identifier for survey site visits (abbreviated site name and visit number) for Bombus queen surveys|
| `Observer` |Text|Identity of surveyor: volunteer or principal investigator (KLS / DEC)|
| `SearchTime` |Numeric|Total duration of surveyor search time, minutes|


ii) To describe the suite of blooming plants available to foraging queens, we performed informal surveys of flowering species across the landscape sites. We did not record blooming plants at Blandy due to logistic constraints. At all other sites, we recorded all animal-pollinated blooming plant species with more than two individual plants in bloom that we encountered during the survey. From this, one dataset was generated:

#### FloweringSpp.csv
records of flowering plant species incidentally observed during Bombus queen survey visits
| Column Name |Data Type|Description|
|:-------|:-------|:-------|
| `SiteID` |Text|Unique identifier for survey site visits (abbreviated site name and visit number)|
| `Family` |Text|Taxonomic family of blooming plants observed during Bombus queen surveys|
| `Genus` |Text|Taxonomic genus of blooming plants observed during Bombus queen surveys|
| `Species` |Text|Taxonomic species of blooming plants observed during Bombus queen surveys|
| `Common` |Text|Common name of blooming plants observed during Bombus queen surveys|


iii) To identify floral pollens present in pollen samples, we used metabarcoding. In brief, we prepared indexed Illumina MiSeq libraries targeting two DNA barcodes, the internal transcribed spacer (ITS2) and the ribulose-1,5-biphosphate carboxylase/oxygenase large subunit (rbcL), using iTru ‘fusion’ primers via a two-step PCR (Glenn et al. 2019). These primers are universal plant barcode primers, ITS2 S2F and ITS2 4R from (Lee et al. 1990, Chen et al. 2010), rbcL 2F and rbcLa R from (Kress and Erickson 2007, Palmieri et al. 2009), with Illumina overhang adapter sequences appended (as in Glenn et al. 2019). After the remainder of library preparation and sequencing (see methods), we used dada2’s denoising algorithm to infer amplicon sequence variants (ASVs) and generate a table of read numbers for each ASV. After quality control (see methods), We used dada2's 'assignTaxonomy' function to implement a naïve Bayesian classifier to classify ASVs, with more than 100 reads, using publicly-available reference databases: ‘PLANiTS’ database for ITS2 sequences (Banchi et al. 2020; last updated 2020), and the ‘rbcL’ database for rbcL sequences (Bell et al. 2017; last updated 2021). From this, two datasets were generated with identical column types:

#### its2.IDs.long.csv and rbcL.IDs.long.csv
records of Amplicon Sequence Variants (ASVs) detected with ITS2 or rbcL metabarcoding and assigned to plant taxonomy; output from bioinformatics processing pipeline 
| Column Name |Data Type|Description|
|:-------|:-------|:-------|
| `Index` |Numeric|Unique identifier for assigned ASV records summarized from MiSeq v3 sequencing run; records pertaining to studies not reported here have been omitted|
| `Kingdom` |Text|Taxonomic kingdom assigned to ASVs detected in Bombus queen pollen samples|
| `Phylum` |Text|Taxonomic phylum assigned to ASVs detected in Bombus queen pollen samples|
| `Class` |Text|Taxonomic class assigned to ASVs detected in Bombus queen pollen samples|
| `Order` |Text|Taxonomic order assigned to ASVs detected in Bombus queen pollen samples|
| `Family` |Text|Taxonomic family assigned to ASVs detected in Bombus queen pollen samples|
| `Genus` |Text|Taxonomic genus assigned to ASVs detected in Bombus queen pollen samples|
| `Species` |Text|Taxonomic species assigned to ASVs detected in Bombus queen pollen samples|
| `ASVTotalReads` |Numeric|Total reads belonging to ASVs appearing in many samples|
| `Sample` |Text|Unique identifier for Bombus queens captured as part of the study|
| `Reads` |Numeric|Number of reads belonging to ASVs in Bombus queen pollen samples|
| `SampleTotalReads` |Numeric|Total reads belonging to Bombus queen pollen samples comprised of many ASVs|


iv) To describe the land cover composition surrounding survey sites and queen locations, we accessed the 2019 National Land Cover Dataset (NLCD), which provides a nationwide 30m resolution land cover data (Homer et al. 2020). Using QGIS version 3.34.11 (QGIS 2021), we extracted land cover within 1km of survey site center points. In our study region, there were 15 land cover categories represented. After data extraction, we reclassified these 15 categories into: water, developed, forest, herbaceous, and crop; based on their relative value for nesting and foraging opportunities for bees (Lanterman et al. 2019). From this, one dataset was generated:

#### export-Sites.csv
exported land cover data from the 2019 National Land Cover Dataset within 1 km of Bombus queen survey sites
| Column Name |Data Type|Description|
|:-------|:-------|:-------|
| `Num` |Numeric|Index|
| `Name` |Text|Full name of survey sites at which Bombus queen surveys were performed|
| `SiteID` |Text|Unique identifier for survey sites (abbreviated site name) at which Bombus queen surveys were performed|
| `Type` |Text|Land ownership category|
| `Acres` |Numeric|Approximate total area of survey site|
| `County` |Text|Virginia county where site was located|
| `Updated_x` |Numeric|Longitude (World Geodetic System 84 datum)|
| `Updated_y` |Numeric|Latitude (World Geodetic System 84 datum)|
| `NLCD_Sites_1000m_11` |Numeric|Count of 30x30m pixels containing Water within 1 km of site center point|
| `NLCD_Sites_1000m_21` |Numeric|Count of 30x30m pixels containing DevelopedOpen within 1 km of site center point|
| `NLCD_Sites_1000m_22` |Numeric|Count of 30x30m pixels containing DevelopedLow within 1 km of site center point|
| `NLCD_Sites_1000m_23` |Numeric|Count of 30x30m pixels containing DevelopedMed within 1 km of site center point|
| `NLCD_Sites_1000m_24` |Numeric|Count of 30x30m pixels containing DevelopedHigh within 1 km of site center point|
| `NLCD_Sites_1000m_31` |Numeric|Count of 30x30m pixels containing Barren within 1 km of site center point|
| `NLCD_Sites_1000m_41` |Numeric|Count of 30x30m pixels containing DeciduousForest within 1 km of site center point|
| `NLCD_Sites_1000m_42` |Numeric|Count of 30x30m pixels containing EvergreenForest within 1 km of site center point|
| `NLCD_Sites_1000m_43` |Numeric|Count of 30x30m pixels containing MixedForest within 1 km of site center point|
| `NLCD_Sites_1000m_52` |Numeric|Count of 30x30m pixels containing ShrubScrub within 1 km of site center point|
| `NLCD_Sites_1000m_71` |Numeric|Count of 30x30m pixels containing Grassland within 1 km of site center point|
| `NLCD_Sites_1000m_81` |Numeric|Count of 30x30m pixels containing PastureHay within 1 km of site center point|
| `NLCD_Sites_1000m_82` |Numeric|Count of 30x30m pixels containing CultivatedCrops within 1 km of site center point|
| `NLCD_Sites_1000m_90` |Numeric|Count of 30x30m pixels containing WoodyWetlands within 1 km of site center point|
| `NLCD_Sites_1000m_95` |Numeric|Count of 30x30m pixels containing HerbaceousWetlands within 1 km of site center point|![image](https://github.com/user-attachments/assets/294d66c7-d298-40b8-a3d4-65fa2fc5bd52)
