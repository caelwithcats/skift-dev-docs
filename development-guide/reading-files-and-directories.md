# Reading files and directories

Reading files/folders is quite simple. Here's a guide on how to do it.

## Reading files
This example shows how to read a file and print it to the console

```c++
#include <libsystem/Result.h>
#include <libsystem/io/File.h>

int main()
{
    const char* file = "/at/some/path/file.txt";
    
    if (!file_exist(file))
    {
        printf("Cannot access file \"%s\". No such file", file);
        return -1;
    }
    
    // You could also use the String datatype
    const char* data;
    
    FileState stat = {};
    stream_stat(stream, &stat);

    size_t read;
    // The size and buffer variables are temporary used by the file_read_all function
    size_t size;
    void* buffer;
    
    Result file_result = file_read_all(file, &buffer, &size)
    if(file_result != SUCCESS)
    {
        printf("Error reading file \"%s\"", file);
        return -1;
    } else {
        // if file is ok
        
    }
    // Don't forget to free the buffer
    free(buffer);


}
