FROM cardiacmodelling/appredict-chaste-libs:1.0.0

################################################################################
# Modifiable (e.g. via command line) args.                                     #
################################################################################

ARG appredict_tag=v2024.1
ARG chaste_tag=2024.1
ARG build_processors=1

################################################################################
# Local vars (not for modification!)                                           #
################################################################################

ENV dir_appredict="${HOME}/apps/ApPredict"
ARG dir_build="${HOME}/build"

################################################################################
# 1. Build ApPredict from source                                               #
################################################################################

#------------------------------------------------------------------------------#
# 1.1. Download Chaste & ApPredict source                                      #
#------------------------------------------------------------------------------#
WORKDIR ${HOME}
RUN git clone -b ${chaste_tag} --recursive --depth 1 https://github.com/Chaste/Chaste.git Chaste

WORKDIR ${HOME}/Chaste/projects
RUN git clone -b ${appredict_tag} --recursive --depth 1 https://github.com/Chaste/ApPredict.git

WORKDIR ${HOME}/Chaste/projects/ApPredict/src/cellml/cellml/
RUN find . ! -name shannon_wang_puglisi_weber_bers_2004.cellml ! -name ten_tusscher_model_2006_epi.cellml ! -name mahajan_shiferaw_2008.cellml ! -name hund_rudy_2004.cellml ! -name grandi_pasqualini_bers_2010_ss.cellml ! -name ohara_rudy_2011_endo.cellml ! -name paci_hyttinen_aaltosetala_severi_ventricularVersion.cellml ! -name ohara_rudy_cipa_v1_2017.cellml -delete

##------------------------------------------------------------------------------#
## 1.2. Build ApPredict and deploy                                              #
##------------------------------------------------------------------------------#

RUN mkdir -p ${dir_build}
WORKDIR ${dir_build}
RUN cmake -j ${build_processors} \
    -DCMAKE_BUILD_TYPE=Release \
    -DChaste_ERROR_ON_WARNING=OFF \
    -DChaste_UPDATE_PROVENANCE=ON \
    -DChaste_USE_VTK=OFF \
    ../Chaste

RUN make -j ${build_processors} ApPredict

RUN mkdir -p ${dir_appredict}
COPY --chown=appredict:appredict ApPredict.sh ${dir_appredict}/ApPredict.sh
RUN chmod +x ${dir_appredict}/ApPredict.sh

RUN ln -s ${dir_build}/projects/ApPredict/apps/ApPredict ${dir_appredict}/ 

ENV CHASTE_TEST_OUTPUT=${dir_appredict}/testoutput

WORKDIR ${HOME}
