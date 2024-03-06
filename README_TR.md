![tea](https://tea.xyz/banner.png)

The tea white paper [LaTeX] olarak gömülü matematiksel temsillere sahip, [anlamsal olarak sürümlendirilmiş][semver], bir [Markdown] belgesidir.
Yeni sürümler [GitHub'da][releases] yayınlanmadan önce `.pdf` olarak [Pandoc] ile derlenmektedir.

# tea/white-paper 1.0.5

## Katkı

Genel geri bildiriminiz varsa lütfen bir tartışma([discussion])  konusu açın.

Düzenlemeleriniz varsa lütfen proje çapındaki [katkı yönergelerimize] bakın. Daha sonra aşağıdakilerden birini yapabilirsiniz:

1. [`white-paper.md`] GitHub üzerinde hemen burada düzenleyebilirsiniz.
   Pull Request isteğinizi gönderdiğinizde CL pdf dosyasını PR'ye ekleyecektir.
2. Veya teknik incelemeyi kendi bilgisayarınızda oluşturabilirsiniz:

    ```sh
    make   #=> ./tea.white-paper.pdf
    ```

## Ön Gereklilikler

Bunları kendiniz temin edin veya tea kullanın: `sh <(curl tea.xyz)`.

| Proje             | Versiyon |
|---------------------|---------|
| pandoc.org          | ^2.18   |
| pandoc.org/crossref | ^0.3    |
| gnome.org/librsvg   | ^2.54   |
| gnu.org/make        | ^4      |


## Çeviri

Tea.xyz'de tüm çevirilerin tam PDF'lerini oluşturuyor, yayınlıyor ve sunuyoruz.

1. [Fork `teaxyz/white-paper`][fork]
2. Sonra terminalinizde:
    ```sh
    $ export LANG=…          # https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes
    $ export USER=…          # your github
    $ export VERSION=$(git describe --abbrev=0) # latest version tag  
    $ git clone https://github.com/${USER}/white-paper tea-white-paper
    …
    $ cd tea-white-paper
    $ git checkout -b i18n/${LANG} ${VERSION}
    …
    $ mkdir -p i18n/${LANG}
    $ cp white-paper.md metadata.yml i18n/${LANG}
    ```
3. Çevirnek `./i18n/${LANG}/metadata.yml`
4. Eklmek `./i18n/${LANG}/metadata.yml` append:
    ```yml
    lang: …       # https://pandoc.org/MANUAL.html#language-variables
    dir: ltr      # language direction; ltr:left-to-right or rtl:right-to-left
    header-includes:
      - \fancyfoot[L]{${VERSION}+${LANG}}   # expand these variables!
    translator:
      - Your Fullname
    ```

    ⚠️ Yalnızca Çince, Japonca ve Korece dilleri. Lütfen aşağıdakileri de ekleyin `metadata.yml`:
    ```yml
    header-includes:
      - \usepackage{xeCJK}
      - \setCJKmainfont{Noto Serif CJK XX} # where XX can be SC, TC, HK, JP, KR https://github.com/googlefonts/noto-cjk
    ```
5. Çevirmek `./i18n/${LANG}/white-paper.md`
6. Çeviriyi git'e kaydedin ve GitHub'a aktarın:
   ```sh
   git add i18n/${LANG}/*
   git commit -m "add ${LANG} translation"
   git push origin i18n/${LANG}
   ```
7. Bir Pull Request isteği oluşturun:
   ```sh
   open https://github.com/teaxyz/white-paper/compare/main...${USER}:white-paper:i18n/${LANG}
   ```

8. (Opsiyonel) Çalışmanızı önizleyin:
   ```sh
   make tea.white-paper_${LANG}.pdf
   ```

## Bakım

### Sürümü Ayarla

```sh
echo "- \fancyfoot[L]{$1}" >> metadata.yml
```

[`white-paper.md`]: ./white-paper.md
[Pandoc]: https://pandoc.org
[Markdown]: https://daringfireball.net/projects/markdown/
[LaTeX]: https://latex-project.org/
[releases]: ../../releases
[brew]: https://brew.sh
[semver]: https://semver.org
[discussion]: ../../discussions
[fork]: ../../fork
[contribution guidelines]: https://github.com/teaxyz/.github/blob/main/CONTRIBUTING.md
