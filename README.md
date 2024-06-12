import os
import csv

def get_files_structure(base_folder):
    files_structure = []
    for root, dirs, files in os.walk(base_folder):
        for file in files:
            folder = os.path.basename(os.path.dirname(root))
            sub_folder = os.path.basename(root)
            file_name, file_ext = os.path.splitext(file)
            files_structure.append((folder, sub_folder, file_name, file_ext))
    return files_structure

def read_file_content(base_folder, folder, sub_folder, file_name):
    file_path = os.path.join(base_folder, folder, sub_folder, file_name + '.txt')
    if os.path.exists(file_path):
        with open(file_path, 'r', encoding='utf-8') as file:
            return file.read()
    return None

def create_csv(files_data, output_csv):
    with open(output_csv, 'w', newline='', encoding='utf-8') as csvfile:
        fieldnames = ['content', 'class', 'sub classes', 'text name']
        writer = csv.DictWriter(csvfile, fieldnames=fieldnames)
        writer.writeheader()
        for data in files_data:
            writer.writerow(data)

def main(folder1, folder2, output_csv):
    files_structure_folder1 = get_files_structure(folder1)
    files_data = []
    
    for folder, sub_folder, file_name, _ in files_structure_folder1:
        content = read_file_content(folder2, folder, sub_folder, file_name)
        if content:
            files_data.append({
                'content': content,
                'class': folder,
                'sub classes': sub_folder,
                'text name': file_name + '.txt'
            })
    
    create_csv(files_data, output_csv)

# Specify your folder paths
folder1 = 'path_to_folder1'
folder2 = 'path_to_folder2'
output_csv = 'output.csv'

# Run the script
main(folder1, folder2, output_csv)

