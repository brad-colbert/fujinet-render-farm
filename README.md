# fujinet-render-farm

Design documents and library code for a multi-machine "render farm" system for Atari 8-bit computers using the FujiNet network device

## Concept

First target use case is [Brooke Vibber's Atari Mandelbrot fractal renderer](https://brooke.vibber.net/git/brooke/mandel-6502/), which can take from a few minutes to a couple hours to render a complete image.

However this work is very parallelizable, and could be broken down by scanline or other grouping units and processed by multiple machines in parallel. Returned output and performance data could be sent back to the network, and then sent on to other machines in the group for display. Thus each connected machine would see the fractal rendering occur faster than any one machine could do it by itself.

The simplest user experience is to have each supported app automatically connect to an internet server, and make it straightforward to either start a new shared workset or join one in progress.

The plan is to:

* devise a user/worker data model suitable for needs, that's extensible to other similar programs
* devise a FujiNet-friendly API for connecting to the service, creating/joining worksets, and uploading/downloading data
* think a little bit about general abuse and junk cleanup needs: making things deletable/moderatable, blocking IP ranges
* devise an API for a library that can be linked in and called from C or assembly programs

## What lives where

* Design docs and library will live here in this repo: https://github.com/bvibber/fujinet-render-farm
* Mandelbrot app is on Brooke's forgejo: https://brooke.vibber.net/git/brooke/mandel-6502/
* prototype server may live separately

## Stretch goals

* a web interface that can view renderings in progress would be neat; this requires being able to describe the image or text data format to the web service for each connected app

## License

Provisionally selecting MIT-style license, see [LICENSE].
