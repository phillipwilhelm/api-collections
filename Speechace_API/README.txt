![Speechace Developer API Documentation](https://s3-us-west-2.amazonaws.com/speechace-public/images/Speechace-API-Card.png)

[Speechace](https://www.speechace.com) is a Speech Recognition API for fluency and pronunciation assessment. Our patented technology is unique in its ability to score a learner's speech and pinpoint individual syllable and phoneme level mistakes in a user's pronunciation in real time.

---
# NEW! Spontaneous Speech Assessment
Speechace API now supports transcription and assessment of spontaneous speech on: Pronunciation, Fluency, Vocabulary. This enables the creation of free speaking activities where a general response can be illicited from the speaker.

 See [Transcribe & Score API](https://docs.speechace.com/#b81a186a-b26e-4378-9967-388aa68985b1) for details.

----
# API Use Cases
The Speechace API can be used to assess and score a variety of speaking activities:

1. Word and Sentence level pronunciation assessment
2. Passage level Fluency assessment
3. Estimating IELTS Speaking score and PTE Speaking score
4. Speaking activities (e.g. Flashcards, fill in the blank, multiple choice)
5. Transcribing and evaluating spontaneous (free speaking) responses to a prompt
6. Evaluating the Vocabulary level of a given text or response.

The Speechace API returns an overall score in each evaluated utterance and detailed sub-scores providing feedback on mistakes at sentence, word, syllable, and phoneme level.

# Requirements
To use this collection you need to add the following to the API calls:
* Speechace API key
* Audio files for each call.

# API Keys
You can obtain a Speechace key [here](https://www.speechace.com/#api).

Your API key is a secret and should only be used from the secure backend of your application. You should not share your key, or use it from your front-end.

# Terms of Service
By using the Speechace API you agree to the [Privacy Policy](https://www.speechace.com/privacy-policy/) and the [Terms of Service](https://www.speechace.com/terms-of-service/).

Speechace API is the Copyright © Speechace LLC, Seattle, WA, USA.

# Recording Audio
You can record and resample audio using the [SoX utility](http://sox.sourceforge.net). Links to sample audio files are also provided in each example below.

The user_audio_file can be wav, mp3, m4a, ogg, webm, aiff. We strongly recommend recording at the following settings to optimize your file size and increase performance:

* *sample size*: 16-bit
* *sample rate*: 16Khz
* *channels*: 1 (i.e. mono)

# API Limits

The Speechace API has the following limits per the API SKU license: Basic, Pro, or Premium.

| Limit | API SKU (BASIC) | API SKU (PRO) | API SKU (PREMIUM) |
|:-----:|:---------------:|:-------------:|:-----------------:|
|Max Audio Length| 15 seconds | 45 seconds | Custom |
|Max File Size| 1.9MB | 2.5MB | Custom |
|Max text Size| 1500 chars | 1500 chars | Custom |



# Samples
You can download samples showing both:
* frontend (recording audio, passing to backend, showing scores)
* backend (calling speechace API, passing scores to frontend)

The samples are available on github [here](https://github.com/speechace/speechace-api-samples)
