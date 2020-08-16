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
    
    if (file_exist(file))
    {
        handle_printf_error(stream, "Cannot access file \"%s\"", file);
        return -1;
    }
    
    // You could also use the String datatype
    const char* data;
    
    FileState stat = {};
    stream_stat(stream, &stat);

    size_t read;
    // This a temporary buffer used by stream_read
    char buffer[1024];
    
    while ((read = stream_read(stream, &buffer, 1024)) != 0)
    {
        if (handle_has_error(stream))
        {
            handle_printf_error(stream, "Failled to read from %s", file);

            return -1;
        }

        stream_write(out_stream, buffer, read);

        if (handle_has_error(out_stream))
        {
            handle_printf_error(out_stream, "cat: Failled to write to stdout");

            return -1;
        }
    }
    
    // Don't forget to flush the stream
    stream_flush(out_stream);


}
