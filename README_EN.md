<p align="center">
  <img src="https://github.com/jotavare/jotavare/blob/main/42/banners/piscine_and_common_core/github_piscine_and_common_core_banner_get_next_line.png">
</p>

<p align="center">
	<img src="https://img.shields.io/badge/status-finished-success?color=%2312bab9&style=flat-square" />
	<img src="https://img.shields.io/badge/evaluated-16%20%2F%2012%20%2F%202024-success?color=%2312bab9&style=flat-square" />
	<img src="https://img.shields.io/badge/score-125%20%2F%20100-success?color=%2312bab9&style=flat-square" />
	<a href='https://www.linkedin.com/in/kerem0zcn' target="_blank"><img alt='Linkedin' src='https://img.shields.io/badge/LinkedIn-100000?style=flat-square&logo=Linkedin&logoColor=white&labelColor=0A66C2&color=0A66C2'/></a>
</p>

## Project Description

The `get_next_line` project provides a C function that allows reading a file descriptor line by line. With bonus features, it also supports simultaneous reading from multiple file descriptors. This project is particularly useful when dealing with large files that need to be processed line by line.

## File Structure

- `get_next_line.c`: Contains the main implementation of the `get_next_line` function.
- `get_next_line_utils.c`: Contains helper functions required for the main implementation.
- `get_next_line_bonus.c`: An alternative implementation of `get_next_line` with bonus features.
- `get_next_line_utils_bonus.c`: Contains helper functions required for the bonus implementation.
- `get_next_line.h`: Includes function prototypes and macro definitions for the base implementation.
- `get_next_line_bonus.h`: Includes function prototypes and macro definitions for the bonus implementation.

## Usage

### Compilation

Use the following commands to compile the project:

#### For the Base Implementation:

```bash
gcc -Wall -Wextra -Werror -D BUFFER_SIZE=42 -c get_next_line.c get_next_line_utils.c
gcc -o gnl get_next_line.o get_next_line_utils.o
```

#### For the Bonus Features:

```bash
gcc -Wall -Wextra -Werror -D BUFFER_SIZE=42 -c get_next_line_bonus.c get_next_line_utils_bonus.c
gcc -o gnl_bonus get_next_line_bonus.o get_next_line_utils_bonus.o
```

The `BUFFER_SIZE` macro defines the number of bytes read per call to `read`. You can adjust this value according to your needs.

### Example Usage

Here is an example code snippet to read lines from a file:

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

The bonus features support reading from multiple file descriptors simultaneously. For this, you can make separate `get_next_line` calls for each file descriptor.

## Function Prototype

```c
char *get_next_line(int fd);
```

- `fd`: The file descriptor to read from.

**Return Value:**
- Returns the line read successfully.
- Returns `NULL` when the end of the file is reached or an error occurs.
