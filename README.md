# setup-netbeans-action
A custom Github action that downloads, extracts and caches a NetBeans 
ZIP distribution for building Ant-based NetBeans modules.

## Inputs

### `version`

**Required** The version of the NetBeans distribution to download (e.g. 
'18', '19').

## Outputs

No outputs.

## Example usage

```yaml

steps:
  - uses: actions/checkout@v4
    name: Checkout project

  - uses: actions/setup-java@v4
    name: Set up JDK 11
    with:
      java-version: '11'
      distribution: 'temurin'

  # Setup netbeans distribution directory on github workspace.
  - uses: cjmach/setup-netbeans-action@v1
    name: Setup NetBeans distribution
    with:
      version: '18'  

  # Run the ant command, with the required NetBeans properties set.
  - name: Run the Ant build target
    run: >-
      ant -noinput -buildfile build.xml
      -Dnbplatform.default.netbeans.dest.dir=${{ github.workspace }}/netbeans
      -Dnbplatform.default.harness.dir=${{ github.workspace }}/netbeans/harness
      build
```
