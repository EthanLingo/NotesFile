# Julia操作文件与文件夹

#内容/编程/Julia语言 

通过几个例子实例其操作文件夹、路径等方式。

## mkpath()、mkdir()等

mkpath(path::AbstractString; mode::Unsigned = 0o777)

Create all directories in the given `path`, with permissions `mode`. `mode` defaults to `0o777`, modified by the current file creation mask. Unlike `mkdir`, `mkpath` does not error if `path` (or parts of it) already exists. Return `path`.

**Examples**

```julia-repl
julia> mkdir("testingdir")  
"testingdir"  
  
julia> cd("testingdir")  
  
julia> pwd()  
"/home/JuliaUser/testingdir"  
  
julia> mkpath("my/test/dir")  
"my/test/dir"  
  
julia> readdir()  
1-element Array{String,1}:  
"my"  
  
julia> cd("my")  
  
julia> readdir()  
1-element Array{String,1}:  
"test"  
  
julia> readdir("test")  
1-element Array{String,1}:  
"dir"
```

## joinpath()等

[`Base.Filesystem.joinpath`](https://docs.juliacn.com/dev/base/file/#Base.Filesystem.joinpath)— Function

```julia
joinpath(parts::AbstractString...) -> String
joinpath(parts::Vector{AbstractString}) -> String
joinpath(parts::Tuple{AbstractString}) -> String
```

Join path components into a full path. If some argument is an absolute path or (on Windows) has a drive specification that doesn't match the drive computed for the join of the preceding paths, then prior components are dropped.

Note on Windows since there is a current directory for each drive, `joinpath("c:", "foo")` represents a path relative to the current directory on drive "c:" so this is equal to "c:foo", not "c:\foo". Furthermore, `joinpath`treats this as a non-absolute path and ignores the drive letter casing, hence `joinpath("C:\A","c:b") = "C:\A\b"`.

**Examples**

```julia-repl
julia> joinpath("/home/myuser", "example.jl")
"/home/myuser/example.jl"
```

```julia-repl
julia> joinpath(["/home/myuser", "example.jl"])
"/home/myuser/example.jl"
```


> 来源：[Julia官方文档之文件系统](https://docs.juliacn.com/dev/base/file/)