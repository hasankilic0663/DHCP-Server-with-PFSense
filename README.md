![image](https://github.com/hasankilic0663/DHCP-Server-with-PFSense/assets/101570706/1b2d3813-fdc9-494f-9457-9269b37b3619)
### Projede Yapılacaklar

1)VirtualBox Sanallaştırma ortamı kuruldu.

2)1 Adet Fortigate veya Pfsense Firewall kuruldu.

3)1 adet Ubuntu Server kuruldu.

4)1 adet Windows 11 kuruldu.

5)1 adet Kali  kuruldu.

Proje amacımız sanal makinelerin firewall üzerinden birbirleriyle haberleşmesini sağlamak. Bunu iki şekilde deniyoruz. İlk olarak makinelere kendi static ip vererek haberleştirmek . Tabi her makinenin ip aralıkları farklı olup PfSense Firewall aracılığıyla Birbirlerine haber sağlamak. İkincisi ile DHCP ubuntu servera kurarak sanal makinelere otomatik ip ataması yapıyoruz. 
Proje Sunumu: Öncelikle Makinelerimizi virtual boxa kuruyoruz. Sonrasında PFSense Firewall makinesine Kendi Wan Kısmına Ellemeyip Lan segmentasyon  kısmını kendi vereceğimiz 10.10.10.2 yi atıyoruz terminalinden.
Ekstra olarakda Lan1 ve Lan2 olarakda ekleyip 20.20.20.2 ve 30.30.30.2 lanlarını atıyoruz. 
![image](https://github.com/hasankilic0663/DHCP-Server-with-PFSense/assets/101570706/a2a2024e-eccb-4e88-aa59-01cf4bbb35cd)

Makinelerle iletişime geçmesi içinde Ağ kısmına adaptörler atıyoruz. Bunun için ilk önce adaptör ekliyoruz Virtual Box'a herbirinin kendi aynı ipsinde veriyoruz. (10.10.10.1 20.20.20.1 30.30.30.1 )
![image](https://github.com/hasankilic0663/DHCP-Server-with-PFSense/assets/101570706/8360bc55-ac34-4ebe-8bef-a17ad9282773)
Ekledikten sonra PfSensin ilk kendi ağını NAT seçiyoruz. Diğre bağdaştırıcılarınıda sırasıyla adaptör 1-2-3 şeklinde ekliyoruz.
![image](https://github.com/hasankilic0663/DHCP-Server-with-PFSense/assets/101570706/5c92abeb-8d77-44cf-ba7e-7057d1ccd637)
Sonrasında da Makinelerimize tek tek girip Her birinde yine kendine özel Lan Segmentasyonunu atıyoruz. (10.10.10.3 20.20.20.3 30.30.30.3) ve gatewayleri ise pfsensin herbirinin kendi lan segmentasyonu olan ipler yazıyoruz .
![image](https://github.com/hasankilic0663/DHCP-Server-with-PFSense/assets/101570706/b3c5ced6-ce98-44c7-a439-b04c05121b50)

Sonrasındada normal sanal makineden girip PfSense arayüzüne bağlanıyoruz. Bağlandıktan sonrada PFSense arayüzünden policy kurucaz her bir lan segmentasyonuna :
![image](https://github.com/hasankilic0663/DHCP-Server-with-PFSense/assets/101570706/9dd0588d-814c-45c9-8362-052dd626c3f0)
ve bu durumda her bir makinenin Lan Segmentasyonu farklı olduğu halde Fırewall uzerınden bağlanarak birbirlerine ping atma işlemini sağlaık . 

### WAN (Geniş Alan Ağı):
WAN, "Wide Area Network" ifadesinin kısaltmasıdır ve genellikle büyük coğrafi alanlarda bulunan bilgisayarlar ve ağ cihazları arasında iletişimi sağlayan bir ağ türüdür. İnternet, dünya çapındaki en büyük WAN örneğidir. WAN'lar, şehirler, ülkeler veya hatta kıtalar arasındaki uzak noktalar arasında veri, ses ve video iletişimini sağlar. Genellikle çeşitli telekomünikasyon teknolojileri, özel hatlar veya uydu bağlantıları kullanılarak oluşturulur.

### LAN (Yerel Alan Ağı):
LAN, "Local Area Network" ifadesinin kısaltmasıdır ve sınırlı bir coğrafi alan içinde (örneğin bir binada veya bir kampüste) yer alan bilgisayarlar ve cihazlar arasında iletişimi sağlayan bir ağdır. LAN, yüksek hızlı veri transferi, dosya paylaşımı ve ortak kaynak kullanımı için kullanılır. Genellikle bir Ethernet kablosu, Wi-Fi veya başka bir yerel iletişim teknolojisi ile bağlanır.

### Switch (Anahtarlayıcı):
Switch, ağdaki bilgisayarlar ve cihazlar arasında veri iletişimini sağlayan bir ağ cihazıdır. Aynı LAN'daki birden fazla cihazı birbirine bağlar ve veri paketlerini doğrudan hedef cihaza ileterek verimli bir iletişim sağlar. Switch, veri hedefini belirleyen ve paketleri ilgili hedef cihaza yönlendiren özel bir ağ cihazıdır.

### Router (Yönlendirici):
Router, ağ trafiğini farklı ağlar arasında yönlendiren ve ileten bir ağ cihazıdır. LAN ile WAN arasındaki bağlantıyı sağlamak gibi farklı ağların birbiriyle iletişim kurmasını mümkün kılar. Router, alıcı ve gönderici arasında veri paketlerini en uygun yoldan ileterek ağ verimliliğini artırır.

### Gateway (Ağ Geçidi):
Gateway, farklı ağ protokollerini birbirine bağlayan ve farklı ağ tipleri arasında iletişimi sağlayan bir ağ cihazıdır. Genellikle LAN ve WAN arasında veya farklı ağ teknolojileri arasında veri dönüşümü yaparak uyumluluğu sağlar. İnternet erişiminde de genellikle bir ağ geçidi kullanılır.

### DHCP (Dynamic Host Configuration Protocol):
DHCP, IP (Internet Protocol) adresi, alt ağ maskesi, varsayılan ağ geçidi ve diğer ağ yapılandırma bilgilerini otomatik olarak bir ağ cihazına atayan bir ağ yönetim protokolüdür. Bu, yeni bir cihazın ağa bağlandığında otomatik olarak yapılandırılmasını sağlar ve ağ yöneticilerinin her cihazı manuel olarak yapılandırmak zorunda kalmadan ağda kolayca yeni cihazlar eklemesine olanak tanır.

### FTP (File Transfer Protocol):
FTP, dosyaların bir bilgisayardan başka bir bilgisayara aktarılması için kullanılan bir ağ protokolüdür. FTP, dosya paylaşımı, güncelleme ve indirme işlemlerini yönetmek için yaygın olarak kullanılır. Genellikle web siteleri, dosyalarını sunucuya yüklemek veya kullanıcılara dosya indirme imkanı vermek için FTP'yi kullanır.
