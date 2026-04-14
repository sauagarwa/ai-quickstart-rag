# AI Quickstart Rag

This pattern encapsulates the [RAG AI Quickstart](https://github.com/rh-ai-quickstart/RAG).

## Installing this pattern (as-is)

* Log into an OpenShift 4.18+ cluster
* Copy [`values-secret.yaml.template`](./values-secret.yaml.template) to `~/values-secret-ai-quickstart-rag.yaml`

  ```bash
  cp values-secret.yaml.template ~/values-secret-ai-quickstart-rag.yaml
  ```

  Update the `hf_token` secret under `llm-service` with an api key that has access to the models used.
  For the default installation, see [Requesting model access](#requesting-model-access) below.
* Run `./pattern.sh make install`

## Requesting model access

By default, this model will require access to [meta-llama/Llama-3.2-3B-Instruct](https://huggingface.co/meta-llama/Llama-3.2-3B-Instruct).
Request access on Hugging Face before installing the pattern with the account that the token in
`~/values-secret-ai-quickstart-rag.yaml` is associated with.

If you update the default models, make sure to accept whatever terms and conditions are necessary for the models
you configured.

## Customizing this pattern

1. Fork [this repo](https://github.com/validatedpatterns-sandbox/ai-quickstart-rag)
2. Clone your fork (with SSH)
   ```bash
   git clone git@github.com:<my_github_user>/ai-quickstart-rag.git
   ```
   or (with HTTPS)

   ```bash
   git clone https://github.com/<my_github_user>/ai-quickstart-rag.git
   ```

   Then,

   ```bash
   cd ai-quickstart-rag
   ```
3. Create a branch for your changes
   ```bash
   git checkout -b my-changes
   ```
4. Make your chages to the repo. For instance, you could [use this pattern with a GPU](#using-this-pattern-with-an-nvidia-gpu).
5. Push up your changes. This is necessary since Validated Patterns are GitOps-driven and ArgoCD needs to be able to
   pull your pattern down from GitHub.
6. At this point, the instructions are pretty much the same as in [Installing this pattern (as-it)](#installing-this-pattern-as-is).
   Log into your cluster, copy and update the secrets with your Hugging Face token, run `./pattern.sh make install`.

## Using this pattern with an Nvidia GPU

Without any changes, this pattern will use a CPU backed LLM and have no need for a GPU. This can be limiting
in terms of usable models as well as speed, so you may wish to use a GPU instead. To enable this, follow along
with the instructions in [Customizing this pattern](#customizing-this-pattern). Once you've made a branch for your
changes, you merely need to update `global.device` to be `gpu` and push your changes to GitHub. This will
add NFD and Nvidia GPU operators to the pattern installation and enable the models to run using an Nvidia accelerator.

**Note**: If you are running this pattern on an OpenShift cluster on AWS, setting `global.device` to `gpu` will
automatically create a GPU (`g6.2xlarge`) machine for you and add it as a worker node to your cluster.
