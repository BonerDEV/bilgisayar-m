# Bilgisayarım

Bilgisayar sağlığını kontrol etmek ve temel bilgisayar parçalarını tanımak için başlangıç rehberi. Komutlar Windows 10 ve Windows 11 içindir.

## Komutları çalıştırma

Başlat menüsünde **Terminal**, **PowerShell** veya **Komut İstemi** aratıp açın. Yönetici izni isteyen komutlar için Terminal'e sağ tıklayıp **Yönetici olarak çalıştır** seçeneğini kullanın. Komutları tek tek yazıp Enter'a basın.

## Bilgisayar sağlığı kontrolleri

### Sistem ve donanım bilgileri

Komut İstemi veya PowerShell'de:

```text
systeminfo
```

Windows sürümü, işlemci ve bellek gibi sistem bilgilerini listeler.

PowerShell'de işlemci bilgisi:

```powershell
Get-CimInstance Win32_Processor | Select-Object Name, NumberOfCores, NumberOfLogicalProcessors
```

Bellek modüllerini görmek için:

```powershell
Get-CimInstance Win32_PhysicalMemory | Select-Object Manufacturer, Capacity, Speed
```

`Capacity` bellek miktarını bayt cinsinden gösterir.

### Windows sistem dosyalarını denetleme

**Yönetici olarak açılmış** Terminal veya Komut İstemi'nde:

```text
sfc /scannow
```

Windows sistem dosyalarını tarar ve bulabildiği bozuk dosyaları onarmayı dener. Tarama tamamlanana kadar pencereyi kapatmayın.

SFC sorunu çözemiyorsa, yönetici PowerShell veya Komut İstemi'nde önce:

```text
DISM /Online /Cleanup-Image /RestoreHealth
```

İşlem tamamlandıktan sonra `sfc /scannow` komutunu yeniden çalıştırın. Bu işlemler zaman alabilir ve internet bağlantısı gerekebilir.

### Sürücü ve disk kontrolü

Komut İstemi veya Terminal'de:

```text
chkdsk C: /scan
```

Windows'un kurulu olduğu `C:` sürücüsünü çevrimiçi olarak denetler. Başka bir sürücüyü kontrol edecekseniz `C:` yerine o sürücünün harfini yazın.

PowerShell'de disklerin bildirdiği sağlık durumunu görmek için:

```powershell
Get-PhysicalDisk | Select-Object FriendlyName, MediaType, HealthStatus, OperationalStatus
```

Bu durum bilgisi bazı bilgisayarlarda veya disklerde sunulmayabilir; sonuç görünmemesi tek başına arıza olduğu anlamına gelmez.

### Açık programları ve işlemleri görme

Komut İstemi'nde:

```text
tasklist
```

Çalışan işlemleri listeler. PowerShell'de `Get-Process` komutu da çalışan işlemleri gösterir. Bir işlemi tanımadan kapatmayın.

## Temel bilgisayar parçaları

- **İşlemci (CPU):** Komutları işler ve programların çalışmasını sağlar.
- **Bellek (RAM):** Açık programların geçici çalışma alanıdır. Bilgisayar kapanınca içeriği silinir.
- **Depolama (SSD/HDD):** Windows, programlar ve dosyalar burada kalıcı olarak saklanır. SSD'ler genellikle HDD'lerden daha hızlıdır.
- **Anakart:** İşlemci, bellek ve diğer parçaların bağlandığı ana devre kartıdır.
- **Ekran kartı (GPU):** Görüntüyü oluşturur; oyun ve grafik işlemlerinde önemlidir. İşlemciye dahili olabilir veya ayrı bir kart olarak takılabilir.
- **Güç kaynağı:** Masaüstü bilgisayardaki parçalara elektrik sağlar.
- **Soğutma sistemi:** İşlemci ve diğer parçaların sıcaklığını kontrol altında tutar.

## Güvenlik notları

- Komutları yalnızca ne yaptığınızı anladığınızda çalıştırın. Bu rehberdeki komutlar bilgi toplama veya Windows tanılama/onarımı içindir.
- Yönetici iznini sadece ilgili Windows tarama ve onarım komutlarında kullanın.
- Disk hatası, aşırı ısınma veya tekrarlayan mavi ekran gibi sorunlar devam ederse önemli dosyalarınızı yedekleyin ve teknik destek alın.
