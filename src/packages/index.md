# Packages
Once the [Typst Universe](https://typst.app/universe) was launched, this chapter has become almost redundant. This is actually a very cool place to look for packages.

However, there are still some cool examples of interesting package usage.

## General
Typst has packages, but, unlike LaTeX, you need to remember:

- You need them only for some specialized tasks, basic formatting _can be totally done without them_.
- Packages are much lighter and much easier "installed" than LaTeX ones.
- Packages are just plain Typst files (and sometimes plugins), so you can easily write your own!

To use mighty package, just write, like this:
```typ
#import "@preview/cetz:0.1.2": canvas, plot

#canvas(length: 1cm, {
  plot.plot(size: (8, 6),
    x-tick-step: none,
    x-ticks: ((-calc.pi, $-pi$), (0, $0$), (calc.pi, $pi$)),
    y-tick-step: 1,
    {
      plot.add(
        style: plot.palette.blue,
        domain: (-calc.pi, calc.pi), x => calc.sin(x * 1rad))
      plot.add(
        hypograph: true,
        style: plot.palette.blue,
        domain: (-calc.pi, calc.pi), x => calc.cos(x * 1rad))
      plot.add(
        hypograph: true,
        style: plot.palette.blue,
        domain: (-calc.pi, calc.pi), x => calc.cos((x + calc.pi) * 1rad))
    })
})
```

## Contributing
If you are author of a package or just want to make a fair overview,
feel free to make issues/PR-s!
