#11.03.2026  
#Seyeon Hwang  
This is a description of the MonofonIC code modifications made to implement Warm Dark Matter  
You can download MonofonIC here : https://bitbucket.org/ohahn/monofonic/wiki/Home
(The version may differ depending on when you downloaded it.)


To use the CLASS parameters as desired, the CLASS input parameters used in MonofonIC need to be modified.  
You can check the CLASS input paramters used in MonofonIC here : /monofonic/include/cosmology_parameters.hh  
(Understanding the workflow of how cosmological parameters are defined in MonofonIC and applied to both CLASS and MonofonIC makes it easier to follow)  

##CHANGES IN /monofonic/include/cosmology_parameters.hh  
1)Omega_c  
1-1) MonofonIC defines Omega_c as Omega_c = Omega_m - Omega_b - Omega_nu_massive (line 173)
1-2) But in my case, I want to define Omega_c myself to make sure that Omega_c = 0 when I use WDM cases.  
So I put Omega_c as a 'input parameter' by adding this line : pmap_["Omega_c"] = cf.get_value_safe<double>("cosmology", "Omega_c", defaultp["Omega_c"]);

2)WDM parameters (N_ncdm, Omega_ncdm, m_ncdm, T_ncdm)
As you may see later, MonofonIC defines these parameters in monofonic/src/plugins/transfer_CLASS.cc.  
However, I want to put these values as input parameters so I also put these line in /monofonic/include/cosmology_parameters.hh  
pmap_["N_ncdm"] = cf.get_value_safe<double>("cosmology", "N_ncdm", defaultp["N_ncdm"]);  
pmap_["Omega_ncdm"] = cf.get_value_safe<double>("cosmology", "Omega_ncdm", defaultp["Omega_ncdm"]);  
pmap_["m_ncdm"] = cf.get_value_safe<double>("cosmology", "m_ncdm", defaultp["m_ncdm"]);  
pmap_["T_ncdm"] = cf.get_value_safe<double>("cosmology", "T_ncdm", defaultp["T_ncdm"]);  
