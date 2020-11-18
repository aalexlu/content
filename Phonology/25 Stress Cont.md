# Stress Cont

<u>Basic Parameters of Word Stress Systems</u>

- **dominance (L or R):** determines the side of the foot where the head is located (σ́σ trochaic / σσ́ iambic)
- **directionality (L→R or R→L):** determines the direction in which foot construction scans the stress domain
  - → (σσ)(σσ)σσ… / …σσ(σσ)(σσ) ←
- **boundedness (+ or -):** <u>bounded stress</u> rules build maximally binary stress feet, while <u>unbounded</u> languages put no upper limit on the size of a foot
  - *monosyllabic* (degenerate) feet are motivated both by culminativity and by exhaustivity
  - *culminativity* - every content word must contain one stressed syllable, hence one foot
  - *exhaustivity* - all syllables of a word must be organized into feet
- **quantity-sensitivity (+ or -):** governs the distribution of light and heavy syllables in terminal nodes of feet

## Examples 1

1. **Maranungku:** 'we.le.ˌpe.ne.ˌman.ta

   - *dominance:* L trochaic (σ́σ)
   - *directionality:* L → R
   - *boundedness:* yes, stresses by foot - ('we.le)(ˌpe.ne)(ˌman.ta)
   - *quantity-sensitivity:* no, syllable weight does not matter

2. **Warao:** ji.ˌwa.ra.'na.e

   - *dominance:* L trochaic

   - *directionality:* R → L, strongest on the right

   - *boundedness:* yes - ji (ˌwa.ra)('na.e)

   - *quantity-sensitivity:* no

     <u>Approach</u>

     1. *even-parity words* - (ˌya.pu)(ˌru.ki)(ˌta.ne)('ha.se)
        - tell us what kind of stress foot (iamb or trochee)
     2. *odd-parity words* - yi(ˌwa.ra)('na.e)
        - tell us about directionality and whether degenerate feet are allowed

3. **Mapuche:** (e.'lu)(mu.ˌju)

   - *dominance:* R iambic
   - *directionality:* L → R
   - *boundedness:* yes 
   - *quantity-sensitivity:* no

4. **Weri:** ˌku.li.'pu

   - *dominance:* R iambic? - (ˌku)(li.'pu)
   - *directionality:* R → L
   - *boundedness:* yes
   - *quantity-sensitivity:* no

5. **Piro:** ˌsa.lwa.je.'hka.kna

   - *dominance:* L trochaic
   - *directionality:* **bidirectional**, assign main stress on R, then continue assigning from L - (ˌsa.lwa)je('hka.kna)
   - *boundedness:* yes
   - *quantity-sensitivity:* no

## Stress in OT

<u>Constraints</u>

- **IAMB:** feet are iambic
- **TROCHEE:** feet are trochaic
- **FTBIN:** a foot must be binary (either two moras or two syllables)
- **NONFINALITY:** a foot may not be final
- **ALIGN(ω, Ft, R):** the right edge of a phonological word is aligned with the right edge of a foot - σ(σσ)
- **ALIGN(ω, Ft, L):** the left edge of a phonological word is aligned with the left edge of a foot - (σσ)σ
- **ALIGN(Foot, ω, R):** the right edge of every foot is aligned with the right edge of the phonological word
- **ALIGN(Foot, ω, L):** the left edge of every foot is aligned with the left edge of the phonological word
- **PARSE-σ:** a syllable must be parsed into a foot

### Maranungku Example

- ('we.le)(ˌpe.ne)(ˌman.ta)
- TROCHEE, ALIGN(ω, Ft, L) >> PARSE-σ >> ALIGN(Foot, ω, L)

| welepenemanta                   | TROCHEE | ALIGN(ω, Ft, L) | PARSE-σ | ALIGN(Foot, ω, L) |
| ------------------------------- | ------- | --------------- | ------- | ----------------- |
| **('we.le)(ˌpe.ne)(ˌman.ta)** ⟵ |         |                 |         | #σσσσ, #σσ        |
| (we.'le)(pe.ˌne)(man.ˌta)       | *!**    |                 |         | #σσσσ, #σσ        |
| ('we.le) pe.ne (ˌman.ta)        |         |                 | * ! *   | #σσσσ             |

*ALIGN(Foot, ω, R) - in (1) manta is 4σ from left word alignment (#σσσσ), pene is 2σ from left word alignment (#σσ)*

## Examples 2: Quantity-Sensitivity

- Vowel length and stress often attract each other
- In many languages with iambic stress feet, stressed vowels lengthen
- **quantity sensitivity:** In other languages, also typically those with iambic feet, long vowels attract stress, distrupting the otherwise neat alternating stress pattern

1. **Leti:** (ka.ˌval.kiv.'nut.na), (ˌroː.'ne.nu)
   - *dominance:* L trochaic (σ́σ)
   - *directionality:* R → L
   - *boundedness:* yes
   - *quantity-sensitivity:* yes
     - words with <u>no long vowels</u> show basic stress pattern - ka(ˌval.kiv)('nut.na)
     - words with <u>a long vowel</u> show a different pattern - (ˌroː)('ne.nu)
       - **long vowels attract stress**
   - *extrametrical syllables:* (ˌmaː.'nʷaː)na
2. **Tubatulabal:** (ˌjuː.ˌduː)(ˌjuː.'dat)
   - *quantity-sensitivity:* long vowels preferentially given stress
3. **Kashaya:** (wa.qá)(du.cé)du → (wa.**qáː**)(du.**céː**)du
   - *iambic lengthening*

