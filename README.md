# Spectrum similarity evaluation

This repository contains code to compare several spectrum similarity scores for the discovery of related molecules.

Similarity scores that are currently implemented are:

- Cosine similarity <br/>
   Stein, S. E. & Scott, D. R. Optimization and testing of mass spectral library search algorithms for compound identification. _Journal of the American Society for Mass Spectrometry_ **5**, 859–866 (1994). [doi:10.1016/1044-0305(94)87009-8](https://doi.org/10.1016/1044-0305(94)87009-8)
- Modified cosine similarity <br/>
   Watrous, J. _et al_. Mass spectral molecular networking of living microbial colonies. _Proceedings of the National Academy of Sciences_ **109**, E1743–E1752 (2012). [doi:10.1073/pnas.1203689109](https://doi.org/10.1073/pnas.1203689109)
- Neutral loss similarity <br/>
   Aisporna, A. _et al_. Neutral loss mass spectral data enhances molecular similarity analysis in METLIN. _Journal of the American Society for Mass Spectrometry_ **33**, 530–534 (2022). [doi:10.1021/jasms.1c00343](https://doi.org/10.1021/jasms.1c00343)
- Modified neutral loss similarity

## Installation

Create a conda enviroment and install all required dependencies using the provided `environment.yml` file:

```
conda env create -f https://raw.githubusercontent.com/bittremieux/cosine_neutral_loss/master/environment.yml
```

## Usage

Code example to create mirror plots using different similarity scores:

```
import spectrum_utils.spectrum as sus

import plot


usi1 = "mzspec:GNPS:GNPS-LIBRARY:accession:CCMSLIB00000424840"
usi2 = "mzspec:MSV000086109:BD5_dil2x_BD5_01_57213:scan:760"

spectrum1 = sus.MsmsSpectrum.from_usi(usi1)
spectrum1.precursor_charge = 1
spectrum1 = spectrum1.set_mz_range(0, spectrum1.precursor_mz)
spectrum1 = spectrum1.remove_precursor_peak(0.1, "Da")

spectrum2 = sus.MsmsSpectrum.from_usi(usi2)
spectrum2.precursor_charge = 1
spectrum2 = spectrum2.set_mz_range(0, spectrum2.precursor_mz)
spectrum2 = spectrum2.remove_precursor_peak(0.1, "Da")

plot.plot_mirror(spectrum1, spectrum2, "cosine", "cosine.png")
plot.plot_mirror(
    spectrum1, spectrum2, "modified_cosine", "modified_cosine.png"
)
plot.plot_mirror(spectrum1, spectrum2, "neutral_loss", "neutral_loss.png")
plot.plot_mirror(
    spectrum1, spectrum2, "modified_neutral_loss", "modified_neutral_loss.png"
)
```

![](cosine_neutral_loss.png)

For more advanced functionality, see the source code.

## Contact

For more information you can visit the [official code website](https://github.com/bittremieux/cosine_neutral_loss) or send an email to <wbittremieux@health.ucsd.edu>.
