# blueprints-modeler

This repo is a suggested template for writing blueprints for FlowBuild.

There are 3 ways you can organize your blueprints.
- You can save a json file according to the structure of a flowbuild blueprint.
- You can save a js file, keeping all the structure of a flowbuild blueprint, but leveraging on some quality-of-life features you can have when using js.
- You can save a js file, but referencing a pre-defined nodeSpec. This situation allows you to reuse node specs instead of having to rewrite the same data over and over.

Always save your blueprints files in the ```blueprints``` folder.

## Examples

There are several examples in the blueprints folder, showcasing different situations.

- multipleFinish.example.json: shows a fully json file.
- *.example.js: several examples of blueprints using js files.
- *.example.nodes.js: those files shows some cases on how to build blueprints from nodeSpecs.

## Scripts 

There are 5 scripts available to help with common tasks when managing blueprints

To run then, use ``` npm run <command> ```

### Export

Run this command to convert your blueprints to json.
All files will be named based on the blueprint name and copied to the export/blueprints folder.

The command will also create a hash for each blueprint and save a summary at /download/me folder.

### Validate

Run this command to validate your blueprint against a FlowBuild server of your choice.
Notice that, in order to this script to work, your engine version should be +7.4.0.

### Pull

Run this command to download all blueprints from a FlowBuild server of your choice.
The blueprints will be copied to download/{NODE_ENV} folder.
The script will also generate a hash for each downloaded blueprint and save into a summary file.

### Compare <base folder> <compare folder>
Run this command to compare hashes from 2 folders on download.
Green names means both are equal
Yellow means the workflow exist on compare folder, bue the hashes do not match.
Red means the workflow was not located on the compare folder.

### Deploy
Run this command to deploy your blueprints at export/blueprints folder to the server of your choice.
The command assumes your flowbuild API has a compare route to deep compare blueprint specs.
The script will call this endpoint to validate and compare your blueprint, if there is any change from the latest version at your server, the blueprint will be published.
Notice that the validation is done for each workflow independently, not as block. Please run the validate script before deploying.

## Envs & Requests

To run the scripts, you will need, at least, a BACKEND_URL variables at your .env file.
If you have a specific implementation to generate tokens, adjust the src/utils/token file accordingly.
Do check the src/utils/requests file if you have any changes on default routes on your flowbuild api router.
