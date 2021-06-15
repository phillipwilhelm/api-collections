Symbl's contextual conversation intelligence platform provides scalable, secure speech recognition and contextual analytics to build differentiated experiences from voice, video or text data in realtime. Generate action items, questions, appointments, topic hierarchy, topics, sentiments, action phrases and your custom entities and so much more without any upfront training data. We give you the comprehensive suite of APIs, machine learning infrastructure and customizable experiences to analyze and act on the human conversation data at scale.

# Authentication

Make sure to get your app id and app secret from https://platform.symbl.ai. Use them to generate your auth token which is required to make any API call.

# Async APIs
The Async API provides a REST interface to allow you to run a job asynchronously in order to process insights out of **audio and video files and textual conversations** (Transcripts, Chats, Emails etc.).

# Telephony API

Use the `Start Connection` endpoint to start a connection with Symbl either over a **phone call or conference over PSTN or a SIP** using a Dial-in Phone Number or SIP URI with support for DTMF.

Use the `Stop Connection` endpoint to end the call and close the connection. This will send you an email with all the generated insights from your conversation.


<h2>Postman does not support WebSocket protocol yet, which is why WebSocket based subscription to get real-time results with Telephony API are not included in this collection. <a href="https://docs.symbl.ai/docs/telephony/guides/get-live-transcription">Learn more</a> about getting real-time results using over Telephony sessions.</h2>

# Streaming API

Streaming API is a WebSocket based real-time API by Symbl that provides the direct, fastest and most accurate of all other interfaces to push the audio stream in real-time, and get the results back as soon as they're available.

<h2>Postman does not support WebSocket protocol yet, which is why Streaming API is not included in this collection. <a href="https://docs.symbl.ai/docs/streamingapi/overview/introduction">Learn more</a> about Streaming API.</h2>
