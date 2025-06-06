# FP-KOMNUM-092

Nama Anggota Kelompok 01
Aji Zaenul Mustafa 5025241065 ||
Nick Alan Marpaung 5025241088 ||
Willy Dava Nugraha 5025241090 ||
Farras Abdurrazzaq 5025241091 ||
Abdullah Sultan Barizy 5025241092 <- Me


### STEP 1
impor library pandas untuk fungsi dataframe dan library math untuk fungsi faktorial
```
import pandas as pd
import math
```

### STEP 2
buat dataframe berdasarkan soal
```
df = pd.DataFrame({
    'x': [3., 6., 9., 12., 15., 18., 21., 24., 27.],
    'y': [-741., -186., 32121., 184956., 634575., 1673874., 3741549., 7451256., 13620771.]
})
```
cetak dataframe df
```
df
```

STEP 3
buat kolom Δfx didapat dari selisih kolom y
```
df1 = (df['y'].shift(-1) - df['y'] ) 
```
hapus NaN di baris akhir
```
df1 = df1.dropna() 
```
beri nama kolom dataframe jadi Δfx
```
df1 = df1.to_frame('Δfx')
```
cetak dataframe df1
```
df1
```

STEP 4
buat kolom Δ2fx didapat dari selisih kolom Δfx
```
df2 = (df1['Δfx'].shift(-1) - df1['Δfx'] ) 
```
hapus NaN di baris akhir
```
df2 = df2.dropna() 
```
beri nama kolom dataframe jadi Δ2fx
```
df2 = df2.to_frame('Δ2fx')
```
cetak dataframe df2
```
df2
```

STEP 5
buat kolom Δ3fx didapat dari selisih kolom Δ2fx
```
df3 = (df2['Δ2fx'].shift(-1) - df2['Δ2fx'] ) 
```
hapus NaN di baris akhir
```
df3 = df3.dropna() 
```
beri nama kolom dataframe jadi Δ3fx
```
df3 = df3.to_frame('Δ3fx')
```
cetak dataframe df3
```
df3
```

STEP 6
buat kolom Δ4fx didapat dari selisih kolom Δ3fx
```
df4 = (df3['Δ3fx'].shift(-1) - df3['Δ3fx'] ) 
```
hapus NaN di baris akhir
```
df4 = df4.dropna() 
```
beri nama kolom dataframe jadi Δ3fx
```
df4 = df4.to_frame('Δ4fx')
```
cetak dataframe df4
```
df4
```

STEP 7
buat fungsi untuk mendapatkan indeks dari x0
```
def get_index(x0,df):
    return df[df['x'] == x0].index[0]
```
menggunakan x0 = 15
```
x0 = 15
```
nilai y dicari dari saat x = xs 
```
xs = 16
```
cari indeks x0
```
index_x0 = get_index(x0,df)
```
cetak indeks (indeks dimulai dari nol)
```
index_x0
```

STEP 8
h merupakan selisih nilai x
```
h = df.iloc[1]['x'] - df.iloc[0]['x']
```
cetak nilai h
```
h
```

STEP 9
cari s (s adalah selisih x dari nilai dicari dan x patokan lalu dibagi h)
```
s = (xs - x0) / h
```
cetak nilai s
```
s
```

STEP 10
buat fungsi untuk mencari nilai yang dicari dengan newton gregory forward
```
def ngf_4(index,s,df,df1,df2,df3,df4):
    return  (df.iloc[index]['y']) + \
            (s * df1.iloc[index]['Δfx']) + \
            (s * (s-1) * df2.iloc[index]['Δ2fx'] / math.factorial(2)) + \
            (s * (s-1) * (s-2) * df3.iloc[index]['Δ3fx'] / math.factorial(3)) + \
            (s * (s-1) * (s-2) * (s-3) * df4.iloc[index]['Δ4fx'] / math.factorial(4))
```
mencari hasil newton gregory forward untuk mencari nilai dicari dengan fungsi ngf_4
```
hasil_ngf = ngf_4(index_x0,s,df,df1,df2,df3,df4)
```
mencetak hasil newton gregory forward
```
hasil_ngf
```

STEP 11
mengeprint hasil
```
print(f'Hasil Newton Gregory Forward untuk xs = {xs} menggunakan x0 = {x0} adalah {hasil_ngf}')
```

STEP 12
fungsi mencari error true
```
def error_true(y_true,y_aprox):
    return round(abs( (y_true - y_aprox) / y_true ) * 100,2)
```
nilai y sebenarnya
```
y_true = 897104
```
mencari error true dengan fungsi error_true
```
et = error_true(y_true,hasil_ngf)
```
cetak error true
```
et
```
OPSIONAL cetak error sebelum dibulatkan dua angka belakang koma
```
print(abs( (y_true - hasil_ngf) / y_true ) * 100)
```
