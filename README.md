# Using Kotlin in a Serverless Architecture with AWS Lambda
Complete code per article for the complete series in medium https://medium.com/@juancho088/using-kotlin-in-a-serverless-architecture-with-aws-lambda-part-1-setting-up-the-project-87033790e2f4

# First Steps

1. Install nodeJS (download [link](https://nodejs.org/en/download/))
2. Run the command `npm install -g serverless`
3. Create your project running the command `serverless create —-template aws-kotlin-jvm-gradle --path your_service`
4. To configure your AWS credentials execute `serverless config credentials --provider aws --key EXAMPLE --secret EXAMPLEKEY`

# Package JSON

1. Create a package.json file with the minimum information so you can install serverless libraries.
```
{
  "name": "my-blockbuster",
  "version": "1.0.0"
}
```

# Plugins

## Serverless to SAM Local

You must have a functional Docker client on the system you plan to use SAM, so install that first if you don’t yet have it!

```
npm install --save-dev serverless-sam
```

Add the plugin in the serverless.yml file:

```
plugins:
  - serverless-sam
```

Compile your function using Shadow, that will generate a set of files in *build/libs/*:

````
gradle build shadowJar
````

Export and invoke your functions

```
sls sam export -o template.yml
sam local invoke hello <<< "{}"
```

*Note:* You will always need to run this command every single time you want to test your lambda function.
Also, by default the function names will start with capitalize letter.

To invoke custom event.json files you can execute the next command:

```
$ sam local invoke Hello -e src/main/resources/event.json
```