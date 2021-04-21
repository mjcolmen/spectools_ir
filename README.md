# spectools-ir
Code is created with infrared medium/high-resolution spectroscopy in mind, and often assumes spectra
are in units of Jy and microns.  Users interested in other applications should proceed with caution.  

Users are requested to let the developer know if they are using the code.  Code has been
tested for only a few use cases, and users utilize at their own risk.

# Requirements
Requires internet access to utilize astroquery.hitran and access HITRAN partition function files

Requires the astropy package

#Modules
flux_calculator is a set of python codes to compute line fluxes from an IR spectrum.

slab_fitter is a set of python codes to perform MCMC slab model fits to CO rotation digrams.  Code is currently
under development and is not ready for use.

slabspec is a set of python codes to produce LTE slab model emission spectra of molecules using the HITRAN database.

## Functions
extract_hitran_data extracts relevant data from HITRAN database

calc_fluxes calculates fluxes from spectra

compute_fluxes calculates line fluxes from relevant HITRAN info and model parameters (column density, temperature and solid angle)

make_rotation_diagram makes a rotation diagram from line fluxes

## Usage

```python
from spectools import extract_hitran_data, calc_fluxes, make_rotation_diagram

#Read in HITRAN data
hitran_data=extract_hitran_data('CO',4.6,5.2,vup=1)  #astropy table

#Read in spectral data
infile='AATau_M.fits'

hdulist=fits.open(infile)
data=hdulist[1].data
wave=data['WAVELENGTH'][0]*1e-3
flux=data['FLUX'][0]

#Calculate fluxes
out=calc_fluxes(wave,flux,hitran_data, v_dop=0,fwhm_v=40.,sep_v=200.,cont=1.05,vet_fits=True, plot=True)

rot=make_rotation_diagram(out)
```

A more complete example can be found in docs/example.ipynb

## License
[MIT](https://choosealicense.com/licenses/mit/)

