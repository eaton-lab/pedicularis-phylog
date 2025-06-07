## Sample datasets

* Liu_et_al_2024-Cladistics.txt - This is Pedicularis occurrence data from [Plant 
species diversification in the Himalaya–Hengduan Mountains region: an example from 
an endemic lineage of Pedicularis (Orobanchaceae) in the role of floral 
specializations and rapid range expansions](https://doi.org/10.1111/cla.12596)

### Eaton Lab data
These data sheets are not checked in to the repository. They can be fetched
from google drive or Eaton Lab servers.

* eaton_lab_fieldnotes.csv - Up to date data sheet for Eaton Lab samples from the
google sheet - [Field notes 2018-22](https://docs.google.com/spreadsheets/d/1s2WTV5PSMozhFE-VXS2ekwUQIVcsdw4Zu6ABL04EyBM/edit?gid=1599831623#gid=1599831623)

* Meek_all_fieldnotes.csv - A datasheet from J. Meek that I originally started using
but that might be out of synch with the current data. DO NOT USE.

### Code for parsing the `Meek_all_fieldnotes.csv`
It took a while to get all this working for the wrong data sheet, so I feel
precious about not deleting it.

```
dae_df = pd.read_csv("../example_data/Meek_all_fieldnotes.csv")

# Remove any subspecies or variety information from the species epithet
dae_df["species_epithet"] = dae_df["species_epithet"].str.split().str[0]

# Drop one sample with ambiguous species id
dae_df = dae_df[dae_df["species_epithet"] != "armata/tricolor"]

# Join the genus/species columns to agree with the Liu data
dae_df["Name"] = dae_df["genus"] + "_" + dae_df["species_epithet"]
# Retain only the name and lat/long
dae_df = dae_df[["Name", "longitude", "latitude"]]
# Rename columns for agreement
dae_df.rename(columns={"longitude":"Longitude", 
                    "latitude":"Latitude"}, inplace=True)

# Cleaning NA
pre = len(dae_df)
dae_df = dae_df.dropna()
print(f"Removed nan samples: {pre - len(dae_df)}")

# Removing AK samples
mask = dae_df['Latitude'] < 60
pre = len(dae_df)
dae_df = dae_df[mask]
print(f"Removed AK samples: {pre - len(dae_df)}")

# Selecting only Pedicularis
mask = dae_df["Name"].str.contains("edicularis")
#display(dae_df[~mask])
pre = len(dae_df)
dae_df = dae_df[mask]
print(f"Removed non-Pedicularis samples: {pre - len(dae_df)}")

# Remove unidentified sp. samples
mask = dae_df["Name"].str.endswith(('sp', 'sp.'))
dae_df = dae_df[~mask]
print(f"Removed samples w/o species id: {sum(mask)}")

print(f"Total retained samples: {len(dae_df)}")
```
