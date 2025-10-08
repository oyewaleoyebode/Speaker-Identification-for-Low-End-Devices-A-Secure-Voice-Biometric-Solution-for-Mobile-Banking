# Speaker-Identification-for-Low-End-Devices-A-Secure-Voice-Biometric-Solution-for-Mobile-Banking

# Abstract 
The rise of the mobile era, especially with the availability of the internet, has significantly contributed to the growth of mobile banking, enhancing financial inclusion, particularly among underserved populations. However, reliance on basic mobile devices without advanced biometric security features exposes users to risks of financial fraud, unauthorized account access, and identity theft. This study introduces a lightweight speaker identification system tailored to improve the security of mobile banking in low-resource environments. By utilizing voice biometric authentication, the system confirms the user’s identity through their voice at the end of each transaction, ensuring that only the authorized user can complete the transaction even if their Personal Identification Number (PIN) is compromised. The system combines advanced deep learning models, such as Whisper-large-v3 and Emphasized Channel Attention, Propagation, and Aggregation in Time Delay Neural Network (ECAPA-TDNN), to extract detailed voice features, including linguistic patterns and unique speaker traits, ensuring high accuracy and reliability in real-time identification. Additionally, liveness detection is integrated to defend against advanced spoofing, further enhancing system security. Evaluations on real-world data demonstrate the system’s robust performance, achieving 99.59\% accuracy, 99.62\% precision, and an Equal Error Rate (EER) of 0.0017, validating the system’s practicality in constrained environments without requiring extensive computational resources. This solution provides a scalable and secure voice authentication method that is particularly beneficial for underserved communities, advancing both mobile banking security and financial inclusion.

# Introduction 
The rapid growth of mobile banking has improved financial inclusion, particularly in developing regions, by enabling digital transactions through affordable mobile devices. However, users of low-end phones that rely solely on Personal Identification Numbers (PINs) for authentication face serious security risks such as fraud, identity theft, and unauthorized access. These vulnerabilities are worsened by user behaviors like storing or sharing PINs and by SIM-based transaction exploits that allow attackers to access sensitive financial data.

<p align="center">
<img width="1611" height="1196" alt="problem" src="https://github.com/user-attachments/assets/e8668c4d-f881-4722-b201-c09c9a184e03" />
</p>

Voice biometric authentication offers a practical security solution because it relies on vocal characteristics such as pitch, tone, and speech pattern to verify identity using only a microphone. This makes it suitable for low-end devices that lack fingerprint or facial recognition features. Integrating voice verification after PIN entry ensures that even if a PIN is stolen, only the genuine account holder can authorize a transaction. This approach enhances both security and accessibility for underserved communities.

Nonetheless, implementing voice biometrics on resource-limited devices presents challenges, including restricted processing power, noise interference, and vulnerability to spoofing attacks. While existing speech technologies perform well on high-end devices, they are often too computationally heavy for basic phones. To address this, the paper proposes a lightweight speaker identification (SI) system optimized for mobile banking on low-end hardware. The system performs real-time user verification before authorizing transactions, providing an extra layer of protection against PIN theft, remote fraud, and social engineering attacks.

The research focuses on developing a resource-efficient, high-accuracy SI model capable of running in real-time while integrating liveness detection to counter spoofed voices. The contribution lies in designing and validating a secure, practical, and computationally optimized speaker identification system suitable for deployment in low-resource mobile banking environments, thereby reinforcing trust and security among financially underserved populations.

<p align="center">
  <img width="2231" height="939" alt="Bank" src="https://github.com/user-attachments/assets/7a92decb-e8d0-462d-a812-82111db1d17a" />
</p>

# Methodology

The proposed Speaker Identification (SI) system is developed for mobile banking on low-end devices, emphasizing real-time performance, resource efficiency, and high security. It combines Whisper and ECAPA-TDNN architectures to extract phonetic, prosodic, and identity-specific voice features, forming embeddings verified using cosine similarity and angular distance metrics. Evaluation criteria include accuracy, F1-score, precision, recall, and Equal Error Rate (EER).

# Dataset Development and Spoofed Data Creation

A custom dataset was created using recordings from 50 NAIST students (20 female, 30 male) representing diverse linguistic backgrounds (Bahasa, Bengali, Chinese, French, Indonesian, etc.). Each participant recorded 50 phrases under both indoor and outdoor conditions using various devices, including GRATINA 4G, Samsung A04s, iPhone SE, and MacBook microphones, sampled at 8–16 kHz to simulate real-world device variability.
A spoofed dataset was generated to evaluate robustness against attacks. Using PlayHT API (for voice synthesis), adversarial perturbations (ε = 0.001–0.005), and WORLD vocoder transformations, 1,500 spoofed samples were created (30 per speaker). These attacks simulated deepfakes and manipulations through pitch, spectral, and temporal modifications, challenging the model’s ability to distinguish authentic from synthetic voices.

# Audio Processing and Conversion

All recordings underwent normalization, resampling (16 kHz), noise suppression, silence trimming, and dynamic range compression to improve consistency. Audio files were segmented into 3–5-second clips for efficient embedding extraction and balanced processing across devices.

# Threat Model and Security Design

Attackers were classified into external, internal, and technically skilled types. The study addressed voice cloning, replay, and adversarial perturbation attacks, each of which is capable of bypassing naive voice verification systems.
To mitigate these threats, the SI system incorporates liveness detection, cross-validation-based generalization, and threshold tuning to minimize false acceptances while ensuring usability under noisy and constrained conditions.

<p align="center">
  <img width="1511" height="803" alt="Impersonator" src="https://github.com/user-attachments/assets/79dc3e64-8d2a-46a7-bda8-9640c22df261" />
</p>

# Speaker Identification and Verification Pipeline

The pipeline includes:

- Feature Extraction using Whisper (phonetic/prosodic) and ECAPA-TDNN (speaker traits).

- Diarization and Segmentation with PyAnnote to isolate individual voices.

- Fusion of Whisper and ECAPA-TDNN embeddings using PCA to reduce dimensionality and enhance robustness.

- Storage & Matching, where embeddings are saved per speaker and compared via cosine similarity to authenticate users.

<p align="center">
  <img width="1550" height="534" alt="Enrollment" src="https://github.com/user-attachments/assets/e14805aa-7073-43fb-83bb-431007553740" />
</p>

# Model Training

Fused embeddings were normalized and trained using a neural network classifier with ReLU activations and Adam optimizer. After 100 epochs, the model achieved 99.59% training accuracy and 99.45% validation accuracy, showing effective learning and generalization. Loss reduced from 0.1654 to 0.0412, validating the embedding fusion strategy.

# System Workflow and Operation

The system operates remotely to support low-end devices.

- Enrollment Phase: Users record multiple voice samples that undergo preprocessing and embedding extraction. These embeddings are stored in a secured database for later verification.

- Verification Phase: New voice samples are preprocessed and compared with stored embeddings. Authentication succeeds if the similarity exceeds a threshold, allowing the transaction to be completed.

# Spoofing Countermeasures and Liveness Detection

A Random Forest classifier was trained on live and spoofed embeddings (5,200 training, 1,300 testing samples) to detect fraudulent voices. It achieved 100% cross-validation accuracy, with a mean Pearson correlation (0.955) and cosine similarity (0.950) between live and spoofed embeddings, confirming the difficulty of the task yet the model’s robustness.
The integrated liveness detection mechanism filters out spoofed inputs before verification. Processing time averaged 25 ms per file, confirming real-time performance.

<p align="center">
  <img width="3633" height="1170" alt="Liveness Detection" src="https://github.com/user-attachments/assets/bc81241f-2932-4e1f-9490-a98fa5fa8b9c" />
</p>

# Outcome

The system demonstrates strong anti-spoofing performance, low computational cost, and high verification accuracy, proving its practicality for enhancing mobile banking security on low-end devices through lightweight, secure, and adaptive speaker identification.

# Results
The proposed Speaker Identification (SI) system achieved exceptional performance across multiple metrics. Training over 100 epochs showed stable convergence, with loss reducing from 0.1654 to 0.0412, confirming strong generalization. The system recorded 99.59% accuracy, 99.62% precision, 99.59% recall, and an F1-score of 99.60%, indicating a well-balanced capability to distinguish between speakers with minimal errors.

Similarity metrics validated this precision: cosine similarity values for genuine users exceeded 0.80, whereas impostors averaged around 0.35. Angular distance analysis supported these findings, with authentic matches showing minimal distances (≈ 0.65 radians). Together, these metrics demonstrated high discrimination power and consistency across varied inputs.

The Equal Error Rate (EER) averaged 0.0017, with individual class values between 0.0020–0.0027, confirming minimal trade-off between false acceptance and false rejection. The ROC curve nearly touched the upper-left corner, producing an AUC close to 1, illustrating near-perfect classification performance and high sensitivity to speaker identity distinctions.

# Conclusion

This study presented a lightweight speaker identification (SI) system designed to improve mobile banking security on low-end devices using voice biometrics. By combining Whisper and ECAPA-TDNN models, the system accurately captures vocal traits, achieving a high identification accuracy of 99.59\% and a low Equal Error Rate (EER) of 0.0017. These results demonstrate its ability to secure transactions even when a PIN is compromised, addressing key vulnerabilities in PIN-only authentication methods commonly used in underserved regions. The integration of liveness detection further reinforces the system’s defenses against spoofing, offering a scalable and resource-efficient solution that supports financial inclusion.

While the system shows strong performance in controlled evaluations, further testing is required in real-world banking environments, where device diversity and background noise may affect results. Future work will prioritize robustness against advanced threats such as voice cloning and adversarial inputs, as well as adaptability across languages and dialects. Additionally, dynamic similarity thresholds could be explored to better manage verification drift and failure cases under varying conditions.

This study also acknowledges the challenge of temporal variability changes in voice due to aging, illness, or environmental influences, which may impact long-term accuracy. Investigating adaptive thresholding strategies or incremental model updates based on longitudinal voice data could enhance system reliability over time, ensuring consistent performance in evolving deployment scenarios.

# Citation
If you wish to cite this work:

```bibtex

@INPROCEEDINGS{11173011,
  author       = {Oyebode Oluwatobi Oyewale and Yuzo Taenaka and Youki Kadobayashi},
  title        = {Speaker Identification for Low-End Devices: A Secure Voice Biometric Solution for Mobile Banking},
  booktitle    = {2025 11th IEEE International Conference on Privacy Computing and Data Security (PCDS)},
  year         = {2025},
  pages        = {80--87},
  keywords     = {Performance evaluation; Accuracy; Error analysis; Biological system modeling; Authentication; Banking; Feature extraction; Biometric authentication; PINs; Object recognition; Voice Biometric Authentication; Speaker Identification; Liveness Detection; Anti-Spoofing; Resource-Constrained Devices},
  doi          = {10.1109/PCDS65695.2025.00020}
}

