# AIMV
AI model that generates a Music Video from a .wav file, using Instrument Classification, Speech Transcription, and Video Generation. 
## *Architecture*:
### Content Transcription
  - #### **Instrument Classification**
    - [Musical Instrument Identification](https://www.mdpi.com/1424-8220/22/8/3033/pdf?version=1650009477)
    
    - [Drum Sound Subtype Classification](https://www.researchgate.net/publication/41538774_Classification_of_snare_drum_sounds_using_neural_networks)
    
    - [Timbre Identification](https://iopscience.iop.org/article/10.1088/1742-6596/1856/1/012006/pdf)
    
    - [Sound Event Detection](https://arxiv.org/pdf/2107.05463)
    
  - #### Speech Recognition (is speech present?) and subsequent Speech Transcription (if present) using OpenAI Whisper ASR. use --language Spanish if Spanish, etc
    [Whisper](https://github.com/openai/whisper) uses Transformer Neural Networks
    
  - #### Concatenation of the above into a general content transcription
    For an audio window of length 1 second containing a Vocal saying "Heart" over a soft drum crash hit:
      - Return (loud, heart, crash, splash, drum, hexcolorvalue)
 
    This translates to:
      -   Volume relative to the running average volume + Vocal transcription + 3 most relevant instrument identifications + color (from frequency)
  
    We then port this list to a sentence. 
      -   Volume informs the intensity of the image, ie if loud/quiet vocal saying Heart, say "person screaming/yelling/whispering, action + object
        - Action being looking at, running at, holding, etc, the object in question ("heart"). Choose action randomly. 
        - Further abstract the crash, splash, drum (transient description) by mapping these to additional words, 
          - crash -> impact, splash -> wave, drum (being the most general category, can be ignored). (impact, wave)
            - Category (drum, guitar, vocal) determines the verb (hits, plays, sings)
          - (kick, bass, drum) -> (canon, deep)
          - (note, string, guitar) -> (floating, vibrate)
          - add these abstracted words to the final text description
    Examples:
      - (loud, heart, crash, splash, drum, hexcolorvalue, impact, wave) -> "Person loudly sings 'heart' over a soft drum crash hit that feels like a wave impact, the scene has a (hexcolorvalue) color palette 
      - (loud, N/A, kick, bass, drum, hexcolorvalue, canon, deep) -> "Kick drum loud hit that feels like a deep canon, the scene has a (hexcolorvalue) color palette
      - (quiet, N/A, note, string, guitar, hexcolorvalue, floating, vibrate) -> "Guitar quietly plays a note that feels like a vibrate floating, the scene has a (hexcolorvalue) color palette.  

### **Video Generation**
  - [CogVideo](https://github.com/THUDM/CogVideo) uses Transformer Neural Networks
  - [CogVideoPaper](https://github.com/THUDM/CogVideo)
