---
layout: post
title: 'Battle 1: MODFLOW-NWT output LMT'
date: '2019-10-28T22:53:00.001-07:00'
author: Chang Liao
tags:
- Fortran
- MODFLOW
- MT3D
modified_time: '2019-10-29T12:09:13.248-07:00'
blogger_id: tag:blogger.com,1999:blog-3189999653395802666.post-2516559152926366080
blogger_orig_url: https://codedoesnotlie.blogspot.com/2019/10/battle-1-modflow-nwt-output-lmt.html
---

While I was trying to run the MT3D, I received an error:
Error Reading Flow-Transport Link File Possibly Caused by:
1. Incompatible Styles of Unformatted Files Used by MODFLOW and MT3D-USGS, ensure usage
of FREE in MT3D-USGS name file matches LMT;
2. Unformatted Flow-Transport Link File Saved by Version 1 of LinkMT3D
Package Which Is No Longer Supported by MT3D-USGS.

Based on some initial investigations:
https://water.usgs.gov/nrp/gwsoftware/ModelMuse/Help/index.html?lmt6.htm
"Unformatted – the flow-transport link file is saved as an unformatted (binary) file, compatible with all versions of MT3D and MT3DMS."

So I have to convert the input to unformatted.
However, doing so will yield another error.
This error is basically caused by the undefined variable "FORM" in the source code file lmt8_nwt.f:

IF(ILMTFMT.EQ.0) THEN

          OPEN(IUMT3D,FILE=FNAME,FORM=FORM,ACCESS=ACCESS,

     &      ACTION=ACTION(2),STATUS='REPLACE')

        ELSEIF(ILMTFMT.EQ.1) THEN

          OPEN(IUMT3D,FILE=FNAME,FORM='FORMATTED',ACTION=ACTION(2),

     &      STATUS='REPLACE',DELIM='APOSTROPHE')

ENDIF 
Another quick investigation:
https://docs.oracle.com/cd/E19957-01/805-4939/6j4m0vnaf/index.html
We can replaced the FORM to "UNFORMATTED".

Rebuild the program and the simulation is running again!

Later on it turned out I need to set the LMT to free format in MT3D and MODFLOW should still use FORMATTED.