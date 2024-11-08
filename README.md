# SoilWaterRetentionCurveEstimateFunction
Uses arguments of soil texture to generate a soil water retention curve with help from the Rosetta 3 model to generate Van Genuchten hydraulic parameters according to texture.


# This script is intended to assist with irrigation scheduling and management.
# The script is reliant upon accurate soil textural analysis, convergence of the Rosetta 3 model,
# and accurate representation of the management system.

# Functionally, the script uses Van Genuchten parameters as estimated by the Rosetta 3 model
# <https://dsiweb.cse.msu.edu/rosetta/> to derive a soil water retention curve for a selected profile depth to be used for irrigation management.
# The script considers the entire profile depth as 1 homogeneous mixture and applies the specified hydraulic parameters to the entire profile depth.
# It is not recommended to manage irrigation across soil profile depths presenting substantive differences in hydraulic movement.

# The script is a single function taking the following arguments:
# 1) 
#   Managed Soil Profile Depth            - Select the total depth that is managed for irrigation needs. This should NOT be deeper than considerable textural changes, and boundary layers affecting hydraulic movement.
# 2) 
#   Van Genuchten Parameters in a vector
#     Sand Fraction                         - Empirical soil texture analysis, particle size 0.05 mm to 2 mm, expressed as a percentage out of 100 (10 = 10%) 
#     Silt Fraction                         - Empirical soil texture analysis, particle size 0.002 mm to 0.05 mm, expressed as a percentage out of 100 (20 = 20%) 
#     Clay Fraction                         - Empirical soil texture analysis, particle size < 0.002 mm, expressed as a percentage out of 100 (30 = 30%) 
#     Saturated Hydraulic Conductivity      - Enter estimate from the free Rosetta 3 model, <https://dsiweb.cse.msu.edu/rosetta/>, expressed as cm/day
#     Residual Soil Water Content           - Enter estimate from the free Rosetta 3 model, <https://dsiweb.cse.msu.edu/rosetta/>, expressed as water cm3 / profile cm3
#     Saturated Soil Water Content          - Enter estimate from the free Rosetta 3 model, <https://dsiweb.cse.msu.edu/rosetta/>, expressed as water cm3 / profile cm3
#     ~Inverse soil-air entry point (alpha) - Enter estimate from the free Rosetta 3 model, <https://dsiweb.cse.msu.edu/rosetta/>
#     Pore size distribution (n)            - Enter estimate from the free Rosetta 3 model, <https://dsiweb.cse.msu.edu/rosetta/>, dimensionless measure

# The script returns:
# 1)
#   A graphical representation (plot) of the Van Genuchten modeled Soil Water Retention Curve for the entered soil.
#   In this graph, volumetric water content (relative to the 'Depth' argument of the function) is expressed on the Y-axis and corresponding soil matric potential on the X-axis.
#
#   Estimates for saturation, field capacity, and permanent wilting point are given as determined by:
#     A) The Rosetta 3 model <https://dsiweb.cse.msu.edu/rosetta/>
#     B) Experimentation by L.F. Ratliff et. al (1983) "Field-measured limits of soil water availability as related to laboratory-measured properties". Soil Science Society of America Journal. doi: 10.2136/sssaj1983.03615995004700040032x | <https://doi.org/10.2136/sssaj1983.03615995004700040032x>
#        Parameter estimate Error for both estimates are derived from experimentation by Ratliff et. al. (1983)
# 2)
#   A data frame (6 columns by 101 rows) aligning expressions of soil water status across rows.
#     "index":
#     "Managed Profile Water Volume":
#     "Managed Profile Plant Available Water":
#     "Managed Profile Volumetric Water Content":
#     "Estimated Corresponding Soil Matric Potential":
#     "Estimated Irrigation Depth for Refill of Managed Profile Volume":
#
# 3)
#   A printed tibble with Rosetta 3 and Ratliff estimates for:
#     A) USDA Soil Texture Class
#     B) Volumetric Water Content @ Saturation
#     C) Volumetric Water Content @ Field Capacity
#     D) Volumetric Water Content @ Permanent Wilting Point
#     E) Soil Matric Potential @ Saturation
#     F) Soil Matric Potential @ Field Capacity
#     G) Soil Matric Potential @ Permanent Wilting Point
