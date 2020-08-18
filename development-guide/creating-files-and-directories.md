# Creating files and directories

Creating files/folders is easy. Just follow the guide

## Writing to a file

This example writes some text to a file

```c++
#include <cstdio>
#include <cstring>
#include <libsystem/Result.h>
#include <libsystem/io/File.h>

int main()
{
    const char* file = "/User/Documents/file.txt";

    if (file_exist(file))
    {
        printf("File \"%s\" already exists!", file);
        return -1;
    }

    const char* string = "Hi there";
    size_t size = strlen(string);

    Result file_result = file_write_all(file, (void*)string, size);

    if(file_result != SUCCESS)
    {
        printf("Cannot write file \"%s\".", file);
        return -1;
    } else {
        printf("Succesfully wrote file to \"%s\"", file);
        return 0;
    }
}
```

## Creating a directory

The steps for creating a directory are very simple:

```
#include <cstdio>
#include <libsystem/io/Filesystem.h>

int main()
{
    if(filesystem_mkdir("directory") == 0)
    {
        printf("Created!");
        return 0;
    } else {
        printf("Failed to create directory");
        return -1;
    }
}
```
