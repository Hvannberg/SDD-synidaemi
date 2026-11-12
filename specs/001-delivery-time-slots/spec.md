# Feature Specification: Val afhendingartímabils

**Feature Branch**: Engin ný grein stofnuð í þessari keyrslu.

**Created**: 2026-11-12

**Status**: Drög til rýni. Áætlanagerð og kóðagerð bíða rýni notanda.

**Input**: Reglur BR-1/BR-2, kröfur FR-DEL-1/FR-DEL-2 og próflýsingar í fyrirmælum notanda.
Viðfangsefnið er val afhendingartímabils í UC-1 „Order a Meal“. Tæknival er óákveðið.

### Heimildir og staða upplýsinga

| Heimild | Innihald | Staða |
| --- | --- | --- |
| H-1 | BR-1 og BR-2 í innsendri lýsingu | Staðfestur grunnur draga |
| H-2 | FR-DEL-1 og FR-DEL-2 í innsendri lýsingu | Staðfestur grunnur draga |
| H-3 | AT-DEL-1 og AT-DEL-2 í innsendri lýsingu | Próflýsingar lagðar fram af notanda |
| H-4 | Tilvísun í AT-DEL-LEID-1 og AT-DEL-LEID-2 úr efni 8.2 | Efni 8.2 sjálft hefur ekki verið lagt fram eða sannreynt |
| H-5 | [Verkefnisstjórnarskrá v1.0.0](../../.specify/memory/constitution.md) | Gildandi almennar reglur um UX, sannprófun inntaks og endurgjöf |

Auðkenni eru varðveitt óbreytt. Samsvörun AT-DEL-LEID-1 við AT-DEL-1 og
AT-DEL-LEID-2 við AT-DEL-2 er óstaðfest; sjá O-1. Engin viðbót úr efni 8.2 er ályktuð.

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Sjá leyfileg tímabil eftir val dags (Priority: P1)

Sem notandi í UC-1 „Order a Meal“ vil ég velja dag og sjá afhendingartímabil sem
samræmast þjónustutíma svo ég geti valið afhendingartíma innan reglna þjónustunnar.

**Heimild**: UC-1 í fyrirmælum notanda; H-1, H-2 og AT-DEL-1 í H-3.

**Why this priority**: Birting leyfilegra tímabila er meginflæði þessa eiginleika.

**Independent Test**: Velja dag og athuga lengd, upphaf og lok allra birtra tímabila.
Önnur skref máltíðarpöntunar þurfa ekki að vera hluti af athuguninni.

**Acceptance Scenarios**:

1. **AT-DEL-1**: **Given** að notandi sé í tímavali UC-1, **When** hann velur dag,
   **Then** sýnir kerfið aðeins 15 mínútna tímabil innan 10:00–14:00 að staðartíma
   sem hefjast á :00, :15, :30 eða :45 í hverri klukkustund.
   **Heimild**: H-3; sannprófar FR-DEL-1 og birtingarhluta FR-DEL-2 samkvæmt BR-1/BR-2.

**AT-DEL-LEID-1**: Auðkenni tilvísaðs prófs úr H-4 er varðveitt hér. Innihald og
samsvörun við AT-DEL-1 bíða staðfestingar, sjá O-1.

### User Story 2 - Skilja höfnun of seins tímabils (Priority: P1)

Sem notandi vil ég fá skýringu þegar beiðni minni um of seint tímabil er hafnað
svo ég skilji hvaða afhendingarmörk gilda.

**Heimild**: FR-DEL-2 og AT-DEL-2; H-5 um skiljanlega endurgjöf.

**Why this priority**: Lokamörkin þurfa að gilda við móttöku beiðna, auk birtingar valkosta.

**Independent Test**: Leggja fram beiðni um 14:00–14:15 og athuga höfnun og skýringu.

**Acceptance Scenarios**:

1. **AT-DEL-2**: **Given** að beiðni um afhendingartímabil sé lögð fram,
   **When** óskað er eftir 14:00–14:15, **Then** hafnar kerfið beiðninni og útskýrir
   að afhendingum þurfi að vera lokið fyrir eða kl. 14:00 að staðartíma.
   **Heimild**: H-3; sannprófar höfnunar- og skýringarhluta FR-DEL-2, byggðan á BR-2.

**AT-DEL-LEID-2**: Auðkenni tilvísaðs prófs úr H-4 er varðveitt hér. Innihald og
samsvörun við AT-DEL-2 bíða staðfestingar, sjá O-1.

### Edge Cases

Afleidd athugunartilvik til rýni; þau breyta ekki upprunalegu prófaauðkennunum.

| Tilvik | Niðurstaða sem leiðir af staðfestum reglum | Heimild |
| --- | --- | --- |
| 09:45–10:00 | Ekki boðið; upphaf fyrir kl. 10:00. | BR-2, FR-DEL-1 |
| 10:00–10:15 | Uppfyllir tímareglurnar; aðrar framboðsreglur óákveðnar. | BR-1, BR-2 |
| 10:05–10:20 | Ekki boðið; hefst utan stundarfjórðungs. | BR-1, FR-DEL-1 |
| 10:00–10:30 | Ekki boðið; lengd er ekki 15 mínútur. | BR-1, FR-DEL-1 |
| 13:45–14:00 | Uppfyllir tímareglurnar; lok nákvæmlega kl. 14:00 eru leyfileg. | BR-1, BR-2 |
| 14:00–14:15 | Ekki boðið; móttekinni beiðni hafnað með skýringu. | FR-DEL-2, AT-DEL-2 |
| Vantar dag/tíma eða lok eru á undan upphafi | Sannprófun áskilin samkvæmt H-5; sértæk viðbrögð til rýni í T-3/O-3. | H-5 |

## Requirements *(mandatory)*

### Viðskiptareglur

Reglurnar lýsa skorðum á afhendingar, óháð birtingu eða móttöku beiðna í kerfinu.

- **BR-1**: Afhendingartímabil eru 15 mínútur og hefjast á hverjum stundarfjórðungi.
  **Heimild**: H-1.
- **BR-2**: Afhendingar mega hefjast í fyrsta lagi kl. 10:00 og þeim skal lokið
  eigi síðar en kl. 14:00 að staðartíma. **Heimild**: H-1.

**Afleiðing til rýni**: Fyrsta mögulega tímabil er 10:00–10:15 og síðasta mögulega
13:45–14:00. Tímaglugginn rúmar 16 slík tímabil. Þetta leiðir af BR-1/BR-2 og felur
hvorki í sér loforð um framboð allra tímabila né reglu um leyfilega afhendingardaga.

### Functional Requirements

Kröfurnar lýsa hegðun kerfisins og eru varðveittar úr innsendri lýsingu.

- **FR-DEL-1**: Kerfið skal aðeins bjóða 15 mínútna afhendingartímabil innan
  þjónustutíma sem hefjast á :00, :15, :30 eða :45 í hverri klukkustund.
  **Heimild**: H-2; byggist á BR-1 og BR-2; sannprófað með AT-DEL-1.
- **FR-DEL-2**: Kerfið skal aðeins bjóða afhendingartímabil sem lýkur eigi síðar en
  kl. 14:00. Berist beiðni um tímabil sem lýkur síðar skal kerfið hafna henni og
  útskýra að afhendingum þurfi að vera lokið fyrir eða kl. 14:00.
  **Heimild**: H-2; byggist á BR-2; sannprófað með AT-DEL-1 og AT-DEL-2.

H-5 krefst sannprófunar alls inntaks áður en aðgerð er framkvæmd, leiðbeinandi
endurgjafar og varðveislu gildra upplýsinga við leiðréttanlegar villur. Þessar almennu
skyldur gilda áfram. Sértækar viðbætur við hegðun FR-DEL-1/2 eru aðskildar í T-3.

### Key Entities *(include if feature involves data)*

Hugtökin hér lýsa viðfangsefninu; þau ákveða ekki tæknilega gagnaskipan.

- **Afhendingardagur**: Dagur valinn af notanda í UC-1. Heimild: AT-DEL-1.
- **Afhendingartímabil**: Upphaf og lok afhendingar á völdum degi, samkvæmt lengd,
  stundarfjórðungum og tímamörkum BR-1/BR-2. Heimild: H-1 og H-2.
- **Beiðni um tímabil**: Ósk sem kerfið metur, þar á meðal óleyfilegt tímabil sem
  þarf að hafna samkvæmt FR-DEL-2. Heimild: H-2 og AT-DEL-2.

### Umfang og rekjanleiki

Umfangið er tímavalshluti UC-1 og höfnun samkvæmt FR-DEL-2. Máltíðaval, greiðsla og
framkvæmd afhendingar eru ekki skilgreind hér. Heimild: afmörkun viðfangsefnis í
fyrirmælum notanda. Tæknival, áætlanagerð og kóðagerð bíða síðari ákvörðunar.

| Regla | Hegðun kerfis | Prófun í innsendum texta | Tilvísun í efni 8.2 |
| --- | --- | --- | --- |
| BR-1 | FR-DEL-1 | AT-DEL-1 | AT-DEL-LEID-1; samsvörun óstaðfest |
| BR-2 | FR-DEL-1 og FR-DEL-2: birting | AT-DEL-1 | AT-DEL-LEID-1; samsvörun óstaðfest |
| BR-2 | FR-DEL-2: höfnun og skýring | AT-DEL-2 | AT-DEL-LEID-2; samsvörun óstaðfest |

## Success Criteria *(mandatory)*

### Measurable Outcomes

Afleidd mælanleg viðmið til rýni; ekki niðurstöður keyrðra hugbúnaðarprófa.

- **SC-DEL-1**: 100% birtra tímabila eru 15 mínútur, hefjast á stundarfjórðungi,
  hefjast eigi fyrr en kl. 10:00 og enda eigi síðar en kl. 14:00 að staðartíma.
  **Heimild**: BR-1/BR-2, FR-DEL-1/FR-DEL-2 og AT-DEL-1.
- **SC-DEL-2**: Beiðnum sem enda eftir kl. 14:00 er hafnað í öllum athugunum á
  FR-DEL-2, þar á meðal 14:00–14:15, og í öllum tilvikum fylgir skýring um lokamörkin.
  **Heimild**: FR-DEL-2 og AT-DEL-2.
- **SC-DEL-3**: Við yfirferð AT-DEL-2 eru bæði ástæða höfnunar og gild lokamörk
  skiljanleg út frá skilaboðunum einum, án lesturs kóða eða munnlegrar útskýringar.
  Bæði atriði þurfa að standast. **Heimild**: FR-DEL-2 og H-5.

## Assumptions

Engin ný forsenda hér að neðan er sett fram sem staðfest krafa. Innri skref UC-1 og
reglur um afhendingardaga liggja ekki fyrir í innsendum texta. Heimild: H-1–H-3.

### Tillögur að nýjum forsendum — óstaðfestar

- **T-1**: Staðartími miðist við afhendingarstað. **Rök**: BR-2 nefnir staðartíma
  en skilgreinir ekki viðmið hans. Krefst ákvörðunar í O-2.
- **T-2**: Grunnsýnidæmið sýni öll 16 tímabil á völdum þjónustudegi, án frekari
  takmarkana. **Rök**: Einföld sýning BR-1/BR-2. Reglurnar sjálfar tryggja ekki
  framboð allra tímabila; sjá O-3.
- **T-3**: Hafna einnig mótteknum beiðnum um upphaf fyrir kl. 10:00, ranga lengd,
  upphaf utan stundarfjórðungs eða ófullnægjandi dag/tíma. Útskýra leiðréttingu,
  halda gildum upplýsingum og birta staðfestingu á samþykktu tímavali.
  **Rök**: BR-1/BR-2 og H-5. Þetta er tillaga að sértækri viðbótarhegðun, ekki
  viðbót sem þegar hafi verið staðfest í FR-DEL-1/2; sjá O-3.

### Opnar spurningar til rýni

- **O-1 — Prófaheimildir**: Samsvara AT-DEL-LEID-1 og AT-DEL-LEID-2 úr efni 8.2
  prófunum AT-DEL-1 og AT-DEL-2 í lýsingunni? Innihalda þau frekari skilyrði?
  **Áhrif**: Rekjanleiki til efnis 8.2 verður ekki fullstaðfestur án þessarar yfirferðar.
- **O-2 — Staðartími**: Hvaða staður eða tímabelti ræður staðartíma BR-2?
  Á að nota afhendingarstað eins og T-1 leggur til?
  **Áhrif**: Þarf ótvírætt viðmið til að sannprófa tímamörkin.
- **O-3 — Framboð og önnur inntakstilvik**: Á að samþykkja T-2 og T-3 fyrir
  sýnidæmið? Hvaða afhendingardagar eru leyfilegir og hafa liðnir tímar,
  pöntunarfyrirvari eða afkastageta áhrif á sýnileg tímabil?
  **Áhrif**: Afmarkar framboð, viðbótarhöfnun og próf utan upprunalegu AT-lýsinganna.

Drögin eru tilbúin til rýni. Opnu atriðin verða ekki ákveðin sjálfkrafa og engin
áætlana- eða kóðagerð hefst áður en notandi hefur rýnt forskriftina.
