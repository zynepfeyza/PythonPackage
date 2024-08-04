## Python Paketi Nedir?
Belirli bir formatta sıkıştırılmış Python kodu demetleridir. Bu paketler, diğer insanlara dağıtılabilir ve pip gibi araçlarla kurulabilir.

https://packaging.python.org/en/latest/tutorials/packaging-projects/

## Örnek Paket Yapısı
```sh
my_package/
├── LICENSE
├── pyproject.toml
├── README.md
├── src/
│   └── my_package/
│       ├── __init__.py
│       └── example.py
│       └── sub_package/
│          ├── __init__.py
│          └── sub_module.py
├── tests/
│   ├── __init__.py
└── └── test_example.py
```
`my_package/`: Ana proje dizini.

`__init__.py`: Bu dosya Python’a bu dizinin bir paket olduğunu belirtir.

`example.py`: Paket içindeki bir modül.

`sub_package/`: Alt paket dizini.

`tests/`: Paketle ilgili testlerin bulunduğu dizin.

`test_example.py`: Modüle ait test dosyası.

`README.md`: Projenin genel bilgilerini sağlayan bir belgedir. 

`LICENSE`: Lisans bilgilerini içeren dosya. Lisans, kullanıcıların projeyi nasıl kullanabileceğini, değiştirebileceğini ve dağıtabileceğini tanımlar.

`pyproject.toml`: Proje yapılandırması ve bağımlılıklarını belirlemek için kullanılır.

  
## Bir Python Uygulamasının Paket Haline Getirilmesi
Python projelerini paylaşmanın ve başkalarının bu projeleri kolayca yükleyip kullanmasının en iyi yolu bir paket oluşturmak ve dağıtmaktır.

Öncelikle pip'in güncel olduğundan emin olmalıyız.
```sh
python3 -m pip install --upgrade pip
```

## Paketleme Araçlarını Kurma
Paketleme işlemi için `setuptools` ve `wheel` kurmamız gerek.
```sh
pip install setuptools wheel
```

## Paketi Oluşturma
build yüklü değilse
```sh
pip install build
```
Bu komut, dist/ dizininde paketleme dosyalarını oluşturur. Bu klasörde `.whl` ve `.tar.gz` gibi dosyalar bulunur.
Aynı zamanda bu komut ile `.egg-info` uzantılı bir dizin oluşur. Bu dizin paketleme ve dağıtım süreci için gerekli meta bilgileri içeren dosyaları içerir. Bu dosyalar:

`dependency_links.txt`: Paketin, yüklenmesi için gerekli olan diğer paketlerin bağlantılarını içerir.

`PKG-INFO`: Paket adı, versiyon, yazar, lisans gibi bilgileri içerir.

`SOURCES.txt`: Paketi oluşturmak için kullanılan tüm dosyaların bir listesidir.

`top_level.txt`: Paketin üst seviye modüllerini veya paketlerini listeler.
```sh
python3 -m build
```
- 1- Source Paketleri (.tar.gz): Paketin kaynak kodunu içeren bir sıkıştırılmış dosyadır. Kullanıcılar bu dosyayı indirip, açarak veya kurarak paketi yükleyebilirler.

- 2- Wheel Paketleri (.whl): Wheel dosyaları, pip gibi paket yönetim araçları tarafından kolayca kurulabilir. Wheel formatı, Python paketlerinin kurulum sürecini hızlandırır çünkü derleme gerektirmez; paketler doğrudan yüklenebilir.

.whl dosyasını ZIP dosyası olarak açabiliriz. İçerisinde:

`METADATA`: Paket bilgilerini içerir.

`WHEEL`: Wheel formatına özgü bilgiler içerir.

`RECORD`: 

`top_level.txt`: Paket içindeki üst seviye modülleri listeler.

`package_name`: Paket içindeki dosyalar ve modülleri içerir.
```sh
my_package-0.0.1-py3-none-any.whl
├── METADATA
├── WHEEL
├── RECORD
├── top_level.txt
└── my_package/
    ├── __init__.py
    └── main.py
```

## Paketi Test Etme
Yeni bir projede paketin çalışıp çalışmadığını test etmek için paket yeni proje dizinine yüklenir.
```sh
pip install dist/my_package-0.0.1-py3-none-any.whl
pip install dist/my_package-0.0.1.tar.gz
```
Yeni bir Python dosyası oluşturulur ve test kodu yazılır. Eğer yine aynı çıktıyı alırsak, paket başarılı bir şekilde yüklenmiştir.
