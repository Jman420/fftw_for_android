# Building FFTW for Android

The [build_fftw.ps1](build_fftw.ps1) script is a PowerShell script which will automatically generate the necessary Android Make files for ndk-build to compile FFTW for Android.

## Steps
  - Download the latest build of FFTW from [www.fftw.org](http://www.fftw.org) (do not download from the GitHub repo; those releases are missing necessary files)
  - Unzip the archive to the /jni/ directory
  - Update version numbers in [fftw_config.h](fftw_config.h) file
    * #define PACKAGE_STRING "fftw 3.3.8"
    * #define PACKAGE_VERSION "3.3.8"
    * #define VERSION "3.3.8"
  - Execute the [build_fftw.ps1](build_fftw.ps1) script
  - Resulting files are in /out/ directory

## Notes

### Building FFTW Static Library
By default the [build_fftw.ps1](build_fftw.ps1) script will compile a Shared Library for FFTW.  If you want a Static Library instead execute ```build_fftw.ps1 -LibraryType STATIC```.

### FFTW Precision
The default configuration for FFTW contained within [fftw_config.h](fftw_config.h) will compile FFTW with single precision.  This means that all of the FFTW methods will use float data type for their calculations and will be prefixed with 'fftwf_'.  This is because Android AudioFlinger currently provides and expects float32 as the largest data type it will handle.

To build FFTW with floating point precision simply comment out the following lines in [fftw_config.h](fftw_config.h) and re-run [build_fftw.ps1](build_fftw.ps1) :
  - #define BENCHFFT_SINGLE 1
  - #define FFTW_SINGLE 1
