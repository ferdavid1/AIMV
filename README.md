# AIMV
AI model that generates a Music Video from a .wav file, using Instrument Classification, Speech Transcription, and Video Generation. 
## *Architecture*:
Content Transcription Model 
  -Instrument Classification
    [Musical Instrument Identification:](https://www.mdpi.com/1424-8220/22/8/3033/pdf?version=1650009477)
    [Drum Sound Subtype Classification:](https://www.researchgate.net/publication/41538774_Classification_of_snare_drum_sounds_using_neural_networks)
    [Timbre Identification:](https://iopscience.iop.org/article/10.1088/1742-6596/1856/1/012006/pdf)
    [Sound Event Detection:](https://arxiv.org/pdf/2107.05463)
    
  -Speech Recognition and subsequent Transcription using OpenAI Whisper ASR. use --language Spanish if Spanish, etc
    [Whisper](https://github.com/openai/whisper) uses Transformer Neural Networks
    
  -Concatenation of the above into a general content transcription
    For an audio window of length 1 second containing a Vocal saying "Heart" over a soft drum crash hit:
      return (heart, crash, splash, drum, soft, hexcolorvalue)
      vocal transcription + 3 most relevant instrument identifications + valence of the action (from timbre) + color (from frequency)
  -Video Generation
    [CogVideo](https://github.com/THUDM/CogVideo) uses Transformer Neural Networks
    [CogVideoPaper](https://github.com/THUDM/CogVideo)
