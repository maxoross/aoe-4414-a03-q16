# sez_to_ecef.py

# Usage: python3 script_name.py arg1 arg2 ...
#  Converts SEZ vector components to ECEF

# Parameters:
#  o_lat_deg: Latitude given in degrees
#  o_lon_deg: Longitude given in degrees
#  o_hae_km: Altitude given in kilometers
# Output:
#  Prints the coordinates in the ecef reference frame (x, y, z), answer in degrees

# Written by Maxwell Oross
# Other contributors: None

# Optional license statement, e.g., See the LICENSE file for the license.

# import Python modules
import math # math module
import sys  # argv

# "constants"
R_E_KM = 6378.1363
E_E    = 0.081819221456

# helper functions
# Calculated Denominator
def calc_denom(ecc, lat_rad):
  return math.sqrt(1.0-(ecc**2)*(math.sin(lat_rad)**2))

# initialize script arguments
o_lat_deg = float(sys.argv[1])
o_lon_deg = float(sys.argv[2])
o_hae_km = float(sys.argv[3])
s_km = float(sys.argv[4])
e_km = float(sys.argv[5])
z_km = float(sys.argv[6])

# parse script arguments
if len(sys.argv)==7:
  o_lat_deg = float(sys.argv[1])
  o_lon_deg = float(sys.argv[2])
  o_hae_km = float(sys.argv[3])
  s_km = float(sys.argv[4])
  e_km = float(sys.argv[5])
  z_km = float(sys.argv[6])
else:
  print(\
   'Usage: '\
   'python3 ecef_to_llh.py r_x_km r_y_km r_z_km'\
  )
  exit()

# write script below this line
#Convert to radians
lat_rad = math.radians(o_lat_deg)
lon_rad = math.radians(o_lon_deg)

# Calculate ECEF
ecef_x1 = (math.cos(lon_rad)*math.sin(lat_rad)*s_km)+(math.cos(lon_rad)*math.cos(lat_rad)*z_km)-(math.sin(lon_rad)*e_km)
ecef_y1 = (math.sin(lon_rad)*math.sin(lat_rad)*s_km)+(math.sin(lon_rad)*math.cos(lat_rad)*z_km)+(math.cos(lon_rad)*e_km)
ecef_z1 = (-math.cos(lat_rad)*s_km)+(math.sin(lat_rad)*z_km)

#Calculate rxyz
denom = calc_denom(E_E, lat_rad)
C_E = R_E_KM / denom
S_E = (R_E_KM * (1 - E_E * E_E)) / denom
r_x_km = (C_E + o_hae_km) * math.cos(lat_rad) * math.cos(lon_rad)
r_y_km = (C_E + o_hae_km) * math.cos(lat_rad) * math.sin(lon_rad)
r_z_km = (S_E +o_hae_km) * math.sin(lat_rad)

#Final ECEF vector
ecef_x_km = ecef_x1+r_x_km
ecef_y_km = ecef_y1+r_y_km
ecef_z_km = ecef_z1+r_z_km

#Final answers
print(ecef_x_km)
print(ecef_y_km)
print(ecef_z_km)
