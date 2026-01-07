# How to deliver this session

🥇 Thanks for delivering this session!

Prior to delivering the workshop please:

1. Read this document and all included resources included in their entirety.
2. Watch the video presentation
3. Ask questions of the content leads! We're here to help!

## Presentation

### Powerpoint

Download the [English version of the Powerpoint presentation](https://aka.ms/AAy25c2).
Speaker notes are available for each slide.

### Video recording

[Watch the recording](https://aka.ms/AAz408e)

### Timing

| Segment                         | Time  |
|---------------------------------|-------|
| Introduction                    | 03:00 |
| Optimal Search Strategies       | 22:30 |
| AGE for PostgreSQL              |  7:00 |
| Agentic retrieval for AI Search |  6:30 |
| Conclusion                      |  1:00 |

## Demos

There are six demos in the presentation, from three different samples:

* **[Zava products database](https://github.com/microsoft/ai-tour-26-zava-diy-dataset-plus-mcp)**: Python scripts that demonstrate different search strategies on a PostgreSQL database.
* **[Agentic Shop](https://github.com/Azure-Samples/postgres-agentic-shop)**: An E2E full-stack app powered by Azure Database for PostgreSQL, showcasing graph query retrieval.
* **[RAG on AI Search](https://github.com/Azure-Samples/azure-search-openai-demo/)**: An E2E full-stack app powered by Azure AI Search, showcasing agentic retrieval.

### Setup

To be able to show the demos yourself, you will need to set up the three codebases. All three codebases are included as submodules in the `src` folder of this repo. Make sure you've cloned the repo with `--recurse-submodules` or run `git submodule update --init --recursive` after cloning.

#### Zava products database

1. Clone [the repo](https://github.com/microsoft/ai-tour-26-zava-diy-dataset-plus-mcp) OR navigate into the `src` folder, where the repo is checked in as a submodule.

    ```bash
    cd ai-tour-26-zava-diy-dataset-plus-mcp
    ```

2. Login with your deployment tenant:

    ```bash
    az login --tenant <your-deployment-tenant-id>
    ```

3. Deploy the necessary infrastructure:

    ```bash
    cd infra && ./deploy.sh
    ```

4. Initialize the database with seed product data:

    ```bash
    ./scripts/init-db.sh
    ```

5. Setup the Python environment and install dependencies:

    ```bash
    python -m venv .venv
    source .venv/bin/activate
    pip install -r requirements-dev.txt
    ```

6. Configure the Azure AI extensions for Azure Database for PostgreSQL:

    ```bash
    python ./scripts/setup_azure_ai.py
    ```

7. Test that each script runs successfully:

    ```bash
    python ./scripts/keyword_search.py
    python ./scripts/vector_search.py
    python ./scripts/hybrid_rrf_search.py
    python ./scripts/hybrid_ranker_search.py
    ```

8. Install the PostgreSQL extension for VS Code and create a new server connection for the provisioned Azure PostgreSQL server. Navigate to zava database, open the retail schema, and use the context menu to visualize the schema.

#### Agentic Shop

1. Clone [the repo](https://github.com/Azure-Samples/postgres-agentic-shop) OR navigate into the `src` folder, where the repo is checked in as a submodule.

    ```bash
    cd postgres-agentic-shop
    ```

2. Create a new azd environment:

    ```bash
    azd env new
    ```

3. Provision the Azure resources and deploy the app:

    ```bash
    azd up
    ```

    * When prompted to select a location, select one close to you.
    * When prompted to pick a resource group, create a new one.
    * When prompted whether you want to deploy container apps, say yes.

4. Navigate to the deployed frontend endpoint and confirm that the application is running. Test the search for "headphones with good reviews about noise cancellation" works.

#### RAG on AI Search

1. Clone [the repo](https://github.com/Azure-Samples/azure-search-openai-demo) OR navigate into the `src` folder, where the repo is checked in as a submodule.

    ```bash
    cd azure-search-openai-demo
    ```

2. Create a new azd environment:

    ```bash
    azd env new
    ```

3. Enable agentic retrieval, set default agentic reasoning effort, and enable web source:

    ```bash
    azd env set USE_AGENTIC_KNOWLEDGEBASE true
    azd env set AZURE_SEARCH_KNOWLEDGEBASE_RETRIEVAL_REASONING_EFFORT medium
    azd env set USE_WEB_SOURCE true
    ```

    You can also choose to enable the Sharepoint source, but then that requires enabling user login, a longer process which may not be feasible on all demo tenants.

4. Copy all the files from the `session-delivery-resources/zava-data` folder into the `data` folder of the azure-search-openai-demo repo:

    ```bash
    cp -r ../session-delivery-resources/zava-data/* ./data/
    ```

5. Provision the Azure resources and deploy the app:

    ```bash
    azd up
    ```

6. Navigate to the deployed endpoint and confirm the app is working. Test the question "Explain how to paint my house most efficiently. Then give me a list of the Zava products and prices for each supply"

### Video recordings

If you'd like, there are videos available for each demo. These videos have audio, which you can choose to mute and talk over.

| Demo                    | Duration | Video - Audio  |
| ------------------------|----------|----------------|
|  1 - Keyword Search     | 3:35     | [aka.ms/AAxryur](https://aka.ms/AAxryur) |
|  2 - Vector Search      | 3:21     | [aka.ms/AAxs6f8](https://aka.ms/AAxs6f8) |
|  3 - RRF Search         | 1:31     | [aka.ms/AAxs6f9](https://aka.ms/AAxs6f9) |
|  4 - Ranker Search      | 1:49     | [aka.ms/AAxsdx4](https://aka.ms/AAxsdx4) |
|  5 - Postgres Shop      | 2:04     | [aka.ms/AAxsdx5](https://aka.ms/AAxsdx5) |
|  6 - Agentic AI Search  | 2:44     | [aka.ms/AAxsdx3](https://aka.ms/AAz24y8) |
