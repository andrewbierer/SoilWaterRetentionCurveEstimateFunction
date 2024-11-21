# SoilWaterRetentionCurveEstimateFunction
Uses arguments of soil texture to generate a soil water retention curve with help from the Rosetta 3 model to generate Van Genuchten hydraulic parameters according to texture.


This script is intended to assist with irrigation scheduling and management. The script is reliant upon accurate soil textural analysis, convergence of the Rosetta 3 model,
and accurate representation of the provided parameters to site locations.

Functionally, the script uses Van Genuchten parameters as estimated by the Rosetta 3 model <https://dsiweb.cse.msu.edu/rosetta/> to derive a soil water retention curve for a selected profile depth to be used for irrigation management.
The script considers the entire entered profile depth as 1 homogeneous layer and applies the specified hydraulic parameters to the entire profile depth. It is not recommended to manage irrigation across soil profile depths presenting substantive differences in hydraulic movement.

# The script is a single function taking the following arguments:
1) Managed Soil Profile Depth:
   
   Select the total depth that is managed for irrigation needs. This should NOT be deeper than considerable textural changes, and boundary layers affecting hydraulic movement.
2) Van Genuchten Parameters in a vector:
   
     Sand Fraction                         - Empirical soil texture analysis, particle size 0.05 mm to 2 mm, expressed as a percentage out of 100 (10 = 10%)
   
     Silt Fraction                         - Empirical soil texture analysis, particle size 0.002 mm to 0.05 mm, expressed as a percentage out of 100 (20 = 20%)
   
     Clay Fraction                         - Empirical soil texture analysis, particle size < 0.002 mm, expressed as a percentage out of 100 (30 = 30%)
   
     Saturated Hydraulic Conductivity      - Enter estimate from the free Rosetta 3 model, <https://dsiweb.cse.msu.edu/rosetta/>, expressed as cm/day
   
     Residual Soil Water Content           - Enter estimate from the free Rosetta 3 model, <https://dsiweb.cse.msu.edu/rosetta/>, expressed as water cm3 / profile cm3
   
     Saturated Soil Water Content          - Enter estimate from the free Rosetta 3 model, <https://dsiweb.cse.msu.edu/rosetta/>, expressed as water cm3 / profile cm3
   
     ~Inverse soil-air entry point (alpha) - Enter estimate from the free Rosetta 3 model, <https://dsiweb.cse.msu.edu/rosetta/>
   
     Pore size distribution (n)            - Enter estimate from the free Rosetta 3 model, <https://dsiweb.cse.msu.edu/rosetta/>, dimensionless measure

# The script returns:
1) A graphical representation (plot) of the Van Genuchten modeled Soil Water Retention Curve for the entered soil. In this graph, volumetric water content (relative to the 'Depth' argument of the function) is expressed on the Y-axis and corresponding soil matric potential on the X-axis.
   Estimates for saturation, field capacity, and permanent wilting point are plotted as determined by A) The Rosetta 3 model <https://dsiweb.cse.msu.edu/rosetta/>; shaded bands indicate the mean and 1 standard deviation for the texture class as determined through experimentation by L.F. Ratliff et. al (1983) "Field-measured limits of soil water availability as related to laboratory-measured properties". Soil Science Society of America Journal. doi: 10.2136/sssaj1983.03615995004700040032x | <https://doi.org/10.2136/sssaj1983.03615995004700040032x>
     
2) A data frame (6 columns by 101 rows) aligning expressions of soil water status across rows.
   
     "index":
   
     "Managed Profile Water Volume":
   
     "Managed Profile Plant Available Water":
   
     "Managed Profile Volumetric Water Content":
   
     "Estimated Corresponding Soil Matric Potential":
   
     "Estimated Irrigation Depth for Refill of Managed Profile Volume":

 3) A printed tibble with Rosetta 3 estimates and Ratliff estimated mean and +- 1 standard deviation for the texture class (where applicable) for:
    
     A) USDA Soil Texture Class
    
     B) Volumetric Water Content @ Saturation
    
     C) Volumetric Water Content @ Field Capacity
    
     D) Volumetric Water Content @ Permanent Wilting Point
    
     E) Soil Matric Potential @ Saturation
    
     F) Soil Matric Potential @ Field Capacity
    
     G) Soil Matric Potential @ Permanent Wilting Point

# Functionally, the script is intended to assist determining irrigation quantities for target thresholds in soil moisture. The script assists users with translation and interpretation of expressions of soil moisture status. Soil matric potential can be readily converted to volumetric water content and plant available water content for the soil of interest.

# Note that hysterectic effects are unaccounted for in the script. The shape of the soil water retention curve varies based upon wetting/drying cycle state and soil properties. 

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

The USDA is an equal opportunity provider and employer. Mention of any names or products are for the purpose of providing specific information only, and should not be construde as recommendation or endorsement.
