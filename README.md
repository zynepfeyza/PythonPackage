# Bir Python Uygulamasının Paket Haline Getirilmesi
Python projelerini paylaşmanın ve başkalarının bu projeleri kolayca yükleyip kullanmasının en iyi yolu bir paket oluşturmak ve dağıtmaktır.

## Python Paketi Nedir?
Belirli bir formatta sıkıştırılmış Python kodu demetleridir. Bu paketler, diğer insanlara dağıtılabilir ve pip gibi araçlarla kurulabilir.

https://packaging.python.org/en/latest/tutorials/packaging-projects/

Bir proje dosyası oluşturulur. Proje ana dizini içerisinde;
- src klasörünün altında, uygulamamızın kodlarını içeren bir klasör oluşturulur; bu klasörde boş bir `__init__.py` dosyası oluşturulur. Bu dosya Python’a bu dizinin bir paket olduğunu belirtir.
- Uygulamamızın testlerini içeren bir klasör oluşturulur.
- Proje ana dizini içerisinde `README.md`, `pyproject.toml` ve `LICENSE` dosyaları oluşturulur.
  - `README.md` : Projenin genel bilgilerini sağlayan bir belgedir.  
  - `pyproject.toml` : Proje yapılandırması ve bağımlılıklarını belirlemek için kullanılır.
  - `LICENSE` : Projenin lisansını belirtir. Lisans, kullanıcıların projeyi nasıl kullanabileceğini, değiştirebileceğini ve dağıtabileceğini tanımlar.
  

## Proje Yapısı
```sh
PythonPackage/
├── LICENSE
├── pyproject.toml
├── README.md
├── src/
│   └── my_package/
│       ├── __init__.py
│       └── main.py
└── tests/
```

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
Bu komut, dist/ dizininde paketleme dosyalarını oluşturur.
```sh
python3 -m build
```
Günümüzde iki ana Python paketi türü vardır:

1- Source Paketleri (.tar.gz): Kaynak kodun snapshot'ı ve ad, sürüm, özet, yazar gibi meta verileri içeren bir dosya içerir.

2- Wheel Paketleri (.whl): Egg formatının bir geliştirmesi olup, şu anda en çok önerilen formattır.

## Paketi Test Etme
Yeni bir projede paketin çalışıp çalışmadığını test etmek için paket yeni proje dizinine yüklenir.
```sh
pip install dist/my_package-0.0.1-py3-none-any.whl
pip install dist/my_package-0.0.1.tar.gz
```
Yeni bir Python dosyası oluşturulur ve test kodu yazılır. Eğer yine aynı çıktıyı alırsak, paket başarılı bir şekilde yüklenmiştir.
