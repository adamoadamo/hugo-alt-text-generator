# Hugo Alt Text Generator

This project integrates Azure Computer Vision into a Hugo framework to automatically generate alt text for images in markdown files hosted on GitHub Pages. The alt text generation is carried out through a GitHub Actions workflow which uses a Python script.

## Getting Started

1. Set up a Hugo website and host it on GitHub Pages.
2. Obtain Azure Computer Vision API credentials and set them as secrets in your GitHub repository.
   
   - `VISION_ENDPOINT`
   - `AZURE_ACCOUNT_REGION`
   - `AZURE_ACCOUNT_KEY`
   
3. Store the Python script in a directory named `assets/scripts` in your GitHub repository.

## GitHub Actions Workflow

The workflow is defined in a YAML file with the following environment variables:

- `VISION_ENDPOINT`: The endpoint for the Azure Computer Vision API.
- `ACCOUNT_REGION`: The region of your Azure account.
- `ACCOUNT_KEY`: Your Azure account key.

The workflow executes the following steps:

1. **Checkout Code**: Checks out the code from the master branch using a personal access token.
2. **Setup Python**: Sets up a Python 3.11 environment.
3. **Install Dependencies**: Installs the necessary Python packages.
4. **Run Python Script**: Executes the Python script to generate alt texts.
5. **Add changes to git**: Adds the modified files to the git index.
6. **Commit changes**: Commits the changes with a generic message, if there are any changes.
7. **Push changes**: Pushes the changes back to the master branch, if there are any commits.

## Python Script
 
The Python script, stored at `./assets/scripts/alt-text.py`, performs the following actions:

- Retrieves the necessary environment variables (`ACCOUNT_REGION`, `ACCOUNT_KEY`) and initializes the Computer Vision Client using the Azure SDK.
- Defines a `get_image_description` function that gets the description of an image from the Azure Computer Vision API.
- Defines an `update_markdown_file` function that updates the alt text of an image in a markdown file based on its description obtained from the API.
- Iterates over all markdown files in the `content/work/` directory, gets the description for each image, and updates the alt text accordingly.

## Usage

Manually trigger the GitHub Actions workflow to generate alt texts for all images in the markdown files. By default, the script is set to check the `content/work/` directory, but you can modify the `SITE_PATH` variable in the Python script to point to the directory where your files are located.

## Contributing

Feel free to fork the project and submit pull requests for any enhancements or fixes.

## License

This project is open-source and available under the [MIT License](LICENSE).

## Acknowledgements

- Azure Computer Vision API
- Hugo
- GitHub Actions
