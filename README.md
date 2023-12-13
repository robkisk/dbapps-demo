# dbtunnel 

Proxy solution to run elegant Web UIs natively inside databricks notebooks.

**YOU CAN ONLY USE THIS IN DATABRICKS NOTEBOOKS WITH A RUNNING CLUSTER**

**FOR SECURE ACCESS PLEASE USE A SINGLE USER CLUSTER (ANYONE WITH ATTACH CAN ACCESS THE UIs)** 

## Description

Easy way to test the following things on a databricks cluster and notebooks

### Framework Support

* [x] fastapi: [fastapi.py](examples%2Ffastapi%2Ffastapi.py)
* [x] gradio: [gradio-demo.py](examples%2Fgradio%2Fgradio-demo.py)
* [x] stable diffusion webui: [stable-diffusion-example.py](examples%2Fstable-diffusion-webui%2Fstable-diffusion-example.py)
* [x] streamlit: [streamlit_example.py](examples%2Fstreamlit%2Fstreamlit_example.py)
* [x] nicegui: [nicegui-example.py](examples%2Fnicegui%2Fnicegui-example.py)
* [x] flask: [flask-app.py](examples%2Fflask%2Fflask-app.py)
* [x] dash: [dask-example.py](examples%2Fdash%2Fdask-example.py)
* [x] bokeh: [bokeh-example.py](examples%2Fbokeh%2Fbokeh-example.py)
* [ ] posit
* [ ] panel
* [x] solara: [solara-example.py](examples%2Fsolara%2Fsolara-example.py)
* [x] chainlit: [chainlit.py](examples%2Fchainlit%2Fchainlit.py)
* [x] code-server on repos [code-server-example.py](examples%2Fcode-server%2Fcode-server-example.py)

Easy way to test out llm chatbots; look in examples/gradio

### Chatbot Support

**You must use A10 GPU instances or higher**

* [x] Mistral-7b [gradio-chat-mistral7b-demo.py](examples%2Fgradio%2Fgradio-chat-mistral7b-demo.py)
* [ ] Llama-2-7b
* [ ] mpt-7b
* [ ] Streaming support (vllm, etc.)
* [x] Typewriter effect

### Tunnel Support:

* [x] ngrok
* [ ] devtunnels
* [ ] cloudflared



## Setup

**Please do not use this in production!!**

1. Clone this repo into databricks repos
2. Go to any of the examples to see how to use them
3. Enjoy your proxy experience :-) 
4. If you want to share the link ensure that the other user has permission to attach to your cluster.

## Exposing to internet using ngrok

**WARNING: IT WILL BE PUBLICLY AVAILABLE TO ANYONE WITH THE LINK SO DO NOT EXPOSE ANYTHING SENSITIVE**

The reason for doing this is to test something with a friend or colleague who is not logged in into databricks.
The proxy option requires you to be logged in into databricks.

1. Go to [ngrok](https://ngrok.com/) and create an account and get an api token and a tunnel auth token
    * You can get a tunnel token from [here](https://dashboard.ngrok.com/get-started/your-authtoken).
    * You can get an api token from [here](https://dashboard.ngrok.com/api).
2. Go to a databricks notebook:
3. **If you are using free tier of ngrok you can only have one tunnel and one session at a time so enable `kill_all_tunnel_sessions=True`** 

Take a look at the full example here [streamlit-example-ngrok.py](examples%2Fstreamlit%2Fstreamlit-example-ngrok.py)

```python
from dbtunnel import dbtunnel

# again this example is with streamlit but works with any framework
dbtunnel.streamlit("<script_path>").share_to_internet_via_ngrok(
    ngrok_api_token="<ngrok api token>",
    ngrok_tunnel_auth_token="<ngrok tunnel auth token>"
).run()

# if you need to kill tunnels because you are on free tier:
# again this example is with streamlit but works with any framework
dbtunnel.streamlit("<script_path>").share_to_internet_via_ngrok(
    ngrok_api_token="<ngrok api token>",
    ngrok_tunnel_auth_token="<ngrok tunnel auth token>",
    kill_all_tunnel_sessions=True,
).run()
```


## Disclaimer
dbtunnel is not developed, endorsed not supported by Databricks. It is provided as-is; no warranty is derived from using this package. For more details, please refer to the license.