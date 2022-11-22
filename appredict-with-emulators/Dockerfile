FROM cardiacmodelling/appredict-no-emulators:0.0.9

################################################################################
# Modifiable (e.g. via command line) args.                                     #
################################################################################

ARG build_processors=1


################################################################################
# 1. Download emulators and create binary versions of them.                    #
################################################################################
COPY --chown=appredict:appredict emulators_*.sh ${dir_appredict}/

RUN chmod +x ${dir_appredict}/*.sh

RUN cd ${dir_appredict} && \
    ./emulators_fetch.sh && \
    ./emulators_bin_gen.sh ${build_processors} ./ApPredict.sh && \
    rm -rf *generator.arch *.tgz emulators_*.sh output

WORKDIR ${HOME}
