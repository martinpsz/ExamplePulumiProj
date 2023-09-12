# NOTES:

### Project set up:

- I wanted to get practice in testing, mainly Unit but, also in Property and Integration. For unit testing, I installed mocha and the necessary typescript definitions as dev dependencies.

```bash
   npm install mocha @types/mocha ts-node --save-dev
```

- Next, after running 'aws config sso' to set up my AWS profile as 'dev' and storing it in /.aws/config, I ran 

```bash
   pulumi config set aws:profile dev
```

I verified that I was able to connect to AWS by running 'pulumi up' and saw that I could connect and deploy a new S3 bucket. Note, that I had an established connection to my AWS profile via the AWS plugin in VS Code.

- In each, 'Pulumi.yaml' file, the typescript option was set to true.

### Tags as Stack configuration

In the example projects, we had a set of tags that were passed as options to certain Pulumi Resources. Example:

```javascript
   const tags = {
        project: "my-project",
        stack: "my-stack",
        env: "dev",
        owner: "my-name",
        team: "my-team",
        source: "my-source"
    }
```

I found that these could be stored as config settings by putting them under 'config' in the project's 'Pulumi.yaml' file like so:

```yaml
   config: 
     tags.project: 'address-project'
     tags.stack: 'example-pulumi-project'
     tags.env: 'dev'
     tags.owner: 'martin'
     tags.team: 'dev'
     tags.source: 'https://github.com/AFSCME/unionware-connector/tree/main' 
```

The above formatting returns an object like the JS example above when called in the project file by using the following code:

```javascript
   let config = new pulumi.Config()
   let data = config.requireObject('tags')
```
