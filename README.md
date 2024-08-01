# 2048 Oyunu

Bu proje, popüler 2048 oyununu `tkinter` kütüphanesi ile oluşturulmuş bir Python uygulamasıdır. Oyunu terminalden çalıştırarak oynayabilirsiniz.

## Kurulum

1. Bu projeyi klonlayın veya indirin.
    ```bash
    git clone https://github.com/staboma/2048-oyunu.git
    cd 2048-oyunu
    ```

2. Gerekli bağımlılıkları yükleyin. Bu oyun sadece standart `tkinter` kütüphanesini kullandığından, ek bir bağımlılık gerektirmez. Python'un 3.x sürümünü kullanmanız yeterlidir.

## Kullanım

1. `2048.py` dosyasını çalıştırarak oyunu başlatın.
    ```bash
    python 2048.py
    ```

2. Oyun başladığında, ok tuşlarını veya `W`, `A`, `S`, `D` tuşlarını kullanarak sayıları birleştirin ve 2048 sayısına ulaşmaya çalışın.

## Oyun Kuralları

- Aynı sayıları birleştirerek 2048 sayısına ulaşmaya çalışın.
- Tahta üzerinde hareket etmek için `W` (yukarı), `A` (sol), `S` (aşağı) ve `D` (sağ) tuşlarını kullanın.
- Her hareketten sonra rastgele bir boş hücreye 2 veya 4 sayısı eklenir.
- Hareket edecek boş hücre kalmadığında oyun sona erer.

