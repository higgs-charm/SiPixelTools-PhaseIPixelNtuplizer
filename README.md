# PhaseIPixelNtuplizer
"PixelTimingStudy" for the Phase I pixel detector

### &#x1F539; Base recipe:

```bash
cmsrel CMSSW_8_1_0_pre8
cd CMSSW_8_1_0_pre8/src
cmsenv
git cms-addpkg SimGeneral/MixingModule
sed -i "95,106d" SimGeneral/MixingModule/python/SiPixelSimParameters_cfi.py
sed -i "84s;digitizer.AddPixelInefficiency = cms.bool(False);digitizer.AddPixelInefficiency = cms.bool(True);" SimGeneral/MixingModule/python/SiPixelSimParameters_cfi.py
git clone https://github.com/jkarancs/PhaseIPixelNtuplizer.git DPGAnalysis/PhaseIPixelNtuplizer
scram b -j 20
ln -s DPGAnalysis/PhaseIPixelNtuplizer/python/PhaseINtuplizer_GenNu_DynIneffDB_cfg.py .
cmsRun PhaseINtuplizer_GenNu_DynIneffDB_cfg.py
```

### &#x1F539; Starting from GEN-SIM
The PhaseINtuplizer_GenNu_DynIneffDB_cfg.py uses neutrino signals (nothing) as a base input, and mixes events to it using GEN-SIM data generated with CMSSW_8_1_0pre8 to achieve flat pileup. Right now the mixing step is really slow, and eats too much memory.

### &#x1F539; Running on Reco
Running on RECO output seems to be impossible right now since the track refitting does not seem to work yet. If you manage to run the refitter step, please send in a pull request.

### &#x1F539; No pileup
If you don't need pileup, it is really fast to generate Ntuples starting with RAW2DIGI -> RECO. Example file: test/RAWTODIGI_RECO_test.py.
