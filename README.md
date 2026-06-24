==============================================================
  MULTIMODAL VEIN ASSESSMENT TOOL
  Plain English Setup & Run Guide
==============================================================

WHAT IS THIS?
  Three Python scripts that build your AI tool for predicting
  IV cannulation failure. No coding experience needed to run.

--------------------------------------------------------------
STEP 1 — INSTALL PYTHON (if not already installed)
--------------------------------------------------------------
  Download Python 3.10 or newer from:
  https://www.python.org/downloads/
  During install: tick "Add Python to PATH"

--------------------------------------------------------------
STEP 2 — PUT ALL FILES IN ONE FOLDER
--------------------------------------------------------------
  Make a folder on your Desktop called:  vein_ai_project

  Put ALL of these files inside it:
    brain_pipeline.py
    eyes_pipeline.py
    fusion_pipeline.py
    run_all.py
    README.txt
    brain_pipeline_cannulation.csv      ← your brain data
    eyes_pipeline_adiva.csv             ← your eyes data

--------------------------------------------------------------
STEP 3 — INSTALL REQUIRED PACKAGES (do this once only)
--------------------------------------------------------------
  Open a terminal (or Command Prompt on Windows):
    - Windows: press Windows key, type "cmd", press Enter
    - Mac: press Cmd+Space, type "terminal", press Enter

  Copy and paste this command, then press Enter:

  pip install xgboost scikit-learn imbalanced-learn matplotlib seaborn pandas joblib openpyxl

  Wait for it to finish (1–3 minutes).

--------------------------------------------------------------
STEP 4 — RUN THE PROJECT
--------------------------------------------------------------
  In the same terminal, navigate to your folder:
    cd Desktop/vein_ai_project

  Then run:
    python run_all.py

  This runs all 3 pipelines automatically in order.

--------------------------------------------------------------
STEP 5 — CHECK YOUR RESULTS
--------------------------------------------------------------
  After running, your folder will contain these new files:

  brain_results.png    → How well the Brain model performs
                         (ROC curve, confusion matrix, feature importance)

  eyes_results.png     → How well the Eyes model performs
                         (same charts for vein suitability)

  fusion_results.png   → Final PIVC Suitability Index chart
                         Shows GREEN / AMBER / RED for each patient

  brain_model.pkl      → Saved Brain AI model
  eyes_model.pkl       → Saved Eyes AI model

  Open the .png files to see your results visually.

--------------------------------------------------------------
IMPORTANT NOTE — A-DIVA EXCEL FILE (pone_0252166_s001.XLSX)
--------------------------------------------------------------
  The original Excel file has 2 sheets named Blad1 and Blad2.
  'Blad' is the Dutch word for 'Sheet'.

  Blad1 = 1,065 patients — FULL dataset (Phase 1 + Phase 2) ← MAIN
  Blad2 =   610 patients — Phase 1 only, subset of Blad1    ← NOT USED

  The Eyes pipeline (eyes_pipeline_adiva.csv) was exported
  from Blad1 ONLY. Blad2 is a smaller older subset and was
  NOT used in any model training or evaluation.

--------------------------------------------------------------
WHAT DO THE RESULTS MEAN?
--------------------------------------------------------------
  AUC score:
    Above 0.80 = your model is working well
    Above 0.70 = acceptable
    Below 0.70 = needs more data or tuning

  EXPECTED RESULTS FOR THIS PROJECT:
    Brain pipeline (cannulation.sav)  → AUC 0.624  ← small dataset (256 patients)
    Eyes pipeline  (A-DIVA Excel)     → AUC 0.936  ← strong result
    This is NORMAL. Brain AUC below 0.80 is a known limitation
    documented in the project due to limited sample size (256 patients).
    It does NOT mean something went wrong.

  Sensitivity:
    How often the model correctly catches a failed attempt
    Higher = better at flagging difficult cases

  Specificity:
    How often the model correctly identifies easy cases
    Higher = fewer unnecessary alerts

  Fusion Suitability Index:
    GREEN  (≥ 0.70) = proceed with standard cannulation
    AMBER  (≥ 0.45) = use ultrasound guidance
    RED    (< 0.45) = seek senior/specialist help

--------------------------------------------------------------
IF SOMETHING GOES WRONG
--------------------------------------------------------------
  Error: "ModuleNotFoundError"
    → Run the pip install command in Step 3 again

  Error: "FileNotFoundError"
    → Make sure the CSV files are in the same folder as the scripts

  Error: "brain_model.pkl not found"
    → Run brain_pipeline.py first, then eyes_pipeline.py, then fusion

  For any other error, copy the red error text and share it
  with Claude — it will fix it for you.

--------------------------------------------------------------
NEXT STEPS AFTER RUNNING SUCCESSFULLY
--------------------------------------------------------------
  1. Share brain_results.png and eyes_results.png with your
     supervisor or clinical collaborator for review.

  2. Open vein_assessment_app.html in any browser — this is your
     working clinical prototype interface. No Python needed to run it.
     Nurses can enter patient data and get instant GREEN/AMBER/RED output.

  3. Eyes pipeline AUC 0.936 already exceeds your project target.
     Brain pipeline AUC 0.624 is a documented limitation — collecting
     more patients with vein depth + diameter data will improve it.

  4. Collect real ultrasound vein images at a clinical site to upgrade
     the Eyes pipeline from tabular to true image-based vision in future.

==============================================================
