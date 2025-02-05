MobInformation - Windows Terminal Yönetim ve Sistem İzleme Aracı
Proje Açıklaması
MobInformation, Windows işletim sistemleri üzerinde ağ bağlantılarını izlemek, sistem kaynaklarını (disk, CPU, RAM) takip etmek ve belirli terminal oturumlarını yönetmek için geliştirilmiş bir masaüstü uygulamasıdır. Bu uygulama, sistem kaynaklarını izleyip uyarılar gönderebilir ve ağda bulunan terminal oturumlarını sonlandırmak için gerekli işlemleri gerçekleştirebilir.

Proje, iki ana bileşenden oluşmaktadır:

Sistem İzleme ve Uyarı Modülü (C#)
Terminal Yönetimi ve Oturum Kapatma Modülü (.bat)
Projede Kullanılan Kütüphaneler ve Temel İşlevleri
System: Temel .NET sınıflarını içerir (veri türleri, istisnalar, matematik işlemleri vb.).
Kullanmış Olduğum Kütüphaneler
System.ComponentModel: Bileşenlerin ve kontrollerin özelliklerini yönetir.
System.Diagnostics: İşlem yönetimi ve hata ayıklama (örneğin Process.Start() ile program başlatma).
System.IO: Dosya okuma, yazma ve yönetme işlemleri.
System.Linq: LINQ sorguları ile koleksiyonları yönetme.
System.Threading: Çoklu iş parçacığı yönetimi.
System.Threading.Tasks: Asenkron programlama için görev yönetimi.
System.Data: Veritabanı işlemleri için temel sınıflar.
System.Data.SqlClient: SQL Server ile bağlantı kurma ve sorgular çalıştırma.
System.Net: Ağ bağlantıları ve veri aktarımı için sınıflar.
System.Net.Http: HTTP istekleri yapma (API çağrıları).
System.Net.NetworkInformation: Ağ bağlantı durumları hakkında bilgi alma.
System.Windows.Forms: Windows Forms uygulamalarındaki kontrolleri yönetme.
System.Drawing: Grafik çizim işlemleri (resimler, renkler, fırçalar vb.).
System.Security.Cryptography: Kriptografik işlemler (AES, SHA, RSA vb.).
Newtonsoft.Json: JSON verilerini serileştirme ve ayrıştırma.
Projede Kullanılan Temel Kodlar ve İşlevler
1. Performans Sayaçları
Performans sayaçları, sistem kaynaklarının kullanımını izler. Örnekler:

CPU Kullanımı: "Processor", "% Processor Time", "_Total"
RAM Kullanımı: "Memory", "% Committed Bytes In Use"
Disk Kullanımı: "PhysicalDisk", "Avg. Disk Queue Length", "_Total"
Bu sayaçlar, sistem performansı hakkında anlık veriler sağlar.

2. Sistem Kaynaklarının Gerçek Zamanlı İzlenmesi
GetCpuInfo(): CPU kullanımını alır, %80’i geçtiğinde uyarı gösterir.
GetMemoryInfo(): RAM kullanımını ölçer ve %80’i geçtiğinde uyarı verir.
GetDiskUsageInfo(): Disk kullanım oranını kontrol eder, %80’i aşarsa bildirim gönderir.
GetNetworkStatus(): Ağ bağlantısını kontrol eder ve durumunu gösterir.
3. Bildirim Gönderme ve Veri Tabanı Bağlantısı
Bu metot, veritabanında kayıtlı bir kullanıcının cihaz bilgilerini alarak mobil bildirim gönderir:

Veritabanına bağlanılır ve cihaz bilgileri alınır.
Bildirim nesnesi JSON formatında hazırlanır ve API’ye POST isteği ile gönderilir.
Veritabanı bağlantısı kapatılır.
4. Uzak Bilgisayarda Masaüstü Oturumu Sonlandırma (.bat)
.bat dosyası, PsExec aracı ile uzak masaüstü (RDP) oturumlarını sonlandırmak için kullanılır. Adımlar:

Adım 1: Sunucu ve kullanıcı bilgileri tanımlanır.
Adım 2: Kullanıcının oturumu kontrol edilir.
Adım 3: Oturum ID'si kullanılarak oturum kapatılır.
Adım 4: İşlem başarıyla tamamlanıp tamamlanmadığı kontrol edilir.
batch
Kopyala
Düzenle
set "server=111.111.1.11"
set "username=kullanici"
set "psexecPath=C:\Windows\System32\PsExec.exe"

For /f "tokens=3 %%A in ('%psexecPath% qwinsta ^| findstr /R /C:"%username%"') do (
    echo Oturum bulundu, ID: %%A
)

%psexecPath% \\%server% rwinsta %%A
5. .bat Dosyasını Çalıştırma
ExecuteBatFile metodu, .bat dosyasını çalıştırır ve hata kontrolü yapar.

csharp
Kopyala
Düzenle
private void ExecuteBatFile(string batFilePath)
{
    // CMD penceresini açar ve .bat dosyasını çalıştırır.
}
6. Gelişmiş .bat Çalıştırma (Progress Bar ile)
csharp
Kopyala
Düzenle
private async void ExecuteBatFileWithProgress(string batFilePath)
{
    // .bat dosyasının çalıştırılma ilerlemesi bir progress bar ile gösterilir.
}
7. AES ile Şifre Çözme (JSON’dan Kullanıcı Bilgilerini Okuma)
csharp
Kopyala
Düzenle
private string decryptData(string encryptedText)
{
    // AES CBC yöntemiyle şifreli veriyi çözer.
}
8. Buton İşlevi (Yetkilendirme ve .bat Çalıştırma)
csharp
Kopyala
Düzenle
private void button1_Click(object sender, EventArgs e)
{
    // Yetkilendirme kontrolü yapılır ve .bat dosyası çalıştırılır.
}
9. Yetkili Bilgisayar Listesi
csharp
Kopyala
Düzenle
List<string> authorizedMachines = new List<string> { "ITSTAJYERNEW", "PC2", "PC3" };
Yalnızca yetkili bilgisayarlar belirlenen işlemleri çalıştırabilir.

Sonuç
Bu sistem, güvenli, kontrol edilebilir ve yönetilebilir bir yapı sunar. .bat dosyasının çalıştırılması, AES şifre çözme, makine adı kontrolü ve işlem ilerlemesi ile tüm süreçler sağlıklı bir şekilde yönetilir.

