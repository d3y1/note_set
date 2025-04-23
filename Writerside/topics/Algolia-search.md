# Algolia search

## Create Algolia application and search index
1. Sign up for an Algolia account.

2. On the Algolia applications page, click **Create Application**.

   Configure application parameters, select a region for your datacenter, and create the application.

3. On the Algolia application page, go to **Data sources | Indices** and click **Create Index**.

   Provide an informative name and create the index.

4. On the index page, go to **Configuration | Facets**, and click **Add an attribute** under **Attributes for faceting**.

   Add two attributes for faceting: **product** and **version**. Make sure both are searchable.

   Do not add them to the list of **Searchable attributes**, only mark them as **searchable** in the **Attributes for faceting** list.

5. Click **Review and Save Settings** and confirm.


## Add Algolia parameters to Writerside build configuration
| variable          | meaning                                                                                                       |
|-------------------|---------------------------------------------------------------------------------------------------------------|
| algolia-id        | Algolia application ID                                                                                        |
| algolia-index     | Algolia index name                                                                                            |
| algolia-api-key   | Algolia Search-Only API Key (public key)                                                                      |
| algolia-show-logo | Show the Algolia logo in search results if you are using their free plan to comply with Algolia's usage terms |

> buildprofiles.xml

```xml
<variables>
    <algolia-id>9TCXX9YCJY</algolia-id>
    <algolia-index>NOTE_SET_INDEX</algolia-index>
    <algolia-api-key>f37d2de2412a22de0f64f63e07fb6af1</algolia-api-key>
    <algolia-show-logo>true</algolia-show-logo>
</variables>
```

## Upload your search index records to Algolia
1. In your repository on GitHub, go to **Settings | Secrets and variables | Actions**, and add a **New repository secret** with the name **ALGOLIA_KEY** and the value of the Admin API Key from your Algolia account.

   You can find the application ID and API keys in your Algolia account settings under API Keys.(Using **Write API Key**)

2. Set up a GitHub Actions workflow that builds your help artifacts as described in **Build and publish on GitHub**. More specifically, make sure that you add a publish-indexes job to the workflow as described in **Upload search indexes**.

After you run this workflow successfully and the publish-indexes job finishes, go to the index in your Algolia account and make sure that the index records have really been uploaded.

After you upload the index records to Algolia, you can check that search works in your published help. You will need to upload new search index records every time you publish a new help build.

