# elg_bertimbau
elg_bertimbau is a tool that predicts which word fits in a masked space on a text using the maskes language model for portuguese language BERTIMBAU.
This repository contains a dockerized API built over BERTIMBAU for integrate it into the ELG. Its original code can
be found [here](https://github.com/neuralmind-ai/portuguese-bert).

## Install

```
sh docker-build.sh
```

## Execute
```
docker run --rm -p 0.0.0.0:8866:8866 --name bertimbau elg_bertimbau:1.0.1
```
## Use

```
curl -X POST  http://0.0.0.0:8866/predict_json -H 'Content-Type: application/json' -d '{"type": "text", "content":"As filhas do primeiro ministro de [MASK] visitaron o palaço do presidente."}'
```


# Test
In the folder `test` you have the files for testing the API according to the ELG specifications.
It uses an API that acts as a proxy with your dockerized API that checks both the requests and the responses.
For this follow the instructions:
1) Configure the .env file with the data of the image and your API
2) Launch the test: `docker-compose up`
3) Make the requests, instead of to your API's endpoint, to the test's endpoint:
   ```
   curl -X POST  http://0.0.0.0:8866/processText/service -H 'Content-Type: application/json' -d '{"type": "text", "content":"As filhas do primeiro ministro de [MASK] visitaron o palaço do presidente."}'
   ```
4) If your request and the API's response is compliance with the ELG API, you will receive the response.
   1) If the request is incorrect: Probably you will don't have a response and the test tool will not show any message in logs.
   2) If the response is incorrect: You will see in the logs that the request is proxied to your API, that it answers, but the test tool does not accept that response. You must analyze the logs.


## Citations
The original work of this tool is:
- Souza, F., Nogueira, R., & Lotufo, R. (2020, October). BERTimbau: pretrained BERT models for Brazilian Portuguese. In Brazilian Conference on Intelligent Systems (pp. 403-417). Springer, Cham.
- Souza, F., Nogueira, R., & Lotufo, R. (2019). Portuguese named entity recognition using BERT-CRF. arXiv preprint arXiv:1909.10649.
- https://github.com/neuralmind-ai/portuguese-bert

The license of the original work is MIT License.
