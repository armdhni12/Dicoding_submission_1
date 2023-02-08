<h1 align="center">
Laporan Proyek Mahchine Learning - Achmad Naila Muna Ramadhani
</h1>



# Domain Proyek

## *project Background*: 

Polusi udara adalah permasalahan kompleks di setiap daerah, tak terkecuali di DKI Jakarta.Relawan dan konsultan kesehatan dari Yayasan Alam Sehat Lestari (ASRI), mencatat bahwa kualitas udara di jakarta sangatlah buruk, bahkan 5 kali lebih buruk daripada standar minimum baru yang ditetapkan WHO. Menurut Kementrian Lingkungan Hidup dan Kehutanan (KLHK) sumber utama terjadinya pencemaran udara di kota-kota besar termasuk DKI Jakarta yaitu penggunaan kendaraan motor yang terlalu banyak.

# *Bussiness  Understanding*

## * Problem Statement *
* Bagaimana melakukan klasifikasi kualitas udara di Jakarta berdasarkan nilai kandungan udara dengan menggunakan *Machine Learning*?

## * Goals *
* Membangun model *machine learning* yang dapat melakukan klasifikasi kualitas udara di DKI Jakarta berdasarkan nilai parameter kandungan udara dengan menggunakan *LogisticRegression*

# *Data Understanding*

Merujuk dari permasalahan yang ada saya menggunakan data yang dirilis oleh Jakarta open data, mengenai Indeks Standar Pencemaran Udara (ISPU) di DKI Jakarta dalam satu tahun terakhir dalam rentang waktu bulan januari sampai dengan bulan Oktober Tahun 2021 yang didapat dari pengukuran oleh 5 stasiun pemantau kualitas udara (SPKU) yang ada di Provinsi DKI Jakarta yang berjumlah sebanyak 758 data Indeks Standar Pencemaran Udara(ISPU). Untuk menentukan tingkat kualitas udara ini, parameternya mengacu pada parameter penilaian yang sudah ditentukan oleh Dinas lingkungan hidup Provinsi terkait. Sehingga hasil penelitian nantinya dapat menjadi bahan acuan penilaian bagaimana tingkat kualitas udara yang ada pada Provinsi DKI Jakarta. Dataset diperoleh melalui portal open data provinsi DKI Jakarta pada link: https://data.jakarta.go.id/dataset/indeks-standar-pencemaran-udara-ispu-tahun-2021

## Variabel Data:

* tanggal : Tanggal pengukuran kualitas udara
* stasiun : Lokasi pengukuran di stasiun
* pm10 : Partikulat salah satu parameter yang diukur
* pm25 : Partikulat salah satu parameter yang diukur
* so2 : Sulfida (dalam bentuk SO2) salah satu parameter yang diukur
* co : Carbon Monoksida salah satu parameter yand diukur
* o3 : Ozon salah satu parameter yang diukur
* no2 : NItrogen dioksida salah satu parameter yang diukur
* max : Nilai ukur paling tinggi dari seluruh parameter yang diukur dalam waktu yang sama
* critical : Parameter yang hasil pengukurannya paling tinggi
* categori : Kategori hasil perhitungan indeks standar pencemaran udara

# Data Preparation

## *importing Dataset*

Tahap pertama dalam melakukan data preparation adalah melakukan importing/membaca dataset yang akan digunakan menggunakan pandas karena data yang digunakan menggunakan format csv dalam filenya kemudian dilakukan pengecekan terhadap data secara keseluruhan untuk mengetahui jumlah baris dan kolomnya.

| tanggal    | stasiun                          | pm10 | pm25 | so2 | co  | o3  | no2 | max | critical | categori       |
|------------|----------------------------------|------|------|-----|-----|-----|-----|-----|----------|----------------|
| 2021-10-01 | DKI1 (Bunderan HI)               | 57   | 81   | 30  | 11  | 32  | 38  | 81  | PM25     | SEDANG         |
| 2021-10-02 | DKI1 (Bunderan HI)               | 67   | 99   | 32  | 11  | 30  | 35  | 99  | PM25     | SEDANG         |
| 2021-10-03 | DKI1 (Bunderan HI)               | 70   | 85   | 29  | 10  | 28  | 28  | 85  | PM25     | SEDANG         |
| 2021-10-04 | DKI1 (Bunderan HI)               | 58   | 82   | 30  | 11  | 34  | 29  | 82  | PM25     | SEDANG         |
| 2021-10-05 | DKI1 (Bunderan HI)               | 55   | 76   | 29  | 11  | 30  | 33  | 76  | PM25     | SEDANG         |
| 2021-10-06 | DKI1 (Bunderan HI)               | 60   | 83   | 38  | 10  | 26  | 35  | 83  | PM25     | SEDANG         |
| 2021-10-07 | DKI1 (Bunderan HI)               | 45   | 62   | 29  | 9   | 21  | 28  | 62  | PM25     | SEDANG         |
| 2021-10-08 | DKI1 (Bunderan HI)               | 54   | 77   | 33  | 11  | 24  | 35  | 77  | PM25     | SEDANG         |
| 2021-10-09 | DKI1 (Bunderan HI)               | 52   | 69   | 27  | 9   | 32  | 29  | 69  | PM25     | SEDANG         |
| 2021-10-10 | DKI1 (Bunderan HI)               | 58   | 83   | 26  | 9   | 38  | 26  | 83  | PM25     | SEDANG         |
| 2021-10-11 | DKI1 (Bunderan HI)               | 59   | 80   | 29  | 10  | 35  | 30  | 80  | PM25     | SEDANG         |
| 2021-10-12 | DKI1 (Bunderan HI)               | 56   | 76   | 37  | 9   | 23  | 35  | 76  | PM25     | SEDANG         |
| 2021-10-13 | DKI1 (Bunderan HI)               | 52   | 67   | 28  | 8   | 25  | 31  | 67  | PM25     | SEDANG         |
| 2021-10-14 | DKI1 (Bunderan HI)               | 64   | 90   | 33  | 11  | 35  | 35  | 90  | PM25     | SEDANG         |
| 2021-10-15 | DKI1 (Bunderan HI)               | 75   | 106  | 29  | 12  | 34  | 37  | 106 | PM25     | TIDAK SEHAT    |
| 2021-10-16 | DKI1 (Bunderan HI)               | 66   | 95   | 28  | 15  | 32  | 44  | 95  | PM25     | SEDANG         |
| 2021-10-17 | DKI1 (Bunderan HI)               | 65   | 93   | 34  | 11  | 36  | 30  | 93  | PM25     | SEDANG         |
| 2021-10-18 | DKI1 (Bunderan HI)               | 44   | 55   | 25  | 9   | 19  | 26  | 55  | PM25     | SEDANG         |
| 2021-10-19 | DKI1 (Bunderan HI)               | 41   | 58   | 29  | 14  | 15  | 30  | 58  | PM25     | SEDANG         |
| 2021-10-20 | DKI1 (Bunderan HI)               | 33   | 53   | 29  | 10  | 21  | 27  | 53  | PM25     | SEDANG         |
| 2021-10-21 | DKI1 (Bunderan HI)               | 45   | 65   | 25  | 9   | 28  | 32  | 65  | PM25     | SEDANG         |
| 2021-10-22 | DKI1 (Bunderan HI)               | 64   | 95   | 31  | 18  | 19  | 48  | 95  | PM25     | SEDANG         |
| 2021-10-23 | DKI1 (Bunderan HI)               | 57   | 83   | 29  | 10  | 20  | 36  | 83  | PM25     | SEDANG         |
| 2021-10-24 | DKI1 (Bunderan HI)               | 58   | 85   | 27  | 11  | 28  | 36  | 85  | PM25     | SEDANG         |
| 2021-10-25 | DKI1 (Bunderan HI)               | 62   | 95   | 27  | 14  | 33  | 37  | 95  | PM25     | SEDANG         |
| 2021-10-26 | DKI1 (Bunderan HI)               | 55   | 78   | 29  | 14  | 23  | 43  | 78  | PM25     | SEDANG         |
| 2021-10-27 | DKI1 (Bunderan HI)               | 55   | 76   | 29  | 15  | 22  | 39  | 76  | PM25     | SEDANG         |
| 2021-10-28 | DKI1 (Bunderan HI)               | 51   | 69   | 28  | 16  | 22  | 39  | 69  | PM25     | SEDANG         |
| 2021-10-29 | DKI1 (Bunderan HI)               | 50   | 64   | 31  | 19  | 18  | 35  | 64  | PM25     | SEDANG         |
| 2021-10-30 | DKI1 (Bunderan HI)               | 48   | 68   | 31  | 12  | 25  | 40  | 68  | PM25     | SEDANG         |
| 2021-10-31 | DKI1 (Bunderan HI)               | 53   | 70   | 27  | 11  | 32  | 32  | 70  | PM25     | SEDANG         |
| 2021-10-01 | DKI2 (Kelapa Gading)             | 57   | 84   | 59  | 10  | 65  | 16  | 84  | PM25     | SEDANG         |
| 2021-10-02 | DKI2 (Kelapa Gading)             | 70   | 103  | 61  | 10  | 58  | 17  | 103 | PM25     | TIDAK SEHAT    |
| 2021-10-03 | DKI2 (Kelapa Gading)             | 64   | 86   | 62  | 11  | 53  | 18  | 86  | PM25     | SEDANG         |
| 2021-10-04 | DKI2 (Kelapa Gading)             | 62   | 95   | 60  | 11  | 64  | 24  | 95  | PM25     | SEDANG         |
| 2021-10-05 | DKI2 (Kelapa Gading)             | 65   | 90   | 67  | 11  | 54  | 27  | 90  | PM25     | SEDANG         |
| 2021-10-06 | DKI2 (Kelapa Gading)             | 65   | 91   | 66  | 9   | 58  | 23  | 91  | PM25     | SEDANG         |
| 2021-10-07 | DKI2 (Kelapa Gading)             | 49   | 64   | 60  | 9   | 50  | 20  | 64  | PM25     | SEDANG         |
| 2021-10-08 | DKI2 (Kelapa Gading)             | 60   | 85   | 64  | 10  | 54  | 20  | 85  | PM25     | SEDANG         |
| 2021-10-09 | DKI2 (Kelapa Gading)             | 53   | 77   | 62  | 9   | 60  | 19  | 77  | PM25     | SEDANG         |
| 2021-10-10 | DKI2 (Kelapa Gading)             | 60   | 83   | 61  | 9   | 72  | 12  | 83  | PM25     | SEDANG         |
| 2021-10-11 | DKI2 (Kelapa Gading)             | 68   | 100  | 64  | 12  | 66  | 26  | 100 | PM25     | SEDANG         |
| 2021-10-12 | DKI2 (Kelapa Gading)             | 77   | 105  | 76  | 12  | 49  | 31  | 105 | PM25     | TIDAK SEHAT    |
| 2021-10-13 | DKI2 (Kelapa Gading)             | 57   | 76   | 63  | 9   | 58  | 18  | 76  | PM25     | SEDANG         |
| 2021-10-14 | DKI2 (Kelapa Gading)             | 73   | 105  | 65  | 12  | 70  | 28  | 105 | PM25     | TIDAK SEHAT    |
| 2021-10-15 | DKI2 (Kelapa Gading)             | 82   | 108  | 64  | 13  | 64  | 27  | 108 | PM25     | TIDAK SEHAT    |
| 2021-10-16 | DKI2 (Kelapa Gading)             | 64   | 95   | 63  | 13  | 63  | 28  | 95  | PM25     | SEDANG         |
| 2021-10-17 | DKI2 (Kelapa Gading)             | 71   | ---  | 63  | 12  | 65  | 22  | 71  | PM10     | SEDANG         |
| 2021-10-18 | DKI2 (Kelapa Gading)             | 50   | 60   | 58  | 9   | 45  | 13  | 60  | PM25     | SEDANG         |
| 2021-10-19 | DKI2 (Kelapa Gading)             | 46   | 63   | 60  | 16  | 42  | 29  | 63  | PM25     | SEDANG         |
| 2021-10-20 | DKI2 (Kelapa Gading)             | 50   | 67   | 73  | 11  | 50  | 26  | 73  | SO2      | SEDANG         |
| 2021-10-21 | DKI2 (Kelapa Gading)             | 52   | 68   | 61  | 9   | 57  | 24  | 68  | PM25     | SEDANG         |
| 2021-10-22 | DKI2 (Kelapa Gading)             | 73   | 115  | 82  | 14  | 46  | 38  | 115 | PM25     | TIDAK SEHAT    |
| 2021-10-23 | DKI2 (Kelapa Gading)             | 67   | 95   | 81  | 10  | 53  | 28  | 95  | PM25     | SEDANG         |
| 2021-10-24 | DKI2 (Kelapa Gading)             | 62   | 96   | 60  | 12  | 62  | 21  | 96  | PM25     | SEDANG         |
| 2021-10-25 | DKI2 (Kelapa Gading)             | 65   | 100  | 62  | 12  | 70  | 27  | 100 | PM25     | SEDANG         |
| 2021-10-26 | DKI2 (Kelapa Gading)             | 63   | 83   | 67  | 13  | 50  | 32  | 83  | PM25     | SEDANG         |
| 2021-10-27 | DKI2 (Kelapa Gading)             | 62   | 86   | 64  | 10  | 49  | 21  | 86  | PM25     | SEDANG         |
| 2021-10-28 | DKI2 (Kelapa Gading)             | 51   | 70   | 67  | 12  | 49  | 30  | 70  | PM25     | SEDANG         |
| 2021-10-29 | DKI2 (Kelapa Gading)             | 54   | 74   | 80  | 14  | 49  | 26  | 80  | SO2      | SEDANG         |
| 2021-10-30 | DKI2 (Kelapa Gading)             | 64   | 90   | 81  | 13  | 56  | 32  | 90  | PM25     | SEDANG         |
| 2021-10-31 | DKI2 (Kelapa Gading)             | 56   | 79   | 63  | 12  | 56  | 28  | 79  | PM25     | SEDANG         |
| 2021-10-01 | DKI3 (Jagakarsa)                 | 58   | 77   | 49  | 9   | 35  | 11  | 77  | PM25     | SEDANG         |
| 2021-10-02 | DKI3 (Jagakarsa)                 | 64   | 100  | 50  | 12  | 28  | 27  | 100 | PM25     | SEDANG         |
| 2021-10-03 | DKI3 (Jagakarsa)                 | 54   | 76   | 50  | 8   | 32  | 14  | 76  | PM25     | SEDANG         |
| 2021-10-04 | DKI3 (Jagakarsa)                 | 52   | 72   | 50  | 9   | 36  | 11  | 72  | PM25     | SEDANG         |
| 2021-10-05 | DKI3 (Jagakarsa)                 | 42   | 65   | 51  | 7   | 36  | 10  | 65  | PM25     | SEDANG         |
| 2021-10-06 | DKI3 (Jagakarsa)                 | 48   | 67   | 51  | 6   | 34  | 11  | 67  | PM25     | SEDANG         |
| 2021-10-07 | DKI3 (Jagakarsa)                 | 44   | 62   | 50  | 7   | 28  | 11  | 62  | PM25     | SEDANG         |
| 2021-10-08 | DKI3 (Jagakarsa)                 | ---  | ---  | --- | --- | --- | --- | 0   |          | TIDAK ADA DATA |
| 2021-10-09 | DKI3 (Jagakarsa)                 | 45   | 63   | 51  | 7   | 38  | 11  | 63  | PM25     | SEDANG         |
| 2021-10-10 | DKI3 (Jagakarsa)                 | 55   | 77   | 51  | 9   | 40  | 14  | 77  | PM25     | SEDANG         |
| 2021-10-11 | DKI3 (Jagakarsa)                 | 58   | 79   | 51  | 10  | 39  | 12  | 79  | PM25     | SEDANG         |
| 2021-10-12 | DKI3 (Jagakarsa)                 | 47   | 65   | 51  | 8   | 37  | 11  | 65  | PM25     | SEDANG         |
| 2021-10-13 | DKI3 (Jagakarsa)                 | 52   | 71   | 52  | 9   | 38  | 15  | 71  | PM25     | SEDANG         |
| 2021-10-14 | DKI3 (Jagakarsa)                 | 61   | 88   | 51  | 12  | 32  | 17  | 88  | PM25     | SEDANG         |
| 2021-10-15 | DKI3 (Jagakarsa)                 | 72   | 107  | 52  | 14  | 40  | 19  | 107 | PM25     | TIDAK SEHAT    |
| 2021-10-16 | DKI3 (Jagakarsa)                 | 64   | 92   | 51  | 15  | 35  | 18  | 92  | PM25     | SEDANG         |
| 2021-10-17 | DKI3 (Jagakarsa)                 | 65   | 95   | 51  | 15  | 39  | 18  | 95  | PM25     | SEDANG         |
| 2021-10-18 | DKI3 (Jagakarsa)                 | 51   | 66   | 50  | 11  | 24  | 15  | 66  | PM25     | SEDANG         |
| 2021-10-19 | DKI3 (Jagakarsa)                 | 45   | 61   | 50  | 15  | 18  | 17  | 61  | PM25     | SEDANG         |
| 2021-10-20 | DKI3 (Jagakarsa)                 | 36   | 52   | 51  | 10  | 29  | 12  | 52  | PM25     | SEDANG         |
| 2021-10-21 | DKI3 (Jagakarsa)                 | 53   | 74   | 53  | 11  | 29  | 15  | 74  | PM25     | SEDANG         |
| 2021-10-22 | DKI3 (Jagakarsa)                 | 58   | 82   | 51  | 15  | --- | 17  | 82  | PM25     | SEDANG         |
| 2021-10-23 | DKI3 (Jagakarsa)                 | 59   | 87   | 52  | 13  | 39  | 21  | 87  | PM25     | SEDANG         |
| 2021-10-24 | DKI3 (Jagakarsa)                 | 68   | 102  | 51  | 17  | 47  | 18  | 102 | PM25     | TIDAK SEHAT    |
| 2021-10-25 | DKI3 (Jagakarsa)                 | 62   | 90   | 51  | 13  | 38  | 15  | 90  | PM25     | SEDANG         |
| 2021-10-26 | DKI3 (Jagakarsa)                 | 51   | 71   | 51  | 13  | 30  | 15  | 71  | PM25     | SEDANG         |
| 2021-10-27 | DKI3 (Jagakarsa)                 | 45   | 64   | 52  | 8   | 33  | 13  | 64  | PM25     | SEDANG         |
| 2021-10-28 | DKI3 (Jagakarsa)                 | 47   | 60   | 51  | 14  | 15  | 18  | 60  | PM25     | SEDANG         |
| 2021-10-29 | DKI3 (Jagakarsa)                 | 37   | 31   | 52  | 17  | 13  | 18  | 52  | SO2      | SEDANG         |
| 2021-10-30 | DKI3 (Jagakarsa)                 | 48   | 31   | 51  | 12  | 39  | 18  | 51  | SO2      | SEDANG         |
| 2021-10-31 | DKI3 (Jagakarsa)                 | 45   | 27   | --- | 28  | 39  | --- | 45  | PM10     | BAIK           |
| 2021-10-01 | DKI4 (Lubang Buaya)              | ---  | 91   | 45  | 10  | 35  | 33  | 91  | PM25     | SEDANG         |
| 2021-10-02 | DKI4 (Lubang Buaya)              | ---  | 127  | 46  | 10  | 35  | 19  | 127 | PM25     | TIDAK SEHAT    |
| 2021-10-03 | DKI4 (Lubang Buaya)              | ---  | 96   | 44  | 9   | 32  | 19  | 96  | PM25     | SEDANG         |
| 2021-10-04 | DKI4 (Lubang Buaya)              | ---  | 110  | 44  | 11  | 33  | 24  | 110 | PM25     | TIDAK SEHAT    |
| 2021-10-05 | DKI4 (Lubang Buaya)              | ---  | ---  | --- | --- | --- | --- | 0   |          | TIDAK ADA DATA |
| 2021-10-06 | DKI4 (Lubang Buaya)              | 66   | 103  | 47  | 8   | 37  | 17  | 103 | PM25     | TIDAK SEHAT    |
| 2021-10-07 | DKI4 (Lubang Buaya)              | 52   | 77   | 41  | 7   | 27  | 23  | 77  | PM25     | SEDANG         |
| 2021-10-08 | DKI4 (Lubang Buaya)              | 58   | 98   | 45  | 9   | 30  | 22  | 98  | PM25     | SEDANG         |
| 2021-10-09 | DKI4 (Lubang Buaya)              | 55   | 83   | 47  | 7   | 36  | 21  | 83  | PM25     | SEDANG         |
| 2021-10-10 | DKI4 (Lubang Buaya)              | 61   | 97   | 42  | 9   | 43  | 16  | 97  | PM25     | SEDANG         |
| 2021-10-11 | DKI4 (Lubang Buaya)              | 62   | 100  | 43  | 10  | 44  | 26  | 100 | PM25     | SEDANG         |
| 2021-10-12 | DKI4 (Lubang Buaya)              | 70   | 111  | 47  | 9   | 32  | 25  | 111 | PM25     | TIDAK SEHAT    |
| 2021-10-13 | DKI4 (Lubang Buaya)              | ---  | 91   | 44  | 8   | 38  | 19  | 91  | PM25     | SEDANG         |
| 2021-10-14 | DKI4 (Lubang Buaya)              | ---  | 131  | 44  | 12  | 45  | 32  | 131 | PM25     | TIDAK SEHAT    |
| 2021-10-15 | DKI4 (Lubang Buaya)              | 100  | 157  | 41  | 15  | 50  | 26  | 157 | PM25     | TIDAK SEHAT    |
| 2021-10-16 | DKI4 (Lubang Buaya)              | 67   | 122  | 40  | 14  | 51  | 23  | 122 | PM25     | TIDAK SEHAT    |
| 2021-10-17 | DKI4 (Lubang Buaya)              | ---  | 126  | 39  | 13  | 53  | 27  | 126 | PM25     | TIDAK SEHAT    |
| 2021-10-18 | DKI4 (Lubang Buaya)              | 57   | 88   | 42  | 11  | 32  | 19  | 88  | PM25     | SEDANG         |
| 2021-10-19 | DKI4 (Lubang Buaya)              | 52   | 80   | 41  | 18  | 31  | 23  | 80  | PM25     | SEDANG         |
| 2021-10-20 | DKI4 (Lubang Buaya)              | ---  | 96   | 45  | 10  | 33  | 17  | 96  | PM25     | SEDANG         |
| 2021-10-21 | DKI4 (Lubang Buaya)              | ---  | ---  | 44  | 10  | 48  | 18  | 48  | O3       | BAIK           |
| 2021-10-22 | DKI4 (Lubang Buaya)              | 71   | 120  | 45  | 13  | 36  | 21  | 120 | PM25     | TIDAK SEHAT    |
| 2021-10-23 | DKI4 (Lubang Buaya)              | 65   | 109  | 45  | 10  | 35  | 20  | 109 | PM25     | TIDAK SEHAT    |
| 2021-10-24 | DKI4 (Lubang Buaya)              | 68   | 113  | 44  | 15  | 39  | 23  | 113 | PM25     | TIDAK SEHAT    |
| 2021-10-25 | DKI4 (Lubang Buaya)              | 62   | 104  | 44  | 11  | 41  | 22  | 104 | PM25     | TIDAK SEHAT    |
| 2021-10-26 | DKI4 (Lubang Buaya)              | 75   | 130  | 45  | 16  | 36  | 24  | 130 | PM25     | TIDAK SEHAT    |
| 2021-10-27 | DKI4 (Lubang Buaya)              | 59   | 90   | 43  | 10  | 50  | 21  | 90  | PM25     | SEDANG         |
| 2021-10-28 | DKI4 (Lubang Buaya)              | 54   | 78   | 40  | 11  | 56  | 18  | 78  | PM25     | SEDANG         |
| 2021-10-29 | DKI4 (Lubang Buaya)              | 51   | 79   | 41  | 15  | 45  | 15  | 79  | PM25     | SEDANG         |
| 2021-10-30 | DKI4 (Lubang Buaya)              | 62   | 103  | 43  | 15  | 58  | 18  | 103 | PM25     | TIDAK SEHAT    |
| 2021-10-31 | DKI4 (Lubang Buaya)              | ---  | 79   | --- | --- | --- | --- | 79  | PM25     | SEDANG         |
| 2021-10-01 | DKI5 (Kebon Jeruk) Jakarta Barat | 55   | 84   | --- | 8   | 34  | 12  | 84  | PM25     | SEDANG         |
| 2021-10-02 | DKI5 (Kebon Jeruk) Jakarta Barat | 67   | 102  | --- | 10  | 31  | 16  | 102 | PM25     | TIDAK SEHAT    |
| 2021-10-03 | DKI5 (Kebon Jeruk) Jakarta Barat | 55   | 82   | --- | 8   | 28  | 12  | 82  | PM25     | SEDANG         |
| 2021-10-04 | DKI5 (Kebon Jeruk) Jakarta Barat | 53   | 80   | --- | 7   | 31  | 10  | 80  | PM25     | SEDANG         |
| 2021-10-05 | DKI5 (Kebon Jeruk) Jakarta Barat | 52   | 79   | --- | 10  | 35  | 16  | 79  | PM25     | SEDANG         |
| 2021-10-06 | DKI5 (Kebon Jeruk) Jakarta Barat | 52   | 74   | --- | 6   | 28  | 14  | 74  | PM25     | SEDANG         |
| 2021-10-07 | DKI5 (Kebon Jeruk) Jakarta Barat | 50   | 71   | --- | 8   | 25  | 17  | 71  | PM25     | SEDANG         |
| 2021-10-08 | DKI5 (Kebon Jeruk) Jakarta Barat | 53   | 81   | --- | 7   | 32  | 16  | 81  | PM25     | SEDANG         |
| 2021-10-09 | DKI5 (Kebon Jeruk) Jakarta Barat | 53   | 74   | --- | 7   | 43  | 12  | 74  | PM25     | SEDANG         |
| 2021-10-10 | DKI5 (Kebon Jeruk) Jakarta Barat | 55   | 80   | --- | 8   | 46  | 11  | 80  | PM25     | SEDANG         |
| 2021-10-11 | DKI5 (Kebon Jeruk) Jakarta Barat | 59   | 88   | --- | 9   | 39  | 11  | 88  | PM25     | SEDANG         |
| 2021-10-12 | DKI5 (Kebon Jeruk) Jakarta Barat | 57   | 81   | --- | 12  | 31  | 23  | 81  | PM25     | SEDANG         |
| 2021-10-13 | DKI5 (Kebon Jeruk) Jakarta Barat | 47   | 69   | --- | 7   | 30  | 13  | 69  | PM25     | SEDANG         |
| 2021-10-14 | DKI5 (Kebon Jeruk) Jakarta Barat | 58   | 91   | --- | 10  | 35  | 14  | 91  | PM25     | SEDANG         |
| 2021-10-15 | DKI5 (Kebon Jeruk) Jakarta Barat | 70   | 107  | --- | 11  | 39  | 16  | 107 | PM25     | TIDAK SEHAT    |
| 2021-10-16 | DKI5 (Kebon Jeruk) Jakarta Barat | 68   | 112  | --- | 14  | 32  | 17  | 112 | PM25     | TIDAK SEHAT    |
| 2021-10-17 | DKI5 (Kebon Jeruk) Jakarta Barat | 62   | 100  | --- | 11  | 48  | 10  | 100 | PM25     | SEDANG         |
| 2021-10-18 | DKI5 (Kebon Jeruk) Jakarta Barat | 52   | 73   | --- | 11  | 19  | 15  | 73  | PM25     | SEDANG         |
| 2021-10-19 | DKI5 (Kebon Jeruk) Jakarta Barat | 50   | 81   | --- | 16  | 13  | 35  | 81  | PM25     | SEDANG         |
| 2021-10-20 | DKI5 (Kebon Jeruk) Jakarta Barat | 42   | 68   | --- | 11  | 22  | 23  | 68  | PM25     | SEDANG         |
| 2021-10-21 | DKI5 (Kebon Jeruk) Jakarta Barat | 42   | 70   | --- | 7   | 34  | 14  | 70  | PM25     | SEDANG         |
| 2021-10-22 | DKI5 (Kebon Jeruk) Jakarta Barat | 60   | 95   | --- | 15  | 24  | 26  | 95  | PM25     | SEDANG         |
| 2021-10-23 | DKI5 (Kebon Jeruk) Jakarta Barat | 52   | 80   | --- | 10  | 29  | 16  | 80  | PM25     | SEDANG         |
| 2021-10-24 | DKI5 (Kebon Jeruk) Jakarta Barat | 60   | 93   | --- | 12  | 35  | 14  | 93  | PM25     | SEDANG         |
| 2021-10-25 | DKI5 (Kebon Jeruk) Jakarta Barat | 64   | 101  | --- | 13  | 36  | 14  | 101 | PM25     | TIDAK SEHAT    |
| 2021-10-26 | DKI5 (Kebon Jeruk) Jakarta Barat | 58   | 92   | --- | 16  | 29  | 24  | 92  | PM25     | SEDANG         |
| 2021-10-27 | DKI5 (Kebon Jeruk) Jakarta Barat | 53   | 76   | --- | 11  | 32  | 17  | 76  | PM25     | SEDANG         |
| 2021-10-28 | DKI5 (Kebon Jeruk) Jakarta Barat | 51   | 77   | --- | 16  | 29  | 27  | 77  | PM25     | SEDANG         |
| 2021-10-29 | DKI5 (Kebon Jeruk) Jakarta Barat | 50   | 70   | --- | 18  | 23  | 33  | 70  | PM25     | SEDANG         |
| 2021-10-30 | DKI5 (Kebon Jeruk) Jakarta Barat | 50   | 74   | --- | 12  | 30  | 24  | 74  | PM25     | SEDANG         |
| 2021-10-31 | DKI5 (Kebon Jeruk) Jakarta Barat | 49   | 74   | --- | 10  | 31  | 13  | 74  | PM25     | SEDANG         |

## Menghapus colom yang tidak diperlukan

Tahap berikutnya adalah melakukan penghapusan kolom data yang tidak diperlukan seperti kolom tanggal dan kolom max dan critical yang berisi nilai terbesar dari salah satu nilai variabel

## Memeriksa informasi tipe data pada tiap variabel

tahap berikutnya adalah melakukan pengecekan rangkuman tipe data pada tiap tiap variabel paada dataset
| #   | Column   | Non-Null Count | Dtype   |
|-----|----------|----------------|---------|
| --- | ------   | -------------- | -----   |
| 0   | stasiun  | 758 non-null   | object  |
| 1   | pm10     | 731 non-null   | float64 |
| 2   | pm25     | 688 non-null   | float64 |
| 3   | so2      | 687 non-null   | float64 |
| 4   | co       | 757 non-null   | float64 |
| 5   | o3       | 755 non-null   | float64 |
| 6   | no2      | 746 non-null   | float64 |
| 7   | categori | 758 non-null   | object  |

## Memeriksa nilai kosong pada dataset
 tahap selanjutnya adalah melakukan pengecekan nilai Nan/nilai kosong pada tiap tiap kolom pada dataset kemudian menggantikan nilai pada kolom yang memiliki nilai kosong dengan nilai rata rata dari tiap kolom variabel pada dataset

| stasiun  | 0  |
|----------|----|
| pm10     | 27 |
| pm25     | 70 |
| so2      | 71 |
| co       | 1  |
| o3       | 3  |
| no2      | 12 |
| categori | 0  |

berikut ini merupakan tabel jumlah nilai kosong pada dataset setelah dilakukan filling menggunakan nilai dari mean pada setiap variabel
| stasiun  | 0 |
|----------|---|
| pm10     | 0 |
| pm25     | 0 |
| so2      | 0 |
| co       | 0 |
| o3       | 0 |
| no2      | 0 |
| categori | 0 |

#EDA
## Dataset Ploting

melakukan pengecekan jumlah pada tiap tiap variabel dengan menggunakan histogram
![download (1)](https://user-images.githubusercontent.com/79986070/217573443-2c2023a0-2931-46b7-b5c2-a46f2a8e0d2d.png)


## *Dataset Correlation Check*

melakukan pengecekan terhadap keterkaitan antara satu variabel dengan variabel lainnya dengan menggunakan correlation matrix  yang dimana semakin tinggi atau semakin terang warna pada kolom matriks maka nilai keterkaitan antar variabel juga semakin tinggi
![download (2)](https://user-images.githubusercontent.com/79986070/217573676-5438406a-7e47-4510-aa09-1f86a61bdcd5.png)


## Cek persentase jumlah kategori kualitas udara

melakukan pengecekan jumlah persentase antara tiap tiap kategori yang dimana jika persentasenya semakin tinggi maka semakin banyak pula jumlah kategori yang terdapat pada dataset 
![download (3)](https://user-images.githubusercontent.com/79986070/217573914-ad12519f-6872-49eb-824d-07c07e4ed417.png)


## Cek hubungan antar variabel terhadap kategori pada dataset

hal ini dilakukan untuk melakukan pemeriksaan hubungan keterkaitan antara tiap variabel indeks dengan kategori dengan menggunakan pairplot
![download (4)](https://user-images.githubusercontent.com/79986070/217573977-b17a5c2b-168a-4e66-bf30-d2d169240d9a.png)


# Modelling

## Dataset Splitting

tahap pertama adalah melakukan Data splitting dengan membagi dataset menjadi X_train,y_train,X_test dan y_test dengan menggunakan train_test_split dengan test_size sebesar  20% dan training data sebesar 80% yang nantinya akan digunakan untuk dilatih dalam model *machine learning*

## Import and Define Model

tahap selanjutnya adalah melakukan importing model dari library scikit learn yaitu algoritma fungsi *LogisticRegresion* kemudian mendefinisikan fungsi model sebagai variabel logreg dengan parameter solver menggunakan 'lbfgs' yang dimana solver ini adalah nilai default untuk melakukan permasalahan klasifikasi multi kelas,parameter selanjutnya adalah nilai iterasi maksimal yang berada pada 400 iterasi.

### Cara kerja model *LogisticRegression*
pada topik kali ini digunakan model LogisticRegression untuk melakukan training,yang dimana model ini memiliki cara kerja yaitu dengan mencari masalah keterhubungan antara variabel independen dengan variabel dependen dengan probabilitas hasil diskrit tertentu. contohnya pada kasus kali ini adalah menentukan apakah kualitas udara di DKI Jakarta baik atau buruk berdasarkan nilai input Indeks Standar Pencemaran Udara (ISPU)


## Model Fitting

tahapan selanjutnya adalah melakuka model fitting dengan menggunakan nilai X_train dan y_train yang telah dilakukan splitting pada beberapa tahap sebelumnya sebesar 80% untuk data training

# Evaluation

Proses evaluasi digunakan menggunakan nilai dari confussion matrix yang dimana model logisticregression mampu bekerja lebih baik karena menghasilkan nilai akurasi,recall dan f1 score dengan rata rata nilai sebesar 94%.
Nilai nilai matriks diatas dapat diperoleh melalui beberapa parameter berikut
* True Positive(TP): merupakan jumlah record data positif yang benar diklasifikasikan sebagai nilai positif
* False Negative(FN): merupakan jumlah record data positif yang diklasifikasikan sebagai nilai yang negative
* False Positive(FP): merupakan jumlah record data yang bernilai negative namun diklasifikasikan sebagai data yang memiliki nilai positif
* True Negative(TN): merupakan jumlah record data yang bernilai negative dan diklasifikasikan sebagai nilai yang negative.

Hasil dari Confussion Matrix akan digunakan sebagai acuan untuk perhitungan evaluasi dengan menggunakan F1 Score,Recall dan 
Precission serta tingkat akurasi.

* Precission: Precission dapat memberitahu kita mengenai seberapa banyak kasus prediksi benar yang ternyata positif. Nilai dari metriks ini dapat menentukan jika model dapat digunakan atau tidak [1]. 𝑃𝑟𝑒𝑐𝑖𝑠𝑖𝑜𝑛 =𝑇𝑟𝑢𝑒 𝑝𝑜𝑠𝑖𝑡𝑖𝑣𝑒 / 𝑇𝑟𝑢𝑒 𝑝𝑜𝑠𝑖𝑡𝑖𝑣𝑒 + 𝐹𝑎𝑙𝑠𝑒 𝑃𝑜𝑠𝑖𝑡𝑖𝑣𝑒
* Recall Metrics: Recall menunjukan jumlah kasus yang benar benar positif yang dapat diprediksi dengan benar menggunakan model. Nilai recall dapat diperoleh melalui persamaan berikut [1]: 𝑅𝑒𝑐𝑎𝑙𝑙 =𝑇𝑟𝑢𝑒 𝑝𝑜𝑠𝑖𝑡𝑖𝑣𝑒 / 𝑇𝑟𝑢𝑒 𝑝𝑜𝑠𝑖𝑡𝑖𝑣𝑒 + 𝐹𝑎𝑙𝑠𝑒 𝑁𝑒𝑔𝑎𝑡𝑖𝑣𝑒
* F1 Score: F1 Score memberikan kita kombinasi data antara precision dan Recall,yang berarti jika kita mencoba meningkatkan nilai dari precision dan recall akan menurun begitu juga sebaliknya [1]. Nilai dari F1 Score dapat diperoleh melalui persamaan berikut: 𝐹1 𝑆𝑐𝑜𝑟𝑒 = 2 ∗(𝑝𝑟𝑒𝑐𝑖𝑠𝑖𝑜𝑛 ∗ 𝑟𝑒𝑐𝑎𝑙𝑙)/(𝑝𝑟𝑒𝑐𝑖𝑠𝑠𝑖𝑜𝑛 + 𝑟𝑒𝑐𝑎𝑙𝑙)
* Accuracy: Accuracy merupakan sebuah fraksi dari sebuah prediksi yang benar dan total dari prediksi yang dibuat oleh pengklasifikasian [1].𝐴𝑐𝑐𝑢𝑟𝑎𝑐𝑦 =𝑇𝑟𝑢𝑒 𝑃𝑜𝑠𝑖𝑡𝑖𝑣𝑒 + 𝑇𝑟𝑢𝑒 𝑁𝑒𝑔𝑎𝑡𝑖𝑣𝑒/𝑇𝑃 + 𝑇𝑁 + 𝐹𝑃 + 𝐹N

berikut merupakan hasil dari nilai *Precision,Recall F1 score dan accuracy* dengan menggunakan LogisticRegression:
* accuracy_Logistic Regression : 0.947
* precision_Logistic Regression : 0.947
* recall_Logistic Regression: 0.947
* f1-score_Logistic Regression : 0.947

Berdasarkan perhitungan menggunakan berbagai formula diatas dapat disimpulkan bahwa model yang dibangun menggunakan LogisticRegression mampu melakukan klasifikasi kualitas udara berdasarkan parameter kandungan udara karena mampu menghasilkan rata rata nilai matriks diatas 90%

# References
[1] A. Tasnim, M. Saiduzzaman, M. A. Rahman, J. Akhter, and A. S. M. M. Rahaman, “Performance Evaluation of Multiple Classifiers for Predicting Fake News,” J. Comput. Commun., vol. 10, no. 09, pp. 1–21, 2022, doi: 10.4236/jcc.2022.109001.



