---
layout:     post
title:      GEANTV的G4集成
category: blog
description: GEANTV的G4集成。
---

       Developer notes to run Geant4 applications using USolids/VecGeom shapes
       =======================================================================


See README file GEANT4_INSTALL.md for configuration of VecGeom and installation
of Geant4 with either USolids and VecGeom shapes implementations.

* Building a Geant4 example for testing

  =====================================

This tutorial uses Geant4 example under ${G4SOURCE}/examples/basic/B1:

  #.. copy the basic/B1 example source tree from G4 release area
  cd $TOPDIR
  mkdir b1
  cp -r ${G4SOURCE}/examples/basic/B1/*  b1/

This example has been extended, to include a larger set of shapes to be
exercised.
The modified files are needed:

  #.. copy modified files which instantiate more shapes for testing
  cd ${TOPDIR}/b1/src
  wget http://home.fnal.gov/~lima/download/B1DetectorConstruction.cc
  wget http://home.fnal.gov/~lima/download/B1PrimaryGeneratorAction.cc

  #.. build B1 example against USolids version of Geant4
  MODE=usolids
  source ${TOPDIR}/geant/install-${VERSION}-${MODE}/bin/geant4.sh
  mkdir ${TOPDIR}/b1/build-${MODE}
  cd ${TOPDIR}/b1/build-${MODE}
  cmake -DGeant4_DIR=${TOPDIR}/geant/install-${VERSION}-${MODE}/lib/Geant4-10.2.0  ..
  make -j8

Then repeat the last block above for MODE=vecgeom.

At this point, if no errors were observed, both USolids-based and VecGeom-based
Geant4 jobs are ready to be run.


* Running and testing

The runtime setup is much simpler, and in principle, none of the steps above are
needed. A setup script is available to help with this:

  cd ${TOPDIR}/b1
  wget http://home.fnal.gov/~lima/download/setmeup.sh

The file setmeup.sh must be adapted according to the local environment,
especially the TOPDIR environment variable.

A typical session would then look like this:

  #.. set up to run for either mode (e.g. vecgeom)
  cd ${TOPDIR}/b1

  #.. run the Geant4 job 
  source setmeup.sh geant4
  build
  exampleB1 run1.mac

  #.. run the USolids-based job 
  source setmeup.sh usolids
  build
  exampleB1 run1.mac

  #.. run the VecGeom-based job 
  source setmeup.sh vecgeom
  build
  exampleB1 run1.mac


A callgrind session can be used to show that vecgeom shapes are actually used:

  valgrind --tool=callgrind exampleB1 run1.mac

  kcachegrind callgrind.out.<PID>


Please send any comments to lima@fnalSPAMNOT.gov.

[BeiYuu]:    http://beiyuu.com  "BeiYuu"