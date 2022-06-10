# snyk-deps-to-csv

Collects all dependencies from either:

* All orgs in a group
* A specific org
* A specific repo/target (ex: my-scm-org/repo)

and outputs the dependencies to a CSV file `snyk-deps_<timestamp>.csv`, see an example [here](sample-output/snyk-deps_2022_01_05_05_40_39_59.csv).

> To process all Snyk orgs in a group, ensure your token has group level permission.  If the token in use only has access to specific orgs in the group, only the data from those orgs will be retrieved.

Please try to avoid running for all dependencies against your snyk group(s) more than 1x or 2x per day.

## To run
install with `npm install`

build with `npm run build`

### Get all dependencies from all orgs in the specified group
```
node dist/index.js --token=$SNYK_TOKEN --group-id=$SNYK_GROUP
```

### Filter by a specific org
```
node dist/index.js --token=$SNYK_TOKEN --group-id=$SNYK_GROUP \
     --org-id=$SNYK_ORG"
```

### Filter by a specific org and repo/target
```
node dist/index.js --token=$SNYK_TOKEN --group-id=$SNYK_GROUP \
     --org-id=$SNYK_ORG" --target=foo/bar
```

### Filter by 1 or more dependencies from all orgs in the specified group
```
node dist/index.js --token=$SNYK_TOKEN --group-id=$SNYK_GROUP \
     --dependency-list="ansi-regex@2.0.0,assert-plus@1.0.0"
```

### Filter by dependencies file from all orgs in the specified group (*nix example)

Log4Shell:

```
node dist/index.js --token=$SNYK_TOKEN --group-id=$SNYK_GROUP \
     --dependency-list="$(cat example-deps-files/log4j-core_deps.txt | xargs | sed -e 's/ /,/g')"
```

Spring4Shell:

```
node dist/index.js --token=$SNYK_TOKEN --group-id=$SNYK_GROUP \
     --dependency-list="$(cat example-deps-files/spring4shell_deps.txt | xargs | sed -e 's/ /,/g')"
```

## Contributing
contributions are welcomed for this project, following the [contribution guidelines](.github/CONTRIBUTING.md)

## Issues
for any issues or questions, please submit a [github issue](https://github.com/snyk-tech-services/snyk-deps-to-csv/issues)

## License
[License: Apache License, Version 2.0](LICENSE)
