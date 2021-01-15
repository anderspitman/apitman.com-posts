My personal cURL cheat sheet

# Downloading files

## Resuming failed download

Need to make sure filename is the same in order for it to automatically determine the offset. The `-`
after `-C` tells it to use the output file to determine where to continue from.

```bash
curl -O -C - https://example.com/dir/filename.bin
```

## Output filename

`-O` uses the filename from the end of the path. 

```bash
curl -O https://example.com/dir/filename.bin
```

This can be annoying if it has query parameters, because they will end up in the filename.
If you add `-J` it lets curl use the filename provided by the server (via the `Content-Disposition`
header) if one is available.

```bash
curl -OJ https://example.com/dir/filename.bin?param=value
```

# Uploading files

Prefer `--data-binary` to `--data/-d` because it doesn't mess with newlines etc.

```bash
curl https://example.com/dir/filename.bin --data-binary @filename.bin
```

`-T` option will make a PUT request. Advantage over `--data-binary` is that it doesn't load the entire
file into memory on the client. You can use `-X POST` to force it to use POST.

```bash
curl https://example.com/dir/ -T filename.bin
```