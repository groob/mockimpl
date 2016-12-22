`mockimpl` generates mock method stubs for implementing an interface.
mockimpl is based on [impl](github.com/josharian/impl)


```bash
go get -u github.com/groob/mockimpl
```

Sample usage:

```bash
$ impl 'f *File' io.ReadWriteCloser
// Automatically generated by mockimpl. DO NOT EDIT!

package mock

import "io"

var _ io.ReadWriteCloser = (*File)(nil)

type ReadFunc func(p []byte) (n int, err error)

type WriteFunc func(p []byte) (n int, err error)

type CloseFunc func() error

type File struct {
       	ReadFunc        ReadFunc
       	ReadFuncInvoked bool

       	WriteFunc        WriteFunc
       	WriteFuncInvoked bool

       	CloseFunc        CloseFunc
       	CloseFuncInvoked bool
}

func (f *File) Read(p []byte) (n int, err error) {
       	f.ReadFuncInvoked = true
       	return f.ReadFunc(p)
}

func (f *File) Write(p []byte) (n int, err error) {
       	f.WriteFuncInvoked = true
       	return f.WriteFunc(p)
}

func (f *File) Close() error {
       	f.CloseFuncInvoked = true
       	return f.CloseFunc()
}

# You can also provide a full name by specifying the package path.
# This helps in cases where the interface can't be guessed
# just from the package name and interface name.
$ impl 's *Source' golang.org/x/oauth2.TokenSource
func (s *Source) Token() (*oauth2.Token, error) {
    panic("not implemented")
}
```

You can use `impl` from Vim with [vim-go-impl](https://github.com/rhysd/vim-go-impl)
