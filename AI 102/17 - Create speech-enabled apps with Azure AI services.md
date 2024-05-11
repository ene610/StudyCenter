# Introduction

Azure AI Speech provides APIs that you can use to build speech-enabled applications. This includes:

- **Speech to text**: An API that enables _speech recognition_ in which your application can accept spoken input.
- **Text to speech**: An API that enables _speech synthesis_ in which your application can provide spoken output.
- **Speech Translation**: An API that you can use to translate spoken input into multiple languages.
- **Speaker Recognition**: An API that enables your application to recognize individual speakers based on their voice.
- **Intent Recognition**: An API that uses conversational language understanding to determine the semantic meaning of spoken input.

This module focuses on speech recognition and speech synthesis, which are core capabilities of any speech-enabled application.

In this module, you'll learn how to:

- Provision an Azure resource for the Azure AI Speech service
- Use the Speech to text API to implement speech recognition
- Use the Text to speech API to implement speech synthesis
- Configure audio format and voices
- Use Speech Synthesis Markup Language (SSML)

The units in the module include important conceptual information about Azure AI Speech and how to use its API through one of the supported software development kits (SDKs), after which you'll be able to try Azure AI Speech for yourself in a hands-on exercise. To complete the hands-on exercise, you will need a Microsoft Azure subscription. If you don't already have one, you can sign up for a free trial at [https://azure.com/free](https://azure.com/free).

---
# Provision an Azure resource for speech

Completed 100 XP

- 2 minutes

Before you can use Azure AI Speech, you need to create an Azure AI Speech resource in your Azure subscription. You can use either a dedicated Azure AI Speech resource or a multi-service Azure AI Services resource.

After you create your resource, you'll need the following information to use it from a client application through one of the supported SDKs:

- The _location_ in which the resource is deployed (for example, _eastus_)
- One of the _keys_ assigned to your resource.

You can view of these values on the **Keys and Endpoint** page for your resource in the Azure portal.
# Use the Azure AI Speech to Text API

Completed 100 XP

- 5 minutes

The Azure AI Speech service supports speech recognition through two REST APIs:

- The **Speech to text** API, which is the primary way to perform speech recognition.
- The **Speech to text Short Audio** API, which is optimized for short streams of audio (up to 60 seconds).

You can use either API for interactive speech recognition, depending on the expected length of the spoken input. You can also use the **Speech to text** API for _batch transcription_, transcribing multiple audio files to text as a batch operation.

You can learn more about the REST APIs in the [Speech to text REST API documentation](https://learn.microsoft.com/en-us/azure/ai-services/speech-service/rest-speech-to-text). In practice, most interactive speech-enabled applications use the Speech service through a (programming) language-specific SDK.

## Using the Azure AI Speech SDK

While the specific details vary, depending on the SDK being used (Python, C#, and so on); there's a consistent pattern for using the **Speech to text** API:

![A diagram showing how a SpeechRecognizer object is created from a SpeechConfig and AudioConfig, and its RecognizeOnceAsync method is used to call the Speech API.](https://learn.microsoft.com/en-gb/training/wwl-data-ai/create-speech-enabled-apps/media/speech-to-text.png)

1. Use a **SpeechConfig** object to encapsulate the information required to connect to your Azure AI Speech resource. Specifically, its **location** and **key**.
2. Optionally, use an **AudioConfig** to define the input source for the audio to be transcribed. By default, this is the default system microphone, but you can also specify an audio file.
3. Use the **SpeechConfig** and **AudioConfig** to create a **SpeechRecognizer** object. This object is a proxy client for the **Speech to text** API.
4. Use the methods of the **SpeechRecognizer** object to call the underlying API functions. For example, the **RecognizeOnceAsync()** method uses the Azure AI Speech service to asynchronously transcribe a single spoken utterance.
5. Process the response from the Azure AI Speech service. In the case of the **RecognizeOnceAsync()** method, the result is a **SpeechRecognitionResult** object that includes the following properties:
    - Duration
    - OffsetInTicks
    - Properties
    - Reason
    - ResultId
    - Text

If the operation was successful, the **Reason** property has the enumerated value **RecognizedSpeech**, and the **Text** property contains the transcription. Other possible values for **Result** include **NoMatch** (indicating that the audio was successfully parsed but no speech was recognized) or **Canceled**, indicating that an error occurred (in which case, you can check the **Properties** collection for the **CancellationReason** property to determine what went wrong).
# Use the text to speech API

Completed 100 XP

- 4 minutes

Similarly to its **Speech to text** APIs, the Azure AI Speech service offers other REST APIs for speech synthesis:

- The **Text to speech** API, which is the primary way to perform speech synthesis.
- The **Batch synthesis** API, which is designed to support batch operations that convert large volumes of text to audio - for example to generate an audio-book from the source text.

You can learn more about the REST APIs in the [Text to speech REST API documentation](https://learn.microsoft.com/en-us/azure/ai-services/speech-service/batch-synthesis). In practice, most interactive speech-enabled applications use the Azure AI Speech service through a (programming) language-specific SDK.

## Using the Azure AI Speech SDK

As with speech recognition, in practice most interactive speech-enabled applications are built using the Azure AI Speech SDK.

The pattern for implementing speech synthesis is similar to that of speech recognition:

![A diagram showing how a SpeechSynthesizer object is created from a SpeechConfig and AudioConfig, and its SpeakTextAsync method is used to call the Speech API.](https://learn.microsoft.com/en-gb/training/wwl-data-ai/create-speech-enabled-apps/media/text-to-speech.png)

1. Use a **SpeechConfig** object to encapsulate the information required to connect to your Azure AI Speech resource. Specifically, its **location** and **key**.
2. Optionally, use an **AudioConfig** to define the output device for the speech to be synthesized. By default, this is the default system speaker, but you can also specify an audio file, or by explicitly setting this value to a null value, you can process the audio stream object that is returned directly.
3. Use the **SpeechConfig** and **AudioConfig** to create a **SpeechSynthesizer** object. This object is a proxy client for the **Text to speech** API.
4. Use the methods of the **SpeechSynthesizer** object to call the underlying API functions. For example, the **SpeakTextAsync()** method uses the Azure AI Speech service to convert text to spoken audio.
5. Process the response from the Azure AI Speech service. In the case of the **SpeakTextAsync** method, the result is a **SpeechSynthesisResult** object that contains the following properties:
    - AudioData
    - Properties
    - Reason
    - ResultId

When speech has been successfully synthesized, the **Reason** property is set to the **SynthesizingAudioCompleted** enumeration and the **AudioData** property contains the audio stream (which, depending on the **AudioConfig** may have been automatically sent to a speaker or file).
# Configure audio format and voices

Completed 100 XP

- 3 minutes

When synthesizing speech, you can use a **SpeechConfig** object to customize the audio that is returned by the Azure AI Speech service.

## Audio format

The Azure AI Speech service supports multiple output formats for the audio stream that is generated by speech synthesis. Depending on your specific needs, you can choose a format based on the required:

- Audio file type
- Sample-rate
- Bit-depth

The supported formats are indicated in the SDK using the **SpeechSynthesisOutputFormat** enumeration. For example, `SpeechSynthesisOutputFormat.Riff24Khz16BitMonoPcm`.

To specify the required output format, use the **SetSpeechSynthesisOutputFormat** method of the **SpeechConfig** object:

C#

```
speechConfig.SetSpeechSynthesisOutputFormat(SpeechSynthesisOutputFormat.Riff24Khz16BitMonoPcm);
```

For a full list of supported formats and their enumeration values, see the [Azure AI Speech SDK documentation](https://learn.microsoft.com/en-us/dotnet/api/microsoft.cognitiveservices.speech.speechsynthesisoutputformat).

## Voices

The Azure AI Speech service provides multiple voices that you can use to personalize your speech-enabled applications. There are two kinds of voice that you can use:

- _Standard voices_ - synthetic voices created from audio samples.
- _Neural voices_ - more natural sounding voices created using deep neural networks.

Voices are identified by names that indicate a locale and a person's name - for example `en-GB-George`.

To specify a voice for speech synthesis in the **SpeechConfig**, set its **SpeechSynthesisVoiceName** property to the voice you want to use:

C#

```
speechConfig.SpeechSynthesisVoiceName = "en-GB-George";
```

For information about voices, see the [Azure AI Speech SDK documentation](https://learn.microsoft.com/en-us/azure/ai-services/speech-service/language-support?tabs=tts).
# Use Speech Synthesis Markup Language

Completed 100 XP

- 3 minutes

While the Azure AI Speech SDK enables you to submit plain text to be synthesized into speech (for example, by using the **SpeakTextAsync()** method), the service also supports an XML-based syntax for describing characteristics of the speech you want to generate. This **Speech Synthesis Markup Language** (SSML) syntax offers greater control over how the spoken output sounds, enabling you to:

- Specify a speaking style, such as "excited" or "cheerful" when using a neural voice.
- Insert pauses or silence.
- Specify _phonemes_ (phonetic pronunciations), for example to pronounce the text "SQL" as "sequel".
- Adjust the _prosody_ of the voice (affecting the pitch, timbre, and speaking rate).
- Use common "say-as" rules, for example to specify that a given string should be expressed as a date, time, telephone number, or other form.
- Insert recorded speech or audio, for example to include a standard recorded message or simulate background noise.

For example, consider the following SSML:

XML

```
<speak version="1.0" xmlns="http://www.w3.org/2001/10/synthesis" 
                     xmlns:mstts="https://www.w3.org/2001/mstts" xml:lang="en-US"> 
    <voice name="en-US-AriaNeural"> 
        <mstts:express-as style="cheerful"> 
          I say tomato 
        </mstts:express-as> 
    </voice> 
    <voice name="en-US-GuyNeural"> 
        I say <phoneme alphabet="sapi" ph="t ao m ae t ow"> tomato </phoneme>. 
        <break strength="weak"/>Lets call the whole thing off! 
    </voice> 
</speak>
```

This SSML specifies a spoken dialog between two different neural voices, like this:

- **Ariana** (_cheerfully_): "I say tomato:
- **Guy**: "I say tomato (pronounced _tom-ah-toe_) ... Let's call the whole thing off!"

To submit an SSML description to the Speech service, you can use the **SpeakSsmlAsync()** method, like this:

C#

```
speechSynthesizer.SpeakSsmlAsync(ssml_string);
```

For more information about SSML, see the [Azure AI Speech SDK documentation](https://learn.microsoft.com/en-us/azure/ai-services/speech-service/speech-synthesis-markup).