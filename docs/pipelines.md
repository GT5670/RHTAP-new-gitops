import os

# Define the phrases and their replacements
replacements = {
    "Red Hat Trusted Application Pipeline": "{ProductName}",
    "RHTAP": "{ProductShortName}"
}

# File extensions to process
target_extension = ".adoc"

def replace_in_file(filepath):
    with open(filepath, "r", encoding="utf-8") as file:
        content = file.read()

    original_content = content
    for target, replacement in replacements.items():
        content = content.replace(target, replacement)

    if content != original_content:
        with open(filepath, "w", encoding="utf-8") as file:
            file.write(content)
        print(f"Updated: {filepath}")

def walk_and_replace(root_dir):
    for dirpath, _, filenames in os.walk(root_dir):
        for filename in filenames:
            if filename.endswith(target_extension):
                replace_in_file(os.path.join(dirpath, filename))

if __name__ == "__main__":
    current_dir = os.path.dirname(os.path.abspath(__file__))
    walk_and_replace(current_dir)
