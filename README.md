Multiverse Logo
================

Just a project that generates the ‘miltiverse’ logo.

``` r
library(tidyverse)
library(rayrender)
set.seed(2019)

spheres <- expand.grid(y = (1:50) / 5 - 5, z = (1:50) / 5 - 5) %>%
  tibble::as_tibble()

noise <- ambient::noise_perlin(c(100, 100, 1))

depth <- purrr::map_dbl(
  1:nrow(spheres),
  function(idx) 20 * noise[floor(spheres$y[idx]*10+50), floor(spheres$z[idx]*10+50), 1])

sphere(material = metal(color="#AAAAFF", implicit_sample = T),
       y = spheres$y, z = spheres$z, x= depth, radius = 0.09) %>%
  render_scene(width = 4400, height = 2200, focal_distance = 2, aperture = 0.0001,
               lookfrom = c(3.25, 3.975, -2.01), lookat = c(-6,3.975,-2.01),
               filename = "multiverse.png")
```

``` html
<html>
    <head>
    </head>
    <body>
        <svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink"
             width="400" height="400" viewBox="20,-100,1732,2200" id="multiverse" xml:space="preserve">
            <clipPath id="area1">
                <polygon points="866,0 1732,500 1732,1500 866,2000 0,1500 0,500"></polygon>
            </clipPath>
            <polygon points="866,0 1732,500 1732,1500 866,2000 0,1500 0,500" stroke="#e8f2ff"
                     stroke-width="0" fill="#bec8ff">
            </polygon>
            <image xlink:href="multiverse.png"
                   x="-1100" y="220" height="2700" clip-path="url(#area1)" class="" width="5400">
            </image>
            <polygon points="866,0 1732,500 1732,1500 866,2000 0,1500 0,500" fill="transparent"
                     class="hex" stroke="#c3caff" stroke-width="80">
            </polygon>
            <text x="220" y="600" font-size="18em" font-family="sans-serif" fill="white" font-weight="200">multiverse</text>
            <text x="-200" y="2110" font-size="4em" font-family="sans-serif" fill="white" font-weight="500"
                  transform="rotate(-29.5)">www.rstudio.com</text>
        </svg>
        <a href="#" id="download">download</a>
        <script>
            var svg = document.getElementById("multiverse");

            var head = '<svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" ' +
                       'width="600" height="600" viewBox="-10,-10,320,320">';

            var source = '<?xml version="1.0" standalone="no"?>\r\n' + head + svg.innerHTML + "</svg>"
            var url = "data:image/svg+xml;charset=utf-8," + encodeURIComponent(source);

            document.getElementById("download").href = url;
        </script>
    </body>
</html>
```

![](multiverse-hex.svg)
