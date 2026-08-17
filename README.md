# Clone sources
git clone https://github.com/cran/anchors.git
git clone https://github.com/JasjeetSekhon/rgenoud.git

# Build and install rgenoud without vignettes (avoids LaTeX issues)
cd rgenoud
R CMD build . --no-build-vignettes
R CMD INSTALL rgenoud_5.9-0.3.tar.gz

# Patch anchors C sources to replace legacy Sint typedef with int
cd ../anchors
powershell -Command "Copy-Item anchors.c anchors.c.bak; (Get-Content anchors.c.bak) -replace '\bSint\b','int' | Set-Content anchors.c"
powershell -Command "Copy-Item conjure.c conjure.c.bak; (Get-Content conjure.c.bak) -replace '\bSint\b','int' | Set-Content conjure.c"

(This is for Windows, if you're on Linux I doubt you need these instructions.)

# Build and install anchors
R CMD build .
R CMD INSTALL anchors_3.0-8.tar.gz
