# Algolia search

## Create Algolia application and search index

<procedure>
   <step>
      <p>Sign up for an Algolia account.</p>
   </step>
   <step>
      <p>On the Algolia applications page, click <control>Create Application</control>.</p>
      <p>Configure application parameters, select a region for your datacenter, and create the application.</p>
   </step>
   <step>
      <p>On the Algolia application page, go to <ui-path>Data sources | Indices</ui-path> and click <control>Create Index</control>.</p>
      <p>Provide an informative name and create the index.</p>
   </step>
   <step>
      <p>On the index page, go to <ui-path>Configuration | Facets</ui-path>, and click <control>Add an attribute</control> under <path>Attributes for faceting</path>.</p>
      <p>Add two attributes for faceting: <path>product</path> and <path>version</path>. Make sure both are searchable.</p>
      <p>Do not add them to the list of <path>Searchable attributes</path>, only mark them as <control>searchable</control> in the <path>Attributes for faceting</path> list.</p>
   </step>
   <step>
      <p>Click <control>Review and Save Settings</control> and confirm.</p>
   </step>
</procedure>

## Add Algolia parameters to Writerside build configuration
| variable          | meaning                                                                                                       |
|-------------------|---------------------------------------------------------------------------------------------------------------|
| algolia-id        | Algolia application ID                                                                                        |
| algolia-index     | Algolia index name                                                                                            |
| algolia-api-key   | Algolia Search-Only API Key (public key)                                                                      |
| algolia-show-logo | Show the Algolia logo in search results if you are using their free plan to comply with Algolia's usage terms |

```xml
<variables>
    <algolia-id>9TCXX9YCJY</algolia-id>
    <algolia-index>NOTE_SET_INDEX</algolia-index>
    <algolia-api-key>f37d2de2412a22de0f64f63e07fb6af1</algolia-api-key>
    <algolia-show-logo>true</algolia-show-logo>
</variables>
```
{collapsible="true" collapsed-title="buildprofiles.xml" default-state="expanded"}

## Upload your search index records to Algolia

<procedure>
   <step>
      <p>In your repository on GitHub, go to <ui-path>Settings | Secrets and variables | Actions</ui-path>, and add a <path>New repository secret</path> with the name <path>ALGOLIA_KEY</path> and the value of the Admin API Key from your Algolia account.</p>
      <p>You can find the application ID and API keys in your Algolia account settings under API Keys.(Using <path>Write API Key</path>)</p>
   </step>
   <step>
      <p>Set up a GitHub Actions workflow that builds your help artifacts as described in <a href="Build-and-publish-on-GitHub.md"><control>Build and publish on GitHub</control></a>. More specifically, make sure that you add a publish-indexes job to the workflow as described in <path>Upload search indexes</path>.</p>
   </step>
</procedure>

After you run this workflow successfully and the publish-indexes job finishes, go to the index in your Algolia account and make sure that the index records have really been uploaded.

After you upload the index records to Algolia, you can check that search works in your published help. You will need to upload new search index records every time you publish a new help build.

