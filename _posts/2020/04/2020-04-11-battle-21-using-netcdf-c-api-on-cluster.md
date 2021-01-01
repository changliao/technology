---
layout: post
title: 'Battle 21: Using NetCDF C++ API on cluster'
date: '2020-04-11T14:55:00.001-07:00'
author: Chang Liao
tags:
- C++
- HexCoastal
- HexWatershed
- NetCDF
- API
- GDAL
modified_time: '2020-04-11T14:55:52.437-07:00'
blogger_id: tag:blogger.com,1999:blog-3189999653395802666.post-2056059825376076399
blogger_orig_url: https://codedoesnotlie.blogspot.com/2020/04/battle-21-using-netcdf-c-api-on-cluster.html
---

I have extended the capability of HexWatershed, which allows it to read MPAS 
mesh grid. 

Some background information for the above statement. 
HexWatershed is a C++ program I developed to delineate watershed using a 
hexagonal mesh grid. Details of the program are introduced in this paper: 
Watershed delineation on a hexagonal mesh grid 
(https://www.sciencedirect.com/science/article/pii/S1364815219308278) 

MPAS mesh is an unstructured mesh used for ocean and atmosphere modeling 
(https://mpas-dev.github.io/files/documents/MPAS-MeshSpec.pdf). 

In order to support this new mesh, I have added the NetCDF I/O into the 
system. However, the NetCDF API for C++ is not widely used by the research 
community. For example, most Earth System Models (ESMs) use the Fortran 90 
instead of C++. 

A few hydrology programs (i.e., DHSVM) using the NetCDF C API which is less 
OOP oriented. 

So I have to setup the NetCDF C++ API on the cluster. First I requested the 
C++ API, however, there are significant changes between the legacy API and the 
NetCDF4 API: 
https://github.com/Unidata/netcdf-cxx4 

After that, we are able to use namespace and other new features in C++11. 
In order to link the library, we need both the C and C++ libraries in the 
CMakeLists file: 
set(NetCDF_LIBRARY_C "/share/apps/netcdf/4.6.3/gcc/8.1.0/lib/libnetcdf.so") 

set(NetCDF_LIBRARY "/share/apps/netcdf/4.6.3/gcc/8.1.0/lib/libnetcdf_c++4.so") 

Besides, I used the VTK FindNetCDF to setup NetCDF: 
https://github.com/Kitware/VTK/blob/master/CMake/FindNetCDF.cmake 

The program compiled and linked. 