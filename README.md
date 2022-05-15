# havg

This repository constructs haplotype-annotaed genome graphs.
```sh
git clone https://github.com/NedaTavakoli/havg
cd havg 
# download data
./vcf_download_data.sh
# get dependencies
# get vcftools 
echo "downloading vcftools"
wget https://github.com/vcftools/vcftools/releases/download/v0.1.16/vcftools-0.1.16.tar.gz
tar xzf vcftools-0.1.16.tar.gz && cd vcftools-0.1.16
./autogen.sh
./configure --prefix=$(pwd)
make -j -s && make install
vcftools=$(pwd)
rm -f "vcftools-0.1.16.tar.gz"
echo "vcftools download and compilation finished"

# get bcftools
#Note that bcftools will be installed in the bin directory of bcftools folder
cd $softwarewd
git clone https://github.com/samtools/bcftools.git
cd bcftools
autoreconf -i  # Build the configure script and install files it uses
./configure  --prefix=$softwarewd/bcftools  # Optional but recommended, for choosing extra functionality
make
make install 
bcftools=$(pwd)
echo "bcftools download and compilation finished"
# construct haplotype-annotated variation graph

# Extract list of haplotypes per variant position for each allele

#  To run for all the chromosomes
for i in $(seq 1 22; echo X; echo Y)
do
    ./chr_id_haplotypes.sh ${i}
done    



