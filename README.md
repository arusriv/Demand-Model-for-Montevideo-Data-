# Demand-Model-for-Montevideo-Data

The main objective of the assignment is to build models and predict **trip generation for study purposes (g2)** and **trip attraction for work purposes (a1)** in Montevideo.  
Montevideo has been divided into a total of **55 TAZ’s (Transportation Analysis Zones)**.  
As per the data, **zone 13** seems to be the most dense in terms of population.

---

## Dataset Information
The dataset was loaded from `GA_Montevideo_raw.RData`.

- The structure was examined using:
  - `summary(df)`
  - `attributes(df)`

### Key Variables
- **Trip-related**
  - `g2`: Number of trips generated for study purposes from a zone
  - `a1`: Number of trips attracted for work purposes to a zone
- **Quantitative Variables**
  - `gt`: Total trips *(not included in the model since it already incorporates g2)*
  - `gtsrh`: Trips for study purposes
  - `sup`: Land area
  - `pobl`: Population
  - `empleo`: Employment
  - `plzesco`: Number of school places
  - `camas`: Number of hospital beds
  - `density`: Population density (`pobl/sup`)
- **Qualitative (Categorical) Variables**
  - `f.resi`: Residential
  - `f.com`: Commercial
  - `f.restau`: Restaurant
  - `f.ocio`: Recreational
  - `f.servi`: Service
  - `f.indu`: Industrial
  - `centro`: City center
  - `f.status`: Socioeconomic status

---

## Key Findings from Profiling
- **Highly correlated variable**: Total trips (`gt`) → excluded from models.
- **Positive correlations**:
  - `density` & `plzesco` (school places)
  - `pobl` (population) → strong predictor of `g2`
- **Categorical factors of importance**:
  - `centro` (city center zones)
  - `f.servi` (service zones)
- **Socioeconomic effect**:
  - `f.status` shows positive correlation.
  - Wealthier zones → more study trips.
  - Lower socioeconomic status (`f.statusBajo`) → negative impact on study trip generation.

---

## Modeling Approach and Results

### 1. Base Model (m1)
- Included all selected numerical predictors.
- **Findings**:
  - Only `pobl` was statistically significant.
  - **R² = 0.7114**
  - VIF values < 5 → no multicollinearity.
  - Marginal plots → `pobl` is a very strong predictor.

### 2. Adding Categorical Factors (m4)
- R² increased to **0.774**.
- Only `pobl` and `f.statusBajo` were significant.
- **Interpretation**:
  - Low socioeconomic areas reduce study-related trip generation.

### 3. Final Model (m4f3 with Log Transformation)
- Applied log transformation.
- Identified influential observations.
- Created dummy variables for:
  - Insignificant population zones
  - Port area zones
- **Model performance**:
  - RSE reduced significantly
  - R² increased to **0.78**
  - F-statistic decreased compared to previous model.

---

## Insights
- **Population (`pobl`)** is the single strongest driver of study-related trips.
- **Socioeconomic status** matters:
  - Higher status → more study trips
  - Lower status → fewer study trips
- **City center** and **service areas** naturally attract more study-related movement.
- Outliers such as port or low-population zones were adjusted with dummy variables for better model fit.

---
