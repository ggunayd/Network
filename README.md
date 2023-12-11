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
  "interface fastEthernet 0/0" -> (switchle routerı bağlayan interface'e gitmemiz gerekiyor.)
  <br>
  "ip address 10.0.101.254 255.255.255.0" -> (ip adresi ve subneti atıyoruz.)
  <br>
  "no shutdown" -> (portu aktif hale getiriyoruz)
  <br>
  "exit" -> (interfaceden çıkıyoruz.)
  <br>
  "end" ve "write memory" -> (ana konsola geçiyoruz ve yaptığımız işlemleri hafızaya kaydediyoruz.)  
  <br>
  -Aynı işlemi bütün pcler ve routerlar için yaptıktan sonra aynı network içinde cihazlar varsa birbirleriyle haberleşebilir.
Cihazlar farklı networkler içerisindeyse; örneğin Pc1'den çıkan paket routera kadar yolunu takip edebilir ama routerdan sonra
yönünü bulamaz ve haberleşemezler.Bunun için static route işlemini yapmalıyız.
<br>
<br>

![router](https://github.com/ggunayd/Network/assets/99563515/12d6efe2-03ea-445b-905b-22471742dea3)
<br>

  -Birbirlerine bağlı routerların haberleşebilmesi için aynı networkde olması ve farklı ip adreslerine sahip olması gerekiyor.
-> R1 ve R3 arasındaki static route;
