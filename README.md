# Dynatrace Data Source Plugin for Grafana

This plugin provides a seamless integration between Dynatrace and Grafana, allowing you to visualize Dynatrace metrics directly in your Grafana dashboards.

## What is the Dynatrace Data Source Plugin?

The Dynatrace Data Source Plugin for Grafana enables you to connect to Dynatrace, fetch metrics, and create beautiful and informative dashboards in Grafana. This integration leverages the power of Dynatrace's monitoring capabilities with Grafana's visualization strengths, providing a comprehensive view of your system's performance.

## Getting started

### Prerequisites

1. [Grafana](https://grafana.com/get) installed and running.
2. A Dynatrace account with an API token. 

### Installation

1. Clone the repository:

   ```bash
   git clone https://github.com/ksverchkov/openorg-dynatrace-datasource
   cd openorg-dynatrace-datasource
   ```

2. Install dependencies:

   ```bash
   npm install
   ```

3. Build the plugin:

   ```bash
   npm run build
   ```

4. Deploy the plugin to your Grafana plugins directory. Typically, this directory is located at `/var/lib/grafana/plugins`. Copy your plugin to this directory:

   ```bash
   cp -r dist /var/lib/grafana/plugins/dynatrace-datasource
   ```

5. Restart Grafana to load the new plugin.

### Configuration

1. Navigate to Grafana and log in.
2. Go to Configuration > Data Sources.
3. Click on "Add data source" and select "Dynatrace".
4. Configure the Dynatrace data source by providing your Dynatrace API URL and API token.
5. Click "Save & Test" to verify the connection.

## Usage

1. Create a new dashboard or select an existing one.
2. Add a new panel to your dashboard.
3. In the panel's data source dropdown, select the Dynatrace data source you configured earlier.
4. Select the metrics you want to visualize from Dynatrace.
5. Customize your panel's visualization settings as needed.

## Development

### Backend

1. Update [Grafana plugin SDK for Go](https://grafana.com/developers/plugin-tools/key-concepts/backend-plugins/grafana-plugin-sdk-for-go) dependency to the latest minor version:

   ```bash
   go get -u github.com/grafana/grafana-plugin-sdk-go
   go mod tidy
   ```

2. Build backend plugin binaries for Linux, Windows, and Darwin:

   ```bash
   mage -v
   ```

3. List all available Mage targets for additional commands:

   ```bash
   mage -l
   ```

### Frontend

1. Install dependencies:

   ```bash
   npm install
   ```

2. Build the plugin in development mode and run in watch mode:

   ```bash
   npm run dev
   ```

3. Build the plugin in production mode:

   ```bash
   npm run build
   ```

4. Run the tests (using Jest):

   ```bash
   npm run test
   npm run test:ci
   ```

5. Spin up a Grafana instance and run the plugin inside it (using Docker):

   ```bash
   npm run server
   ```

6. Run the E2E tests (using Cypress):

   ```bash
   npm run e2e
   ```

7. Run the linter:

   ```bash
   npm run lint
   npm run lint:fix
   ```

## Distributing your plugin

When distributing a Grafana plugin either within the community or privately, the plugin must be signed so the Grafana application can verify its authenticity. This can be done with the `@grafana/sign-plugin` package.

_Note: It's not necessary to sign a plugin during development._

### Initial steps

Before signing a plugin, please read the Grafana [plugin publishing and signing criteria](https://grafana.com/legal/plugins/#plugin-publishing-and-signing-criteria) documentation carefully.

1. Create a [Grafana Cloud account](https://grafana.com/signup).
2. Ensure the first part of the plugin ID matches the slug of your Grafana Cloud account.
3. Create a Grafana Cloud API key with the `PluginPublisher` role.
4. Keep a record of this API key as it will be required for signing a plugin.

### Signing a plugin

#### Using Github actions release workflow

If the plugin is using the GitHub actions supplied with `@grafana/create-plugin`, signing a plugin is included out of the box. The [release workflow](./.github/workflows/release.yml) can prepare everything to make submitting your plugin to Grafana as easy as possible. Before signing the plugin, add a secret to the GitHub repository.

1. Navigate to "settings > secrets > actions" within your repo to create secrets.
2. Click "New repository secret".
3. Name the secret "GRAFANA_API_KEY".
4. Paste your Grafana Cloud API key in the Secret field.
5. Click "Add secret".

#### Push a version tag

To trigger the workflow, push a version tag to GitHub:

1. Run `npm version <major|minor|patch>`.
2. Run `git push origin main --follow-tags`.

## Learn more

Below you can find source code for existing app plugins and other related documentation:

- [Basic data source plugin example](https://github.com/grafana/grafana-plugin-examples/tree/master/examples/datasource-basic#readme)
- [`plugin.json` documentation](https://grafana.com/developers/plugin-tools/reference/plugin-json)
- [How to sign a plugin?](https://grafana.com/developers/plugin-tools/publish-a-plugin/sign-a-plugin)

## Support

For support and queries, please open an issue in this repository. We welcome contributions and feedback from the community to improve this plugin.
