---
title: AutoMapper
date: 2018-11-08 11:08:28
categories:
- AutoMapper
tags:
- AutoMapper
- C#
---

# AutoMapper

> 兩個 class 要對映，可以使用linq來寫，但是當欄位一多的時候，就要寫的很多，這時候就可以使用 AutoMapper。

```code
private class MyClass
{
    public int A { get; set; }
    public int b { get; set; }
    public int c { get; set; }
    public int d { get; set; }
    public int e { get; set; }
    public int f { get; set; }
    public int g { get; set; }
    public int h { get; set; }
    public int i { get; set; }
    public int j { get; set; }
    public int k { get; set; }
    public int l { get; set; }
    public int hh { get; set; }
}

private class MyClass2
{
    public int A { get; set; }
    public int b { get; set; }
    public int c { get; set; }
    public int d { get; set; }
    public int e { get; set; }
    public int hh { get; set; }
}
```

## 使用 Linq

```code

List<MyClass2> data = my.Select(x => new MyClass2()
{
    A = x.A,
    b = x.b,
    c = x.c,
    d = x.d,
    e = x.e,
    hh = x.hh
}).ToList();
```

## 使用 AutoMapper 對映

```bash
Mapper.Initialize(cfg =>
{
    cfg.CreateMap<MyClass, MyClass2>();
});
List<MyClass2> data2 = Mapper.Map<List<MyClass2>>(my);

```

# 參考網址

* [Automapper官網](https://automapper.org/)
* [Automapper Github](https://github.com/AutoMapper/AutoMapper)