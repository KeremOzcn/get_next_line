<p align="center">
  <img src="https://github.com/jotavare/jotavare/blob/main/42/banners/piscine_and_common_core/github_piscine_and_common_core_banner_get_next_line.png">
</p>

<p align="center">
	<img src="https://img.shields.io/badge/status-finished-success?color=%2312bab9&style=flat-square" />
	<img src="https://img.shields.io/badge/evaluated-16%20%2F%2012%20%2F%202024-success?color=%2312bab9&style=flat-square" />
	<img src="https://img.shields.io/badge/score-125%20%2F%20100-success?color=%2312bab9&style=flat-square" />
	<a href='https://www.linkedin.com/in/kerem0zcn' target="_blank"><img alt='Linkedin' src='https://img.shields.io/badge/LinkedIn-100000?style=flat-square&logo=Linkedin&logoColor=white&labelColor=0A66C2&color=0A66C2'/></a>
</p>

## Proje Açıklaması

`get_next_line` projesi, bir dosya tanımlayıcısından satır satır veri okumayı sağlayan bir C fonksiyonudur. Bonus özellikleri ile birden fazla dosya tanımlayıcısından eş zamanlı olarak okuma işlemi de desteklenir. Bu proje, özellikle büyük dosyaların satır bazında işlenmesi gereken durumlarda kullanışlıdır.

[Click here for the English version](README_EN.md)

## Dosya Yapısı

- `get_next_line.c`: `get_next_line` fonksiyonunun temel implementasyonunu içerir.
- `get_next_line_utils.c`: Yardımcı fonksiyonların implementasyonlarını içerir.
- `get_next_line_bonus.c`: Bonus özellikleri sağlayan alternatif `get_next_line` fonksiyonu.
- `get_next_line_utils_bonus.c`: Bonus özellikler için gerekli yardımcı fonksiyonlar.
- `get_next_line.h`: Temel fonksiyon prototiplerini ve makro tanımlamalarını içerir.
- `get_next_line_bonus.h`: Bonus fonksiyon prototiplerini ve makro tanımlamalarını içerir.

## Kullanım

### Derleme

Projeyi derlemek için aşağıdaki komutları kullanabilirsiniz:

#### Temel Fonksiyonlar İçin:

```bash
gcc -Wall -Wextra -Werror -D BUFFER_SIZE=42 -c get_next_line.c get_next_line_utils.c
gcc -o gnl get_next_line.o get_next_line_utils.o
```

#### Bonus Özellikler İçin:

```bash
gcc -Wall -Wextra -Werror -D BUFFER_SIZE=42 -c get_next_line_bonus.c get_next_line_utils_bonus.c
gcc -o gnl_bonus get_next_line_bonus.o get_next_line_utils_bonus.o
```

`BUFFER_SIZE` makrosu, `read` fonksiyonunun her çağrılışında okunacak bayt sayısını belirler. Bu değeri ihtiyaçlarınıza göre değiştirebilirsiniz.

### Kullanım Örneği

Bir dosyadan satır okumak için aşağıdaki kod örneğini kullanabilirsiniz:

```c
#include "get_next_line.h"
#include <fcntl.h>
#include <stdio.h>

int main(void)
{
    int fd = open("example.txt", O_RDONLY);
    if (fd == -1)
    {
        perror("Error opening file");
        return (1);
    }

    char *line;
    while ((line = get_next_line(fd)) != NULL)
    {
        printf("%s", line);
        free(line);
    }

    close(fd);
    return (0);
}
```

Bonus özellikler, birden fazla dosya tanımlayıcısından aynı anda satır okuma işlemini destekler. Bu özelliği kullanırken, her dosya tanımlayıcı için ayrı bir `get_next_line` çağrısı yapılabilir.

## Fonksiyon Prototipi

```c
char *get_next_line(int fd);
```


- `fd`: Okuma yapılacak dosya tanımlayıcısı.

**Dönüş Değeri:**
- Başarıyla okunan satırı döner.
- Dosya sonuna ulaşıldığında veya bir hata oluştuğunda `NULL` döner.
