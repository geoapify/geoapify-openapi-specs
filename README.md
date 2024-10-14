# Geoapify OpenAPI specifications

## Overview
The Geoapify OpenAPI specifications provides a convenient way to interact with the Geoapify geolocation services, including:

- Address Autocomplete API (https://apidocs.geoapify.com/docs/geocoding/address-autocomplete/)
- Batch Geocoding API (https://apidocs.geoapify.com/docs/geocoding/batch/)
- Forward Geocoding API (https://apidocs.geoapify.com/docs/geocoding/forward-geocoding/)
- Reverse Geocoding API (https://apidocs.geoapify.com/docs/geocoding/reverse-geocoding/)
- IP Geolocation API (https://apidocs.geoapify.com/docs/ip-geolocation/)
- Routing API (https://apidocs.geoapify.com/docs/routing/)
- Route Matrix API (https://apidocs.geoapify.com/docs/route-matrix/)
- Map Matching API (https://apidocs.geoapify.com/docs/map-matching/)
- Route Planner API (https://apidocs.geoapify.com/docs/route-planner/)
- Isoline API (https://apidocs.geoapify.com/docs/isolines/)

## Configuration

### API Key Configuration
- **API Key**: Ensure to replace `YOUR_API_KEY` placeholder in requests with your actual API key.

## How to use Swagger?

### Option 1: Using Swagger Editor
1) Choose the YAML file that you want to use. For example, `address_autocomplete.yaml`.
2) Open Swagger Editor ([https://editor.swagger.io/](https://editor.swagger.io/)).
3) Paste the content of the YAML file into the editor.
4) You can now interact with the API, view the documentation, and use the **"Try it out"** feature to make sample requests directly from the editor.

### Option 2: Using Local Swagger UI

1) Download or clone this repository to your local machine.
2) In the `index.html` file, multiple Swagger YAML files are pre-configured.
3) To open the Swagger UI, run: "npm start" 
4) By default, Swagger UI will load the first API definition (for example, `Forward Geocoding API`).
5) To switch to another API:
    - Use the **"Select a definition"** dropdown at the top of the page.
    - Choose the API you want to explore, such as `Address Autocomplete API`.
6) After selecting the desired API, Swagger UI will load its documentation and enable you to use the **"Try it out"** feature for testing API endpoints.

*Note
Ensure to replace YOUR_API_KEY in the request parameters with your actual API key before making requests.

## How to generate the client?
1) Choose the YAML file that you want to use. For example, address_autocomplete.yaml.
3) Open Swagger Editor (https://editor.swagger.io/). Paste the content of the YAML file into the editor.
3) At the top of the Swagger Editor, click the "Generate Client" button. Select the language for which you want to generate the client SDK (e.g., typescript-angular).
4) Download the generated client SDK as a .zip file and extract its contents.
6) Move the extracted folder to your Angular project directory. Rename the folder to swagger-client for simplicity.
5) Navigate to the swagger-client folder and run: "npm link"
6) Then, navigate back to the root directory of your Angular project and run: "npm link swagger-client"
7) Import the following modules in your Angular application -> [ApiModule, HttpClientModule]
8) Now you can use the services declared in ApiModule. Example usage:
```
  private ipGeolocationAPIService = inject(IPGeolocationAPIService);

  constructor() {
    this.ipGeolocationAPIService.getIPGeolocation("YOUR_API_KEY").subscribe((data) => {
      console.log(data);
    });
  }
```