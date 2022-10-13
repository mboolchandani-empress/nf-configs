# [![nf-core/configs](docs/images/nfcore-configs_logo.png "nf-core/configs")](https://github.com/nf-core/configs) <!-- omit in toc -->


A repository for hosting Nextflow configuration files containing custom parameters required to run nf-core pipelines.

## Adding a new config

If you decide to upload your custom config file to `nf-core/configs` then this will ensure that your custom config file will be automatically downloaded, and available at run-time to all nf-core pipelines, and to everyone within your organisation.
You will simply have to specify `-profile <config_name>` in the command used to run the pipeline.
See [`nf-core/configs`](https://github.com/nf-core/configs/tree/master/conf) for examples.

Before adding your config file to nf-core/configs, we highly recommend writing and testing your own custom config file (as described [above](Using an existing config)), and then continuing with the next steps.

N.B. In your config file, please also make sure to add an extra `params` section with `params.config_profile_description`, `params.config_profile_contact` and `params.config_profile_url` set to reasonable values.
Users will get information on who wrote the configuration profile then when executing a nf-core pipeline and can report back if there are things missing for example.


### Uploading to `nf-configs`

* **add** the custom config file to the [`conf/`](https://github.com/nf-core/configs/tree/master/conf) directory
* **edit** and add your custom profile to the [`nfcore_custom.config`](https://github.com/nf-core/configs/blob/master/nfcore_custom.config) file in the top-level directory of the clone
* **edit** and add your custom profile to the [`README.md`](https://github.com/nf-core/configs/blob/master/README.md) file in the top-level directory of the clone


## Adding a new pipeline-specific config

Sometimes it may be desirable to have configuration options for an institute that are specific to a single nf-core pipeline.
Such options should not be added to the main institutional config, as this will be applied to all pipelines.
Instead, we can create a pipeline-specific institutional config file.

> The following steps are similar to the instructions for standard institutional config, however using `pipeline` variants of folders e.g., `conf/pipeline/` or under `pipeline/`

:warning: Remember to replace the `<PIPELINE>` and `<PROFILE>` placeholders with the pipeline name and profile name in the following examples

Institutional configs work because the pipeline `nextflow.config` file loads the [`nf-core/configs/nfcore_custom.config` config file](https://github.com/nf-core/configs/blob/master/nfcore_custom.config), which in turn loads the institutional configuration file based on the profile `<PROFILE>` supplied on the command line.

To add in pipeline-specific institutional configs, we add a second `includeConfig` call in the pipeline `nextflow.config` file, which loads the `pipeline/<PIPELINE>.config` file from the [`nf-core/configs`](https://github.com/nf-core/configs) repo.
This file has `<PIPELINE>` specific institution configuration again with different profiles `<PROFILE>`.

The pipeline `nextflow.config` file should first load the generic institutional configuration file and then the pipeline-specific institutional configuration file.
Each configuration file will add new params and overwrite the params already existing.

Note that pipeline-specific configs are not required and should only be added if needed.