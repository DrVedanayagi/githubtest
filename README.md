# githubtest
ved_infinito
#To convert the given json file to a single dataframe 
#and to extract the output of the dataframe into an excel form


pip install pandas 

import json, os  # to read the json file and too edit the output in the computer

json_dir = "/content/drive/MyDrive/isbi/data"  # change the directory path
final_data = []

for json_file_name in os.listdir(json_dir):
    json_file_path = os.path.join(json_dir, json_file_name)

    with open(json_file_path) as json_file:
        data = json.load(json_file)

        records = data.get("records", [])

        for record in records:
            extracted_info = { "Article Title": record.get("articleTitle", ""),
                "Citation Count": record.get("citationCount", 0),
                "Download Count": record.get("downloadCount", 0),
                "Start Page": record.get("startPage", ""),
                "End Page": record.get("endPage", ""),
                "Abstract": record.get("abstract", ""),
                "Publication Title": record.get("publicationTitle", "")}
              #  "Authors": ", ".join(record.get("authors", []))}

            final_data.append(extracted_info)

df = pd.DataFrame(final_data)
 
excel_file ="/content/drive/MyDrive/isbi/extracted_data.xlsx"  # itself will create a route 
df.to_excel(excel_file, index=False) 

print(f"Data has been saved to {excel_file}")
