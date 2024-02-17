# **Project Introduction Telco Customer Churn**

## Business Problem Understanding
**Context**

Industri Telekomunikasi mengalami pertumbuhan yang pesat, persaingan antar penyedia jasa layanan Telekomunikasi juga semakin meningkat. Tantangan utama yang dihadapi saat ini oleh para penyedia jasa Telekomunikasi adalah mempertahankan pelanggan yang saat ini mereka miliki dan mencegah beralihnya pelanggan ke pesaing.

Perusahaan ingin mengetahui pelanggan mana yang benar-benar ingin beralih ke pesaing (churn), dan pelanggan mana yang masih stay dan loyal (no churn) agar dapat mengantisipasi terjadinya kerugian.

Dataset ini mewakili profil pelanggan di perusahaan telekomunikasi, termasuk pelanggan yang telah meninggalkan (churn) dan pelanggan yang masih menggunakan layanan (no churn). Churn adalah situasi ketika pelanggan meninggalkan penyedia layanan.

Target: 
- 0 : No Churn / Stay
- 1 : Churn / Turn Over

**Probelm Statement :**

Saat perusahaan berusaha untuk membuat seseorang menjadi pelanggan di perusahaan tersebut, perusahaan pasti sudah mengeluarkan banyak strategi, tenaga, dan waktu untuk mendapatkannya. Hal ini tentu akan sangat disayangkan jika pelanggan tersebut lepas begitu saja.

Oleh sebab itu, sangat penting bagi perusahaan untuk memastikan growth rate perusahaan terus meningkat dan menjaga agar [churn rate](https://majoo.id/solusi/detail/churn) dapat menurun. Salah satu langkah yang dapat diambil untuk menjaga churn rate dapat menurun adalah dengan memprediksi target pelanggan yang tepat agar dapat disesuaikan metode yang akan diambil guna mencegah churn. 

**Goals :**

Berdasarkan permasalahan tersebut, perusahaan ingin memiliki kemampuan untuk memprediksi kemungkinan pelanggan akan churn atau stay, sehingga dapat melakukan tindakan pencegahan yang diperlukan. Karna pelanggan yang berhenti mungkin sulit dan mahal untuk digantikan.

Dan juga, perusahaan ingin mengetahui apa faktor yang membuat pelanggan churn dan stay, sehingga dapat memberikan insentif atau promosi khusus untuk mempertahankan pelanggan yang memiliki kecenderungan akan berhenti dan me-maintaince pelanggan yang masih stay.

**Analytic Approach :**

Jadi yang akan dilakukan adalah menganalisis data untuk menemukan pola yang membedakan pelanggan yang churn dan yang stay.
Kemudian akan dilanjutkan dengan membangun model klasifikasi yang akan membantu perusahaan untuk dapat memprediksi probabilitas seorang pelanggan akan churn atau stay.

**Metric Evaluation**

![image](https://github.com/teguhspt/telco-churn-predict/assets/151754504/09bcd885-34dd-4f2c-adf3-22f3ec408bcf)

**Insight :** <br>

Berdasarkan metric evaluation diatas, dapat kita interpretasikan untuk case yang akan kita kerjakan:
- *Target*
    - 0 (Negative): No Churn (Stay)
    - 1 (Positive): Churn (Turnover)
- *Interpretasi*
    - True Positive (TP)    : Prediksi Pelanggan Churn padahal Aktualnya Churn
    - True Negative (TN)    : Prediksi Pelanggan No Churn padahal Aktualnya No Churn
    - False Positive (FP)   : Prediksi Pelanggan Churn padahal Aktualnya No Churn
    - False Negative (FN)   : Prediksi Pelanggan No Churn padahal Aktualnya Churn

Berdasarkan interpretasi diatas, diketahui ada 2 Error yang akan terjadi, yang dapat merugikan perusahaan
Type 1 error : `False Positive`
- Kita prediksi pelanggan Churn padahal aktualnya No Churn/Stay
- Konsekuensi: Melakukan upaya pencegahan Churn yang tidak perlu, seperti memberikan insentif atau promosi khusus untuk mempertahankan pelanggan yang sebenarnya tidak akan berhenti.

Type 2 error : `False Negative`
- Kita prediksi pelanggan No Churn/Stay padahal aktualnya Churn
- Konsekuensi: Perusahaan mungkin kehilangan pelanggan tanpa melakukan tindakan pencegahan yang diperlukan. Pelanggan yang berhenti mungkin sulit dan mahal untuk digantikan

**Conclusion :** <br>
Risiko akan lebih tinggi ketika terjadi False Negative (FN) : Pelanggan **Churn** di prediksi **No Churn** <br>
Sebagai hasilnya, perusahaan akan kehilangan pelanggan tanpa mendeteksinya secara tepat waktu, yang bisa berdampak negatif pada bisnis.

Berdasarkan konsekuensinya, sebisa mungkin  yang akan kita lakukan adalah mengurangi False Negatives (FN) dan memaksimalkan True Positive (TP), karena FN mewakili situasi di mana model salah memprediksi bahwa pelanggan tidak akan churn padahal sebenarnya mereka akan churn. Alasannya adalah karena konsekuensi dari False Negative lebih berisiko dan merugikan bagi perusahaan. Dengan mengidentifikasi pelanggan yang sebenarnya akan berhenti (Churn) dan mengambil tindakan pencegahan, perusahaan dapat mengurangi kerugian finansial dan juga menjaga kepuasan pelanggan.

Meskipun demikian, perlu diingat bahwa dalam praktiknya, ada trade-off antara False Positive dan False Negative. Seiring dengan upaya meningkatkan sensitivitas model untuk mengurangi False Negative, kita mungkin akan mengalami peningkatan jumlah False Positive. Oleh karena itu, perlu ada keseimbangan yang baik sesuai dengan tujuan dan kebijakan perusahaan.

Berdasarkan konsekuensinya, maka sebisa mungkin yang akan kita lakukan adalah membuat model yang dapat mangantisipasi perusahaan kehilangan pelanggan, tetapi dengan tetap me-maintance pelanggan yang stay untuk menciptakan kepuasan pelanggan. Kita menginginkan sebanyak mungkin prediksi kelas positif yang benar, dengan sedikit mungkin prediksi false negative. Jadi nanti metric utama yang akan kita gunakan adalah **Recall**.

## Data Understanding

Dataset source: [Telco Customer Churn](https://drive.google.com/drive/folders/1_fR7R0srpZgnFnanbrmELgnK-xmzMAHp)

Dataset ini menyajikan informasi yang dapat digunakan untuk menganalisis perilaku churn pelanggan dan mengidentifikasi faktor-faktor yang mempengaruhi keputusan mereka untuk berhenti berlangganan layanan. Berikut adalah ringkasan informasi dalam dataset ini:

1. **Informasi Demografi Pelanggan (`Dependents`):**
   Data ini memberikan wawasan tentang apakah pelanggan memiliki tanggungan atau tidak, yang mungkin dapat memengaruhi kestabilan keanggotaan mereka dalam layanan.
2. **Layanan yang Digunakan oleh Pelanggan:**
   Dataset mencakup informasi tentang berbagai layanan yang dimanfaatkan oleh pelanggan, seperti: `Internet Service`, `Online Security`, `Online Backup`, `Device Protection`, dan `Tech Support`. 
3. **Informasi Akun Pelanggan:**
   Data ini meliputi detail tentang akun pelanggan, termasuk durasi langganan (`tenure`), jenis kontrak yang dimiliki pelanggan (`Contract`), apakah pelanggan menggunakan faktur elektronik atau kertas (`PaperlessBilling`), dan jumlah biaya bulanan (`MonthlyCharges`). 
4. **Status Churn Pelanggan:**
   Terakhir, kolom yang kritis dalam dataset adalah kolom Churn, yang menunjukkan apakah seorang pelanggan telah berhenti berlangganan layanan. Analisis terhadap kolom ini akan membantu dalam memahami pola churn pelanggan dan mengidentifikasi faktor-faktor yang berkaitan dengan keputusan mereka untuk meninggalkan layanan.

Dengan menggunakan dataset ini, akan dilakukan analisis yang cermat untuk mengidentifikasi pola-pola yang terkait dengan churn pelanggan. Hal ini akan membantu dalam mengembangkan strategi retensi yang lebih efektif dan meminimalkan kehilangan pelanggan yang bernilai bagi perusahaan.

### Attribute Information

| Attribute | Data Type | Description |
| --- | --- | --- |
| Dependents | object | Whether the customer has dependents or not |
| tenure | int64 | Number of months the customer has stayed with the company |
| OnlineSecurity | object | Whether the customer has online security or not |
| OnlineBackup | object | Whether the customer has online backup or not |
| InternetService | object | Whether the client is subscribed to Internet service |
| DeviceProtection | object | Whether the client has device protection or not |
| TechSupport | object | Whether the client has tech support or not |
| Contract | object | Type of contract according to duration |
| PaperlessBilling | object | Bills issued in paperless form |
| MonthlyCharges | float64 | Amount of charge for service on monthly bases |
| Churn | object | Whether the customer churns or not (1 - Churn, 0 - Not churns) |

### Steps
1. Data Understanding & Data Cleaning
2. Exploratory Data Analysis
3. Data Preparation: Feature Selection dan Feature Engineering
4. Data Splitting, Modeling.
5. Imbalanced Data Treatment & Hyperparameter Tuning
6. Conclusion & Recommendation

#### Created By : Teguh Saputra | [Email](hi.teguhsaputra@gmail.com) | JCDSOL-012 (C)
