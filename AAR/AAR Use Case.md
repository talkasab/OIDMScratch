
# Advanced Assisted Reporting Sample User Stories

## AI-detected Nodule Pulmonary Nodule Advisor

An AI tool has detected pulmonary nodules and the Advanced Assisted Reporting Encapsulation Server (AARES) has detected that data from PIN (encoded as FHIR, labeled with Common Data Element [CDE] IDs) and incorporated it into the Diagnostic Reporting Context Object Model (DRCOM). The Pulmonary Nodule Advisor (PNA) detects the presence of the pulmonary nodule in the DRCOM and process it to suggest the following report text for the radiologist:

> **Findings:**  Non-calcified 7 mm solid nodule in the right middle lobe (series 2, image 24) is indeterminate.
> 
> **Impression:** Indeterminate solid pulmonary nodule measuring 7 mm.
>
> **Recommendation:** In a patient of unknown risk level with a solid nodule of 6-8 mm, recommend CT at 6-12 month. If unchanged at that time, in a low-risk patient, then consider CT at 18-24 month. In a high-risk patient, if the nodule is stable at 6-12 month, recommend CT at 18-24 month.

The radiologist chooses to insert the report text.

## Radiologist Dictates a Nodule

The radiologist then dictates the description of an additional pulmonary nodule that had not been detected by the AI. The Clinical Language Understanding (CLU) service detects that description and extracts a structured description of the nodule into the DRCOM, where the PNA detects it and updates its generated text to reflect the new, multiple-nodule scenario:

> **Findings:**
> Multiple pulmonary nodules seen:
> | Location     |  Size | Consistency  |
> |--------------|-------|--------------|
> | Right Middle |  7 mm | Solid        |
> | Right Upper  | 11 mm | Ground glass |
> 
> **Impression:** Multiple pulmonary nodules, the most concerning being an 11 mm ground glass nodule in the right middle lobe. 
>
> **Recommendation:** Follow-up CT at 3-6 months. Subsequent management based on most suspicious nodule.

The radiologist replaces the prior report text with the new text.

## "Did You Forget?" Asks about Adrenal Nodules

When the radiologist clicks off to sign their report, the tool compares the report the radiologist has created with prior reports and notices that prior reports have included descriptions of a left adrenal nodule and the current report does not mention the nodule. A dialog box comes up that says:

> ###  "Did you forget?"
> Prior reports on this patient's exams of type "CT.TH.CHEST+" (most recently 2021-09-20) have included
> a finding which doesn't seem to be in this report:
> - **Left adrenal nodule**
> 
> Would you like to return to your report and describe this lesion, or continue signing?

Final report:

> **CT CHEST WITH CONTRAST**
> 
> **TECHNIQUE**: Multidetector CT of the chest was performed with intravenous contrast using tailored
> dose modulation techniques.
> 
> **COMPARISON**: CT CHEST WITH CONTRAST 2021-Sep-20
> 
> **FINDINGS**:
> 
> **Devices/Tubes/Lines**: None.
> 
> **Lungs**: Central airways are patent. Diffuse bronchial wall thickening. Multiple pulmonary nodules:
> | Location     |  Size | Consistency  |
> |--------------|-------|--------------|
> | Right Middle |  7 mm | Solid        |
> | Right Upper  | 11 mm | Ground glass |
>
> **Pleura**: No pleural effusion or pneumothorax.
> 
> **Mediastinum**: Neck findings reported separately. The heart is normal in size. No pericardial > effusion. Moderate coronary arterial calcifications. Minimal residual thymus is present in the anterior > mediastinum. Small hiatal hernia with unchanged mild distal esophageal wall thickening.
> 
> **Lymph Nodes**: No enlarged supraclavicular, axillary, mediastinal, or hilar lymph nodes.
> 
> **Upper Abdomen**: No abnormality in the visualized spleen. Cholelithiasis. Partially imaged 2.6 cm > low-attenuation lesion in the right kidney, likely a cyst. Unchanged 1.2 cm hypodensity in the left hepatic lobe. Unchanged nodule in the left adrenal.
> 
> **Chest Wall**: No chest wall mass.
> 
> **Bones**: No suspicious lytic or blastic lesions.
> 
> **IMPRESSION:**
> - Multiple pulmonary nodules, the most concerning being an 11 mm ground glass nodule in the right middle lobe. 
> - No intrathoracic lymphadenopathy.
> 
> **RECOMMENDATION:**
> 
> Follow-up CT at 3-6 months. Subsequent management based on most suspicious nodule.