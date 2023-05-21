
# Revocalize AI – API Documentation 🎙️

![Revocalize AI Voice Models](/images/revocalize-ai-voice-models.png)

Welcome to the Revocalize AI Documentation! This innovative AI voice synthesizer platform utilizes state-of-the-art voice modeling and fingerprinting technology to generate natural-sounding voice models. With millions of hours of audio training data, you can now sing like any singer using AI and instantly record & convert your voice into any other voice. Explore the power of Revocalize AI and join our growing community of developers & enthusiasts.

## 🚀 API Features

The Revocalize AI API offers a variety of features:

- 🌍 Works in any language: Your voice model retains the original accent, tone, and pronunciation, irrespective of the language.
- 🎭 Emotional range: Express true emotions through the voice, from joy and excitement to sadness, and more.
- 🎶 Real-Time Auto Tune: Hits those high notes with ease, thanks to real-time vocal tuning.
- 🔄 Auto-generate variations: Create multiple unique voice variations, each carrying its own unique emotion.
- 🔊 Voice modulation: Adjust pitch, volume, and speed of singing or speech to produce more pleasing results.

## 🔑 Setup Authentication

To use the Revocalize API, you'll first need to generate an API Key through your Revocalize dashboard at `www.revocalize.ai/api-keys`. Tokens must be included in the `Authorization` HTTP header in all requests as a type `Bearer`.

```shell
'Authorization': 'Bearer <revocalize_api_key>'
```

You can test if everything is working correctly using the ping endpoint and curl:

```shell
curl -H "Authentication: Bearer " https://api.revocalize.ai/ping
```

The response will be `{"ping":"pong"}` (if it all goes well) 🏓


## 🛠️ API Endpoints

The API provides multiple endpoints to interact with Revocalize's voice modeling and fingerprinting technology.

### POST Convert Audio File 🔄

This endpoint takes a WAV vocal audio file and returns a URL string with the converted vocals audio file.
```shell
curl --request POST \
      --url https://api.revocalize.ai/convert \
      --header 'Authorization: Bearer <token>' \
      --data '{
      "audio_file": "<audio_file>",
      "model": "<model>" }'
```

The response will be a `task_id` string, which is the ID of the conversion task.

### POST Create Model 📦

This endpoint creates a new AI voice model, which is initially created in a pending state. You must train the model before it can be used for synthesis.

```shell
curl --request POST \
      --url https://api.revocalize.ai/models/create \
      --header 'Authorization: Bearer <token>' \
      --data '{"training_audio_files": "<training_audio_files>"}'
```

You'll get a `model_id` string as a response, which is the ID of the pending model. ⏳


### POST Train Model 🏋️‍♀️


Train a custom AI voice model after creating it in a pending state.


```shell
curl --request POST \
      --url https://api.revocalize.ai/models/{model_id}/train \
      --header 'Authorization: Bearer <token>' \
      --data '{"epochs": 0}'
```

The response will include the status of the training task 🚦, the ID of the model being trained, and the current epoch.

Example Request:

    curl --location --request POST 'https://api.revocalize.ai/models/123456/train' \
    --header 'Content-Type: application/json' \
    --header 'Authorization: Bearer <token>' \
    --form 'epochs=100'

Response:

    {
      "status": "training",
      "model_id": "123456",
      "current_epoch": 50001
    }