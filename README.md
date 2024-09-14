# An Analysis of World Energy Consumption Data
import subprocess
import os
import shutil

def run_command(command):
    process = subprocess.Popen(command, stdout=subprocess.PIPE, stderr=subprocess.PIPE, shell=True)
    output, error = process.communicate()
    if process.returncode != 0:
        print(f"Error: {error.decode('utf-8')}")
        return False
    return True


repo_path = "https://github.com/ZianaTY/Data-Analysis-" 
branch_name = "Visualisation"
file_name = "interactive_coal_data_faceted.html"
file_path = "/Users/soofiya/Downloads/interactive_coal_data_faceted.html"  
commit_message = "Add interactive coal data graph"
remote_name = "origin"  


os.chdir(repo_path)


if not run_command(f"git checkout {branch_name}"):
    print(f"Failed to checkout {branch_name} branch")
    exit(1)


if not run_command(f"git pull {remote_name} {branch_name}"):
    print(f"Failed to pull latest changes from {branch_name}")
    exit(1)


try:
    shutil.copy2(file_path, os.path.join(repo_path, file_name))
    print(f"Copied {file_name} to the repository")
except Exception as e:
    print(f"Failed to copy the file: {str(e)}")
    exit(1)


if not run_command(f"git add {file_name}"):
    print("Failed to add the HTML file")
    exit(1)


if not run_command(f'git commit -m "{commit_message}"'):
    print("Failed to commit changes")
    exit(1)


if not run_command(f"git push {remote_name} {branch_name}"):
    print("Failed to push to GitHub")
    exit(1)

print(f"Successfully pushed {file_name} to {branch_name} branch on GitHub")


github_username = "your_github_username"  # Replace with your GitHub username
repo_name = "Data Analysis"  # Replace with your actual repository name

preview_link = f"https://htmlpreview.github.io/?https://github.com/{github_username}/{repo_name}/blob/{branch_name}/{file_name}"
print(f"\nYou can view your interactive graph at:\n{preview_link}")


print("\nTo add this link to your README.md, you can use the following Markdown:")
print(f"[View Interactive Coal Data Graph]({preview_link})")
