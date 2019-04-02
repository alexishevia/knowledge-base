# The defer command
The `defer` command enables us to tell a function to run after we return from the current function.

By deferring a function early on, we can ensure that some functionality runs regardless of where in the function we return, as well as grouping logic together at the place where it makes sense.

```go
func CopyFile(dstName, srcName string) error {
	src, err := os.Open(srcName)
	if err != nil {
		return err
	}
	defer src.Close()

	dst, err := os.Open(dstName)
	if err != nil {
		return err
	}
	defer dst.Close()

	_, err := io.Copy(dst, src)
	return err
}
```
In this example, we open two different files so that we can copy from one to the other. By calling `defer src.Close()` after we open the source file, we’re saved from having to remember calling it before we return at the end of the function, or when we return if there’s an error opening the dst file.
