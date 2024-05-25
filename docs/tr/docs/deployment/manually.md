# Bir Sunucuyu El ile Çalıştırma

## `fastapi run` Komutunu Kullanın

Özetle FastAPI uygulamanızı sunmak için `fastapi run` kullanın:

<div class="termy">

```console
$ <font color="#4E9A06">fastapi</font> run <u style="text-decoration-style:single">main.py</u>
<font color="#3465A4">INFO    </font> Using path <font color="#3465A4">main.py</font>
<font color="#3465A4">INFO    </font> Resolved absolute path <font color="#75507B">/home/user/code/awesomeapp/</font><font color="#AD7FA8">main.py</font>
<font color="#3465A4">INFO    </font> Searching for package file structure from directories with <font color="#3465A4">__init__.py</font> files
<font color="#3465A4">INFO    </font> Importing from <font color="#75507B">/home/user/code/</font><font color="#AD7FA8">awesomeapp</font>

 ╭─ <font color="#8AE234"><b>Python module file</b></font> ─╮
 │                      │
 │  🐍 main.py          │
 │                      │
 ╰──────────────────────╯

<font color="#3465A4">INFO    </font> Importing module <font color="#4E9A06">main</font>
<font color="#3465A4">INFO    </font> Found importable FastAPI app

 ╭─ <font color="#8AE234"><b>Importable FastAPI app</b></font> ─╮
 │                          │
 │  <span style="background-color:#272822"><font color="#FF4689">from</font></span><span style="background-color:#272822"><font color="#F8F8F2"> main </font></span><span style="background-color:#272822"><font color="#FF4689">import</font></span><span style="background-color:#272822"><font color="#F8F8F2"> app</font></span><span style="background-color:#272822">  </span>  │
 │                          │
 ╰──────────────────────────╯

<font color="#3465A4">INFO    </font> Using import string <font color="#8AE234"><b>main:app</b></font>

 <font color="#4E9A06">╭─────────── FastAPI CLI - Production mode ───────────╮</font>
 <font color="#4E9A06">│                                                     │</font>
 <font color="#4E9A06">│  Serving at: http://0.0.0.0:8000                    │</font>
 <font color="#4E9A06">│                                                     │</font>
 <font color="#4E9A06">│  API docs: http://0.0.0.0:8000/docs                 │</font>
 <font color="#4E9A06">│                                                     │</font>
 <font color="#4E9A06">│  Running in production mode, for development use:   │</font>
 <font color="#4E9A06">│                                                     │</font>
 <font color="#4E9A06">│  </font><font color="#8AE234"><b>fastapi dev</b></font><font color="#4E9A06">                                        │</font>
 <font color="#4E9A06">│                                                     │</font>
 <font color="#4E9A06">╰─────────────────────────────────────────────────────╯</font>

<font color="#4E9A06">INFO</font>:     Started server process [<font color="#06989A">2306215</font>]
<font color="#4E9A06">INFO</font>:     Waiting for application startup.
<font color="#4E9A06">INFO</font>:     Application startup complete.
<font color="#4E9A06">INFO</font>:     Uvicorn running on <b>http://0.0.0.0:8000</b> (Press CTRL+C to quit)
```

</div>

Çoğu durumda bu komutu kullanabilirsiniz. 😎

Bu komutu FastAPI uygulamanızı bir konteynerde, bir sunucuda vb. başlatmak için kullanabilirsiniz.

## ASGI Sunucuları

Hadi detay denizinin biraz daha derinlerine inelim.

FastAPI, Python web çerçeveleri ve sunucuları oluşturmak için bir standart olan <abbr title="Asynchronous Server Gateway Interface">ASGI</abbr> standardını kullanır. FastAPI, bir ASGI web çerçevesidir.

Bir **FastAPI** uygulamasını (veya başka bir ASGI uygulamasını) uzak bir sunucuda çalıştırmak için ihtiyacınız olan en temel şey, `fastapi` komutuyla varsayılan olarak gelen **Uvicorn** gibi bir ASGI sunucu programıdır.

Birkaç alternatif bulunmaktadır, bunlar arasında:

* <a href="https://www.uvicorn.org/" class="external-link" target="_blank">Uvicorn</a>: yüksek performanslı bir ASGI sunucusu.
* <a href="https://pgjones.gitlab.io/hypercorn/" class="external-link" target="_blank">Hypercorn</a>: HTTP/2 ve Trio başta olmak üzere farklı özellikleri olan bir ASGI sunucusu.
* <a href="https://github.com/django/daphne" class="external-link" target="_blank">Daphne</a>: Django Channels için inşa edilmiş ASGI sunucusu.

## Sunucu Makinesi ve Sunucu Programı

İsimlerle ilgili küçük bir detayı aklınızda tutmanızda fayda var. 💡

**Sunucu** kelimesi genellikle hem uzak/bulut bilgisayar (fiziksel veya sanal makine) hem de o makinede çalışan program (örneğin Uvicorn) için kullanılır.

"Sunucu" kelimesiyle karşılaştığınızda, genellikle bu iki şeyden birine atıfta bulunulduğunu unutmayın.

Uzak makineden bahsederken genellikle **sunucu**, **makine**, **VM** (sanal makine), **düğüm** gibi ifadeler kullanılır. Bunlar genellikle Linux çalıştıran bir çeşit uzak makineye atıfta bulunur.

## Sunucu Programını Kurun

FastAPI'ı kurduğunuzda bir yayınlama sunucusu olan Uvicorn ile birlikte gelir ve `fastapi run` komutuyla çalıştırabilirsiniz.

Bununla birlikte bir ASGI sunucusunu manuel olarak da kurabilirsiniz:

=== "Uvicorn"

    * <a href="https://www.uvicorn.org/" class="external-link" target="_blank">Uvicorn</a>, uvloop ve httptools üzerine inşa edilmiş çok hızlı bir ASGI sunucusudur.

    <div class="termy">

    ```console
    $ pip install "uvicorn[standard]"

    ---> 100%
    ```

    </div>

    !!! tip "İpucu"
        `standard` etiketini kullandığınızda Uvicorn, bazı önerilen ek bağımlılıkları yükleyecek ve kullanacaktır.

        Bu `asyncio` için yüksek performanslı bir alternatif olan `uvloop`'u içerir, bu da büyük bir eş zamanlılık performans artışı sağlar.

        FastAPI'ı `pip install fastapi` gibi bir komut ile kurduğunuzda zaten `uvicorn[standard]`'ı da kurmuş olursunuz.

=== "Hypercorn"

    * <a href="https://gitlab.com/pgjones/hypercorn" class="external-link" target="_blank">Hypercorn</a>, HTTP/2 ile uyumlu bir ASGI sunucusudur.

    <div class="termy">

    ```console
    $ pip install hypercorn

    ---> 100%
    ```

    </div>

    ...veya başka bir ASGI sunucusu.

## Sunucu Programını Çalıştırma

Manuel olarak bir ASGI sunucusu kurduysanız, FastAPI uygulamanızı dahil etmek için özel bir formatta içe aktarma metini kullanmanız gerekir:

=== "Uvicorn"

    <div class="termy">

    ```console
    $ uvicorn main:app --host 0.0.0.0 --port 80

    <span style="color: green;">INFO</span>:     Uvicorn running on http://0.0.0.0:80 (Press CTRL+C to quit)
    ```

    </div>

=== "Hypercorn"

    <div class="termy">

    ```console
    $ hypercorn main:app --bind 0.0.0.0:80

    Running on 0.0.0.0:8080 over http (CTRL + C to quit)
    ```

    </div>

!!! note "Not"
    `uvicorn main:app` komutunu şu şekilde açıklayabiliriz:

    * `main`: dosya olan `main.py` (yani Python "modülü").
    * `app`: ise `main.py` dosyasının içerisinde `app = FastAPI()` satırında oluşturduğumuz `FastAPI` nesnesi.

    Aşağıdaki satıra eşdeğerdir:

    ```Python
    from main import app
    ```

!!! warning "Uyarı"
    Uvicorn ve diğerleri geliştirme sırasında kullanışlı olan bir `--reload` seçeneğini destekler.

    `--reload` seçeneği, daha fazla kaynak tüketir, daha kararsızdır, vb.

    **Geliştirme** sırasında çok yardımcı olur, ancak **yayınlama** sürecinde kullanmamalısınız.

## Trio ile Hypercorn

Starlette ve **FastAPI**, Python'un standart kütüphanesi olan <a href="https://docs.python.org/3/library/asyncio-task.html" class="external-link" target="_blank">asyncio</a> ve <a href="https://trio.readthedocs.io/en/stable/" class="external-link" target="_blank">Trio</a> ile uyumlu hale getiren <a href="https://anyio.readthedocs.io/en/stable/" class="external-link" target="_blank">AnyIO</a> üzerine kuruludur.

Yine de Uvicorn şu anda yalnızca asyncio ile uyumludur ve genellikle `asyncio` için yüksek performanslı bir alternatif olan <a href="https://github.com/MagicStack/uvloop" class="external-link" target="_blank">`uvloop`</a>'u kullanır.

Eğer doğrudan **Trio** kullanmak istiyorsanız, **Hypercorn**'u kullanabilirsiniz. ✨

### Trio ile Hypercorn Kurulumu

Öncelikle Hypercorn'u Trio desteğiyle kurmanız gerekmektedir:

<div class="termy">

```console
$ pip install "hypercorn[trio]"
---> 100%
```

</div>

### Trio ile Çalıştırma

`--worker-class` komut satırı seçeneğini `trio` değeriyle kullanabilirsiniz:

<div class="termy">

```console
$ hypercorn main:app --worker-class trio
```

</div>

Bu şekilde Hypercorn'u Trio ile kullanarak uygulamanızı çalıştırabilirsiniz. 🎉

Artık Trio'yu uygulamanızın içinde kullanabilirsiniz. Daha da iyisi, kodunuzu hem Trio hem de asyncio ile uyumlu tutmak için AnyIO'yu kullanabilirsiniz. 🎉

## Yayınlama Kavramları

Bu örnekler, **tek bir işlem** başlatan sunucu programını (örneğin Uvicorn) çalıştırır ve belirli bir bağlantı noktasında (örneğin `80`) tüm IP'leri (`0.0.0.0`) dinler.

Temel fikir bu. Ancak aşağıdakiler gibi ek şeylerle ilgilenmek isteyebilirsiniz:

* Güvenlik - HTTPS
* Başlangıçta çalıştırma
* Yeniden başlatma
* Yineleme (çalışan işlem sayısı)
* Bellek
* Çalıştırmadan önceki adımlar

İlerleyen bölümlerde, bu kavramların her biri hakkında daha fazla bilgi vereceğim, nasıl düşünülmesi gerektiği ve bunlarla başa çıkmak için stratejilerle ilgili bazı somut örnekler vereceğim. 🚀
