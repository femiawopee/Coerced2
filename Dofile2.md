
/////// DATA SET //////////
/// TO BE MERGED //////////
//// COERCED SEX /////////


// Population: Females and ever had sex


// Tony 2019
use Tony2019, clear

tab1 a_age a_age_5year a_study a_sex a_MSTATUS a_Sppoverall a_sppfinance a_sppresource a_livarrnge a_family a_Falive a_Freside a_Malive a_Mreside a_children a_alcohol a_drugs a_cigarette

codebook b_eversex b_sexpartner b_fsexstate b_fsexage b_fsexregret

codebook a_sex b_eversex
*keep if a_sex==2
keep if b_eversex==1
save Tony2019_keep, replace
use Tony2019_keep, clear
tab b_eversex

// recoding
codebook a_age a_Sppoverall a_family a_Falive a_Freside a_Malive a_Mreside  a_alcohol a_drugs a_cigarette b_fsexstate b_fsexage b_fsexregret

recode a_Sppoverall (1=1 "Adequate") (2=2 "Moderate") (3 4=3 "Little/No"), gen(a_Support1)

recode a_family (1=1 "Nuclear") (2=2 "Polygamous") (3=3 "SingleParent")(4=4 "FosterParent"), gen(a_family1)

recode a_Falive (1=1 "Yes") (2=0 "No"), gen(a_Falive1)
recode a_Freside (1=1 "Yes") (2 .=0 "No"), gen(a_Freside1)

recode a_Malive (1=1 "Yes") (2=0 "No"), gen(a_Malive1)
recode a_Mreside (1=1 "Yes") (2 .=0 "No"), gen(a_Mreside1)

recode a_alcohol (1 2=1 "Yes") (3=0 "No"), gen(a_alcohol1)
recode a_drugs (1 2=1 "Yes") (3=0 "No"), gen(a_drugs1)
recode a_cigarette (1 2=1 "Yes") (3=0 "No"), gen(a_cigarette1)

// learn to spot data entry error (via questionnaire)
recode b_fsexstate (1 0=1 "Persuaded") (2 12=2 "Forced") (3=3 "Willing") (.=4 "Missing"), gen(b_fsexstate1)

mean b_fsexage
gen b_fsexage1=b_fsexage
*replace b_fsexage1=18 if b_fsexage==.
// edit by inputing 18 and 19 based on mean decimal results
*edit b_fsexage b_fsexage1
tab1 b_fsexage1 b_fsexage, mis

recode b_fsexregret (1=1 "Yes") (2 3 .=0 "No"), gen(b_fsexregret1)

tab1 a_age a_Support1 a_family1 a_Falive1 a_Freside1 a_Malive1 a_Mreside1 a_alcohol1 a_drugs1 a_cigarette1 b_fsexstate1 b_fsexage1 b_fsexregret1

keep a_age a_Sppoverall a_family a_Falive a_Freside a_Malive a_Mreside  a_alcohol a_drugs a_cigarette b_fsexstate b_fsexage b_fsexregret a_age a_Support1 a_family1 a_Falive1 a_Freside1 a_Malive1 a_Mreside1 a_alcohol1 a_drugs1 a_cigarette1 b_fsexstate1 b_fsexage1 b_fsexregret1

save Tony2019_recode, replace
 
 
 
 
// Dataset\Merged data-16-24 years
use Mergeddata1624yearsunmarriedPEPdatasetsav, clear

tab1 respondent_age respondent_sex nationality marital_status parity respondent_level faculty respondent_residence living_arrange respondent_religion if_not_on_the_list frequency_religion religion_importance rate_religiousity Rate_dad_religiosity rate_mum_religiosity father_alive Live_with_you easy_to_talk discussed_sex how_often mother_alive live_in_same_household talk_with_mother talk_sex frequent_sex_talk father_describe mother_describe living_arrangement_home family_support parent_socialstatus job ever_drank currently_drink drank_lastweek binge_drink drink_frequency ever_smoke currently_smoke number_of_sticks

codebook ever_sex age_sexual_debut describe_relationship partner_decribe_relationship descibe_sex regret_first_sex

codebook respondent_sex ever_sex
keep if respondent_sex==2
keep if ever_sex==1
save Mergeddata1624yearsunmarriedPEPdatasetsav_keep, replace
use Mergeddata1624yearsunmarriedPEPdatasetsav_keep, clear
tab ever_sex

// recoding
codebook respondent_age family_support father_alive Live_with_you mother_alive live_in_same_household living_arrangement_home ever_drank  ever_drug ever_smoke descibe_sex age_sexual_debut regret_first_sex

rename respondent_age a_age 

recode family_support (1=1 "Adequate") (2=2 "Moderate") (3 4=3 "Little/No"), gen(a_Support1)

recode living_arrangement_home (2=1 "Nuclear") (1=3 "SingleParent")(3 4=4 "FosterParent"), gen(a_family1)

recode father_alive (1=1 "Yes") (2/max=0 "No"), gen(a_Falive1)
recode Live_with_you (1=1 "Yes") (2/max .=0 "No"), gen(a_Freside1)

recode mother_alive (1=1 "Yes") (2/max=0 "No"), gen(a_Malive1)
recode live_in_same_household (1=1 "Yes") (2/max .=0 "No"), gen(a_Mreside1)

recode ever_drank (1=1 "Yes") (2/5=0 "No"), gen(a_alcohol1)
recode ever_drug (1=1 "Yes") (2/5=0 "No"), gen(a_drugs1)
recode ever_smoke (1=1 "Yes") (2/5=0 "No"), gen(a_cigarette1)

// learn to spot data entry error (via questionnaire)
recode descibe_sex (2 3=1 "Persuaded") (1 4=2 "Forced") (5 6=3 "Willing")  (.=4 "Missing"), gen(b_fsexstate1)

gen b_fsexage1=age_sexual_debut

recode regret_first_sex (1=1 "Yes") (2/max .=0 "No"), gen(b_fsexregret1)

tab1 a_age a_Support1 a_family1 a_Falive1 a_Freside1 a_Malive1 a_Mreside1  a_alcohol1 a_drugs1 a_cigarette1 b_fsexstate1 b_fsexage1 b_fsexregret1

keep respondent_age family_support father_alive Live_with_you mother_alive live_in_same_household living_arrangement_home ever_drank  ever_drug ever_smoke descibe_sex age_sexual_debut regret_first_sex a_age a_Support1 a_family1 a_Falive1 a_Freside1 a_Malive1 a_Mreside1  a_alcohol1 a_drugs1 a_cigarette1 b_fsexstate1 b_fsexage1 b_fsexregret1


save Mergeddata1624yearsunmarriedPEPdatasetsav_recode, replace





// Sexually active only consistent
use Sexuallyactiveonlyconsistentcondomuse, clear

tab1 UNIVERISTY DOB Age Agecategory Sex levelofstudy campusresidence Livingarrangementoncampus Religiousbackground frequencyofreligiousattendance Importanceofreligioninyourlife rateyourreligiousity dad mum fatheralive livewithyou talkaboutsex easytotalk frequencyofsextalk Motheralive Liveinthesamehousehold easytotalk_A sex_A Describefather describemother Livingarrangement Familysupport Parentssocioeconmicstatus Alcohol Currentlydrink daysinthelastmonth EverSmoke Currentlysmoke Howmanysticks Usedrug Currentlyusedrug Timesinthelastmonth

codebook Haveyoueverengagedinsexualinterc Ageatfirstsex Relationshipwiththeperson howwouldhedescribeyourrelationsh descibethesex Didyouregretit

codebook Sex Haveyoueverengagedinsexualinterc
keep if Sex==2
drop if Age>25
save Sexuallyactiveonlyconsistentcondomuse_keep, replace
use Sexuallyactiveonlyconsistentcondomuse_keep, clear
tab1 Sex Age

// recoding
codebook Age Familysupport fatheralive livewithyou Motheralive Liveinthesamehousehold Livingarrangement Alcohol Usedrug EverSmoke Ageatfirstsex descibethesex Didyouregretit
 
gsort  Agecategory Age DOB
*browse Age Agecategory DOB Age1
codebook Age Agecategory DOB 

gen Age1=Age
replace Age1=20 if Agecategory==3 & Age==.
replace Age1=25 if Agecategory==4 & Age==.
tab Age1

codebook Age1 fatheralive livewithyou Motheralive Liveinthesamehousehold Livingarrangement Familysupport Alcohol Usedrug EverSmoke Ageatfirstsex descibethesex Didyouregretit DidyouregretitVAR00002

rename Age1 a_age 

recode Familysupport (1=1 "Adequate") (2=2 "Moderate") (3 4=3 "Little/No"), gen(a_Support1)

recode Livingarrangement (2=1 "Nuclear") (3=2 "Polygamous") (1=3 "SingleParent")(4=4 "FosterParent"), gen(a_family1)

recode fatheralive (1=1 "Yes") (2=0 "No"), gen(a_Falive1)
recode livewithyou (1=1 "Yes") (2 .=0 "No"), gen(a_Freside1)

recode Motheralive (1=1 "Yes") (2 .=0 "No"), gen(a_Malive1)
recode Liveinthesamehousehold (1=1 "Yes") (2 .=0 "No"), gen(a_Mreside1)

recode Alcohol (1=1 "Yes") (2=0 "No"), gen(a_alcohol1)
recode Usedrug (1=1 "Yes") (2=0 "No"), gen(a_drugs1)
recode EverSmoke (1=1 "Yes") (2=0 "No"), gen(a_cigarette1)

// learn to spot data entry error (via questionnaire)
recode descibethesex (2 3=1 "Persuaded") (1 4=2 "Forced") (5=3 "Willing"), gen(b_fsexstate1)

gen b_fsexage1=Ageatfirstsex

recode DidyouregretitVAR00002 (1=1 "Yes") (2=0 "No"), gen(b_fsexregret1)

tab1 a_age a_Support1 a_family1 a_Falive1 a_Freside1 a_Malive1 a_Mreside1 a_alcohol1 a_drugs1 a_cigarette1 b_fsexstate1 b_fsexage1 b_fsexregret1

keep Age1 fatheralive livewithyou Motheralive Liveinthesamehousehold Livingarrangement Familysupport Alcohol Usedrug EverSmoke Ageatfirstsex descibethesex Didyouregretit DidyouregretitVAR00002
 a_age a_Support1 a_family1 a_Falive1 a_Freside1 a_Malive1 a_Mreside1 a_alcohol1 a_drugs1 a_cigarette1 b_fsexstate1 b_fsexage1 b_fsexregret1

save Sexuallyactiveonlyconsistentcondomuse_recode, replace




// Merging or appending
use Tony2019_recode, clear
append using Mergeddata1624yearsunmarriedPEPdatasetsav_recode Sexuallyactiveonlyconsistentcondomuse_recode

save coerced, replace

tab1 a_age a_Support1 a_family1 a_Falive1 a_Freside1 a_Malive1 a_Mreside1 a_alcohol1 a_drugs1 a_cigarette1 b_fsexstate1 b_fsexage1 b_fsexregret1
v