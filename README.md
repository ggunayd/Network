# Network

![odev_topolojisi1](https://github.com/ggunayd/Network/assets/99563515/efdf29ba-2a4d-4293-b6b4-50c8ac4b049c)
-Bu topolojide bilgisayarların birbirleriyle iletişim halinde olmasını sağlayacağız.

![1 network](https://github.com/ggunayd/Network/assets/99563515/19471d9f-2ac6-433f-8f5f-97742f7e4628)
<br>
-10.0.101.0/24 networku için ip atamalarımızı yapıyoruz.
<br>
->Pc1:
<br>
  "ip 10.0.101.2/24 10.0.101.254"
  <br>
  "write memory"
  <br>
-Routerın 10.0.101.0/24 network portuna ip ataması yapıyoruz.
<br>
  "configure terminal"
  <br>
  "interface fastEthernet 0/0" -> (switchle routerı bağlayan interface'e gitmemiz gerekiyor.)
  <br>
  "ip address 10.0.101.254 255.255.255.0" -> (ip adresi ve subneti atıyoruz.)
  <br>
  "no shutdown" -> (portu aktif hale getiriyoruz)
  <br>
  "exit" -> (interfaceden çıkıyoruz yani bir önceki işlem kısmına geliyoruz. config-if modundan config moda geçmiş oluruz.)
  <br>
  "end" ve "write memory" -> (ana konsola geçiyoruz ve yaptığımız işlemleri hafızaya kaydediyoruz.)  
  <br>
  -Aynı işlemi bütün pcler ve routerlar için yaptıktan sonra aynı network içinde cihazlar varsa birbirleriyle haberleşebilir.
Cihazlar farklı networkler içerisindeyse; örneğin Pc1'den çıkan paket routera kadar yolunu takip edebilir ama routerdan sonra
yönünü bulamaz ve haberleşemezler.Bunun için static route işlemini yapmalıyız.
<br>
<br>

![r1](https://github.com/ggunayd/Network/assets/99563515/b0314764-1a28-4b0e-9a76-9ed66b558ac1)
<br>
![r5](https://github.com/ggunayd/Network/assets/99563515/349ec5e6-2c08-49a9-9ecb-ca9a090f6787)

<br>
  -Pc1'in Pc6 ile haberleşmesini sağlayacağız.
  <br>
  -Birbirlerine bağlı routerların haberleşebilmesi için aynı networkde olması ve farklı ip adreslerine sahip olması gerekiyor. Bizim topolojimizdeki gibi iki routerı bağlayan başka bir router varsa bir cihazdan
  başka bir cihaza ulaşmak için yolu takip ederek tüm routerlar için karşılıklı ip route işlemi yapmamız gerekiyor.
  <br>
  -> R1 ve R3 arasındaki static route;
  <br>
  -Öncelikle routelarımıza ip atamasını yapıyoruz.
  <br>
  ![r1_00](https://github.com/ggunayd/Network/assets/99563515/85ea1485-00cb-4a8b-8b51-dacaaf62be60)
  <br>
  -Port bilgilerimize bakıyoruz. R1'in iç bacağı için fastEthernet 0/0 portuna ip ataması yapacağız.
  <br>
   "interface fastEthernet 0/0"
  <br>
  "ip address 10.0.101.254 255.255.255.0"
  <br>
  ![01portu](https://github.com/ggunayd/Network/assets/99563515/ca519610-6209-4bbd-be64-c4a4740295a6)
  <br>
  -Port bilgilerimize bakıyoruz. R1'in dış bacağı için fastEthernet 0/1 portuna ip ataması yapacağız.
  <br>
  "interface fastEthernet 0/1"
  <br>
  "ip address 10.0.105.2 255.255.255.0"
  <br>
  ![00portu](https://github.com/ggunayd/Network/assets/99563515/3c2c4b73-f9eb-4867-a5f9-c9fac4d92716)
  <br>
  -Port bilgilerimize bakıyoruz. R3 fastEthernet 0/0 portuna ip ataması yapacağız.
  <br>
  "interface fastEthernet 0/0"
  <br>
  "ip address 10.0.105.254 255.255.255.0"
  <br>
  <br>
  -Ip atamalarımızı yaptık.Şimdi R1 ve R3 arasındaki static route işlemimizi yapabiliriz.
  <br>
  ip route -> hedef network id / subnetmask / gateway (ip route'u bu şekilde vermemiz gerekiyor.)
  <br>
  -Yani R1 için ip route;
  <br>
  "ip route 172.16.30.0 255.255.255.0 10.0.105.254" (R1'den R3'e ip route yazarken R3'ün 2/0 interface'indeki network id'siniz baz alıyoruz.)
  <br>
  R3 için ip route;
  <br>
  "ip route 10.0.101.0 255.255.255.0 10.0.105.2" 
  <br>
  "ip route 10.0.100.0 255.255.255.0 10.0.105.2" (R3'den R1'e ip route yazarken R1'e bağlı 2 network ağı oluduğu için ikisi için de ip route işlemini yapıyoruz.)
  <br>
  ![pc1ping](https://github.com/ggunayd/Network/assets/99563515/fecd05a9-9afe-4025-aa3e-1e97cc648cdf)
  -Şu anda Pc1'den R3'e ulaşabiliyoruz. 
  <br>
  -Aynı işlemleri R1 ve R3 arasında da uyguluyoruz ve Pc6dan R3'e ulaşacak konuma geliyoruz. Daha sonra Pc1 ve Pc6 cihazlarımızın haberleşebilmesi için R1 ve R5 arasında static route 
  işlemimizi yapıyoruz.
  <br>
  -R1'den R5'e ip route;
  <br>
  "ip route 172.16.40.0 255.255.255.0 172.16.30.1"
  <br>
  -R5'den R1'e ip route;
  <br>
  "ip route 10.0.101.0 255.255.255.0 10.0.105.2"
  <br>
  "ip route 10.0.100.0 255.255.0 10.0.105.2"
  <br>
  -Tüm işlemleri tamamladıktan sonra sorunsuz bir şekilde Pc1'den Pc6'ya ulaşabiliyoruz.
  <br>
  ![ping](https://github.com/ggunayd/Network/assets/99563515/f6f6c27b-b26a-47f9-888c-f3b4d3184f1f)
  <br>
  -Tüm cihazların haberleşmesi için bu işlemleri sırasıyla uyguluyoruz ve cihazlarımızın birbirleriyle iletişim halinde olmasını sağlıyoruz.
  
  
  
  
  
  
  
  
  
