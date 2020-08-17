# Reading files and directories

Reading files/folders is quite simple. Here's a guide on how to do it.

## Reading files
This example shows how to read a file and print it to the console

```c++
#include <cstdio>
#include <libsystem/Result.h>
#include <libsystem/io/File.h>

int main()
{
    // Replace with the path you choose. eg. /System/Configs/open/file-extensions.json
    const char* file = "/at/some/path/file.txt";

    if (!file_exist(file))
    {
        printf("Cannot access file \"%s\". No such file", file);
        return -1;
    }
    
    // The size and buffer variables
    size_t size;
    void* buffer;
    
    Result file_result = file_read_all(file, &buffer, &size);
    if(file_result != SUCCESS)
    {
        printf("Error reading file \"%s\"", file);
        return -1;
    } else {
        // If file is ok, cast the buffer to a const char*
        const char* string = (const char*)buffer;
        printf("Contents of %s:\n%s", file, string);
    }
    // Don't forget to free the buffer
    free(buffer);


}
```

## Reading directories

This code will list the contents of a folder:
```c++
#include <cstdio>
#include <libsystem/io/Directory.h>

int main()
{
	const char* directory_path = "/System";

	Directory *directory = directory_open(directory_path, OPEN_READ);
	DirectoryEntry entry;

   	printf("Contents of %s:\n", directory_path);
	while (directory_read(directory, &entry) > 0)
	{
        printf("%s\n", entry.name);
    }
    return 0;
}
```
