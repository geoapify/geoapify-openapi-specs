# How to use the Swagger?
1) Pick the yaml file that you want to use. (for example: geocoding.yaml)
2) Paste it into https://editor.swagger.io/.
3) Now you can Swagger requests.

*Note
You need to populate the API_KEY as a request parameter.

# How to generate the client?
1) Pick the yaml file that you want to use. (for example: geocoding.yaml)
2) Paste it into https://editor.swagger.io/.
3) On top you can see the "Generate Client" button.
4) After clicking on it, pick the language for which you want to generate the client. (for example: typescript-angular)
5) Extract the zip file.
6) Move the folder to your Angular project's directory. (rename it to swagger-client)
5) Execute "npm link" on that folder (swagger-client).
6) Execute "npm link swagger-client" on the root directory.
7) Import the following modules in your Angular application -> [ApiModule, HttpClientModule]
8) Now you can use the services declared in ApiModule, for example:
```
  private ipGeolocationAPIService = inject(IPGeolocationAPIService);

  constructor() {
    this.ipGeolocationAPIService.getIPGeolocation("6dc7fb95a3b246cfa0f3bcef5ce9ed9a").subscribe((data) => {
      console.log(data);
    });
  }
```