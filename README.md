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


repo_path = "/" 
branch_name = "Visualisation"
file_name = "interactive_coal_data_faceted.html"
file_path = "/Users/soofiya/Downloads/interactive_coal_data_faceted.html"  
commit_message = "Add interactive coal data graph"
remote_name = "origin"  # Usually "origin" for GitHub

# Change to the repository directory
os.chdir(repo_path)

# Checkout the existing visualization branch
if not run_command(f"git checkout {branch_name}"):
    print(f"Failed to checkout {branch_name} branch")
    exit(1)

# Pull the latest changes from the remote branch
if not run_command(f"git pull {remote_name} {branch_name}"):
    print(f"Failed to pull latest changes from {branch_name}")
    exit(1)

# Copy the HTML file from storage to the repository
try:
    shutil.copy2(file_path, os.path.join(repo_path, file_name))
    print(f"Copied {file_name} to the repository")
except Exception as e:
    print(f"Failed to copy the file: {str(e)}")
    exit(1)

# Add the HTML file
if not run_command(f"git add {file_name}"):
    print("Failed to add the HTML file")
    exit(1)

# Commit the changes
if not run_command(f'git commit -m "{commit_message}"'):
    print("Failed to commit changes")
    exit(1)

# Push the changes to GitHub
if not run_command(f"git push {remote_name} {branch_name}"):
    print("Failed to push to GitHub")
    exit(1)

print(f"Successfully pushed {file_name} to {branch_name} branch on GitHub")

# Generate the GitHub preview link
github_username = "your_github_username"  # Replace with your GitHub username
repo_name = "Data Analysis"  # Replace with your actual repository name

preview_link = f"https://htmlpreview.github.io/?https://github.com/{github_username}/{repo_name}/blob/{branch_name}/{file_name}"
print(f"\nYou can view your interactive graph at:\n{preview_link}")

# Instructions for adding link to README
print("\nTo add this link to your README.md, you can use the following Markdown:")
print(f"[View Interactive Coal Data Graph]({preview_link})")

### References
<a href =https://ourworldindata.org >Our World in Data </a>


<a href = https://www.energyinst.org/statistical-review>Statistical review of world energy (Energy Institute, EI) </a>

<a href = https://www.eia.gov/opendata/index.php#bulk-downloads>International energy data (U.S. Energy Information Administration, EIA</a>

<a href = https://www.theshiftdataportal.org/energy> Energy from fossil fuels (The Shift Dataportal)</a>

<a href = https://ember-climate.org/data-catalogue/yearly-electricity-data/> Yearly Electricity Data (Ember </a>

<a href =https://ember-climate.org/insights/research/european-electricity-review-2022/ > European Electricity Review (Ember) </a>

<a href = https://github.com/owid/etl/blob/master/etl/steps/data/garden/ember/2023-07-10/combined_electricity.py> Combined Electricity (Our World in Data based on Ember's Yearly Electricity Data and European Electricity Review)</a>

<a href = https://github.com/owid/etl/blob/master/etl/steps/data/garden/energy/2023-07-10/energy_mix.py > Energy mix (Our World in Data based on EI's Statistical review of world energy ) </a>

<a href = https://github.com/owid/etl/blob/master/etl/steps/data/garden/energy/2023-07-10/fossil_fuel_production.py >Fossil fuel production (Our World in Data based on EI's Statistical review of world energy & The Shift Dataportal's Energy from fossil fuels)</a>

<a href = https://github.com/owid/etl/blob/master/etl/steps/data/garden/energy/2023-07-10/primary_energy_consumption.py>Primary energy consumption (Our World in Data based on EI's Statistical review of world energy & EIA's International energy data)</a> 


