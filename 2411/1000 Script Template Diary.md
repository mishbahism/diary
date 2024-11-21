# Minggu 10 November 2024

Rekap Hari Ini:

- Pagi aku kesiangan
- Aku antar londri, 6 jam 10rb, aku bayar 23rb
- Aku beli susu 9300, padahal tulisannya 9400. 9000? 300. Aku iseng keluarin 9000, baru 500. Trus gaada kembalian, jadi 9000 aja. Alhamdulillah.
- Aku sarapan ketoprak 13rb, enak.
- Aku naik tj sekarang nih.
- Aku berencana, nulis template unutuk beberapa bulan ke depan, pake script. Ntar tanya chatgpt aja. Jadi yang perlu kulakukan tinggal edit-edit aja, gaperlu bikin file ulang, ubah ulang judul, baru nulis Rekap hari ini tiap kali mau nulis. Biar gampang gitu tinggal isi isi aja.
- Aku nyelesaikan tugas inputan ke halosis, speedrun 29 artikel dapet 17 menit. Cuman emang dikit kek copas-copas gitu aja.
- Aku bikin script powershell (by ChatGPT) untuk generate template diary-ku sampai 3 bulan ke depan. Ini kodenya.

<details>
    <summary>Lihat Script</summary>

```powershell
# Menangkap input batas bulan dari pengguna
param (
    [Parameter(Mandatory=$true)]
    [int]$batasBulan
)

# Fungsi untuk menerjemahkan nama hari ke bahasa Indonesia
function Get-IndonesianDay {
    param ([string]$day)
    switch ($day) {
        "Sunday"    { return "Minggu" }
        "Monday"    { return "Senin" }
        "Tuesday"   { return "Selasa" }
        "Wednesday" { return "Rabu" }
        "Thursday"  { return "Kamis" }
        "Friday"    { return "Jumat" }
        "Saturday"  { return "Sabtu" }
        default     { return $day }
    }
}

# Fungsi untuk menerjemahkan nama bulan ke bahasa Indonesia
function Get-IndonesianMonth {
    param ([string]$month)
    switch ($month) {
        "January"   { return "Januari" }
        "February"  { return "Februari" }
        "March"     { return "Maret" }
        "April"     { return "April" }
        "May"       { return "Mei" }
        "June"      { return "Juni" }
        "July"      { return "Juli" }
        "August"    { return "Agustus" }
        "September" { return "September" }
        "October"   { return "Oktober" }
        "November"  { return "November" }
        "December"  { return "Desember" }
        default     { return $month }
    }
}

# Mendapatkan tanggal hari ini dan batas ke depan
$today = Get-Date
$endDate = $today.AddMonths($batasBulan)

# Looping untuk setiap hari dari hari ini hingga batas ke depan
while ($today -lt $endDate) {
    # Membuat nama folder dan file berdasarkan tanggal
    $yy_mm = $today.ToString("yyMM")         # Format folder YYMM
    $dd00 = $today.ToString("dd") + "00.md"  # Format file DD00.md

    # Menerjemahkan hari dan bulan ke bahasa Indonesia
    $dayName = Get-IndonesianDay -day $today.DayOfWeek.ToString()
    $monthName = Get-IndonesianMonth -month $today.ToString("MMMM")

    # Konten file sesuai template dengan hari dan bulan dalam bahasa Indonesia
    $fileContent = @"
# $dayName, $($today.ToString("dd")) $monthName $($today.ToString("yyyy"))

Rekap Hari Ini:

- Bangun tidur
"@

    # Membuat folder jika belum ada
    $folderPath = Join-Path -Path (Get-Location) -ChildPath $yy_mm
    if (!(Test-Path -Path $folderPath)) {
        New-Item -ItemType Directory -Path $folderPath | Out-Null
    }

    # Membuat file dengan konten yang ditentukan
    $filePath = Join-Path -Path $folderPath -ChildPath $dd00
    if (!(Test-Path -Path $filePath)) { # Menghindari overwrite jika file sudah ada
        Set-Content -Path $filePath -Value $fileContent
        Write-Output "File $dd00 berhasil dibuat di folder $yy_mm."
    }

    # Melanjutkan ke hari berikutnya
    $today = $today.AddDays(1)
}
```

</details>

- itu scriptnya biar rapi juga aku simpen ke [sini](../Script/Create%20Diary%20Template.ps1)
- Aku dikasih kopi, terus kunci ruangannya aku yang pegang nanti aku yang balikin
- Aku lanjut edit beberapa hal di halosis, ada 207 artikel di kategori root, dipindahin 1 1 ke kategori SIS. Agak kesel sih soalnya gaada shortcutnya (atau aku gak nemu?), akua stopwatch ginian makan 30 menit hadeh...
  