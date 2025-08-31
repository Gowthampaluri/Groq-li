The context manager is required so that the response will reliably be closed.

Making custom/undocumented requests
This library is typed for convenient access to the documented API.

If you need to access undocumented endpoints, params, or response properties, the library can still be used.

Undocumented endpoints
To make requests to undocumented endpoints, you can make requests using client.get, client.post, and other http verbs. Options on the client will be respected (such as retries) when making this request.

import httpx

response = client.post(
    "/foo",
    cast_to=httpx.Response,
    body={"my_param": True},
)

print(response.headers.get("x-foo"))
Undocumented request params
If you want to explicitly send an extra param, you can do so with the extra_query, extra_body, and extra_headers request options.

Undocumented response properties
To access undocumented response properties, you can access the extra fields like response.unknown_prop. You can also get all the extra fields on the Pydantic model as a dict with response.model_extra.

Configuring the HTTP client
You can directly override the httpx client to customize it for your use case, including:

Support for proxies
Custom transports
Additional advanced functionality
import httpx
from groq import Groq, DefaultHttpxClient

client = Groq(
    # Or use the `GROQ_BASE_URL` env var
    base_url="http://my.test.server.example.com:8083",
    http_client=DefaultHttpxClient(
        proxy="http://my.test.proxy.example.com",
        transport=httpx.HTTPTransport(local_address="0.0.0.0"),
    ),
)
You can also customize the client on a per-request basis by using with_options():

client.with_options(http_client=DefaultHttpxClient(...))
Managing HTTP resources
By default the library closes underlying HTTP connections whenever the client is garbage collected. You can manually close the client using the .close() method if desired, or with a context manager that closes when exiting.

from groq import Groq

with Groq() as client:
  # make requests here
  ...

# HTTP client is now closed
Versioning
This package generally follows SemVer conventions, though certain backwards-incompatible changes may be released as minor versions:

Changes that only affect static types, without breaking runtime behavior.
Changes to library internals which are technically public but not intended or documented for external use. (Please open a GitHub issue to let us know if you are relying on such internals.)
Changes that we do not expect to impact the vast majority of users in practice.
We take backwards-compatibility seriously and work hard to ensure you can rely on a smooth upgrade experience.

We are keen for your feedback; please open an issue with questions, bugs, or suggestions.

Determining the installed version
If you've upgraded to the latest version but aren't seeing any new features you were expecting then your python environment is likely still using an older version.

You can determine the version that is being used at runtime with:

import groq
print(groq.__version__)
Requirements
Python 3.8 or higher.

Contributing
See the contributing documentation.
