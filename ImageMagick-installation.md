# Installation Log of ImageMagick

ImageMagick က ပုံဖိုင်တွေကို အမျိုးမျိုးပြုပြင်ပြောင်းလဲဖို့အတွက် အင်မတန် အသုံးဝင်တဲ့ tool ပါ။  
Installation log ကို reference အဖြစ် တင်ထားတာ။  

## wget

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool$ wget https://www.imagemagick.org/download/ImageMagick.tar.gz
--2021-01-30 04:32:08--  https://www.imagemagick.org/download/ImageMagick.tar.gz
Resolving www.imagemagick.org (www.imagemagick.org)... 44.234.227.205
Connecting to www.imagemagick.org (www.imagemagick.org)|44.234.227.205|:443... connected.
HTTP request sent, awaiting response... 302 Found
Location: https://download.imagemagick.org/ImageMagick/download/ImageMagick.tar.gz [following]
--2021-01-30 04:32:09--  https://download.imagemagick.org/ImageMagick/download/ImageMagick.tar.gz
Resolving download.imagemagick.org (download.imagemagick.org)... 50.251.58.9
Connecting to download.imagemagick.org (download.imagemagick.org)|50.251.58.9|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 14789095 (14M) [application/x-gzip]
Saving to: ‘ImageMagick.tar.gz’

ImageMagick.tar.gz                            100%[================================================================================================>]  14.10M   484KB/s    in 29s     

2021-01-30 04:32:40 (496 KB/s) - ‘ImageMagick.tar.gz’ saved [14789095/14789095]
```

## tar xzvf

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool$ tar xzvf ./ImageMagick.tar.gz 
ImageMagick-7.0.10-60/
ImageMagick-7.0.10-60/coders/
ImageMagick-7.0.10-60/coders/aai.h
ImageMagick-7.0.10-60/coders/art.h
ImageMagick-7.0.10-60/coders/ashlar.h
ImageMagick-7.0.10-60/coders/avs.h
ImageMagick-7.0.10-60/coders/bgr.h
ImageMagick-7.0.10-60/coders/bmp.h
ImageMagick-7.0.10-60/coders/braille.h
ImageMagick-7.0.10-60/coders/bytebuffer-private.h
ImageMagick-7.0.10-60/coders/cals.h
ImageMagick-7.0.10-60/coders/caption.h
ImageMagick-7.0.10-60/coders/cin.h
ImageMagick-7.0.10-60/coders/cip.h
ImageMagick-7.0.10-60/coders/clipboard.h
ImageMagick-7.0.10-60/coders/clip.h
ImageMagick-7.0.10-60/coders/cmyk.h
ImageMagick-7.0.10-60/coders/coders.h
ImageMagick-7.0.10-60/coders/coders-list.h
ImageMagick-7.0.10-60/coders/coders-private.h
ImageMagick-7.0.10-60/coders/cube.h
ImageMagick-7.0.10-60/coders/cut.h
ImageMagick-7.0.10-60/coders/dcm.h
ImageMagick-7.0.10-60/coders/dds.h
ImageMagick-7.0.10-60/coders/debug.h
ImageMagick-7.0.10-60/coders/dib.h
ImageMagick-7.0.10-60/coders/djvu.h
ImageMagick-7.0.10-60/coders/dng.h
ImageMagick-7.0.10-60/coders/dot.h
ImageMagick-7.0.10-60/coders/dps.h
ImageMagick-7.0.10-60/coders/dpx.h
ImageMagick-7.0.10-60/coders/emf.h
ImageMagick-7.0.10-60/coders/ept.h
ImageMagick-7.0.10-60/coders/exr.h
ImageMagick-7.0.10-60/coders/farbfeld.h
ImageMagick-7.0.10-60/coders/fax.h
ImageMagick-7.0.10-60/coders/fits.h
ImageMagick-7.0.10-60/coders/fl32.h
ImageMagick-7.0.10-60/coders/flif.h
ImageMagick-7.0.10-60/coders/fpx.h
ImageMagick-7.0.10-60/coders/ghostscript-private.h
ImageMagick-7.0.10-60/coders/gif.h
ImageMagick-7.0.10-60/coders/gradient.h
ImageMagick-7.0.10-60/coders/gray.h
ImageMagick-7.0.10-60/coders/hald.h
ImageMagick-7.0.10-60/coders/hdr.h
ImageMagick-7.0.10-60/coders/heic.h
ImageMagick-7.0.10-60/coders/histogram.h
ImageMagick-7.0.10-60/coders/hrz.h
ImageMagick-7.0.10-60/coders/html.h
ImageMagick-7.0.10-60/coders/icon.h
ImageMagick-7.0.10-60/coders/info.h
ImageMagick-7.0.10-60/coders/inline.h
ImageMagick-7.0.10-60/coders/ipl.h
ImageMagick-7.0.10-60/coders/jbig.h
ImageMagick-7.0.10-60/coders/jnx.h
ImageMagick-7.0.10-60/coders/jp2.h
ImageMagick-7.0.10-60/coders/jpeg.h
ImageMagick-7.0.10-60/coders/json.h
ImageMagick-7.0.10-60/coders/jxl.h
ImageMagick-7.0.10-60/coders/kernel.h
ImageMagick-7.0.10-60/coders/label.h
ImageMagick-7.0.10-60/coders/mac.h
ImageMagick-7.0.10-60/coders/magick.h
ImageMagick-7.0.10-60/coders/map.h
ImageMagick-7.0.10-60/coders/mask.h
ImageMagick-7.0.10-60/coders/mat.h
ImageMagick-7.0.10-60/coders/matte.h
ImageMagick-7.0.10-60/coders/meta.h
ImageMagick-7.0.10-60/coders/miff.h
ImageMagick-7.0.10-60/coders/mono.h
ImageMagick-7.0.10-60/coders/mpc.h
ImageMagick-7.0.10-60/coders/mpr.h
ImageMagick-7.0.10-60/coders/msl.h
ImageMagick-7.0.10-60/coders/mtv.h
ImageMagick-7.0.10-60/coders/mvg.h
ImageMagick-7.0.10-60/coders/null.h
ImageMagick-7.0.10-60/coders/ora.h
ImageMagick-7.0.10-60/coders/otb.h
ImageMagick-7.0.10-60/coders/palm.h
ImageMagick-7.0.10-60/coders/pango.h
ImageMagick-7.0.10-60/coders/pattern.h
ImageMagick-7.0.10-60/coders/pcd.h
ImageMagick-7.0.10-60/coders/pcl.h
ImageMagick-7.0.10-60/coders/pcx.h
ImageMagick-7.0.10-60/coders/pdb.h
ImageMagick-7.0.10-60/coders/pdf.h
ImageMagick-7.0.10-60/coders/pes.h
ImageMagick-7.0.10-60/coders/pgx.h
ImageMagick-7.0.10-60/coders/pict.h
ImageMagick-7.0.10-60/coders/pix.h
ImageMagick-7.0.10-60/coders/plasma.h
ImageMagick-7.0.10-60/coders/png.h
ImageMagick-7.0.10-60/coders/pnm.h
ImageMagick-7.0.10-60/coders/ps2.h
ImageMagick-7.0.10-60/coders/ps3.h
ImageMagick-7.0.10-60/coders/psd.h
ImageMagick-7.0.10-60/coders/psd-private.h
ImageMagick-7.0.10-60/coders/ps.h
ImageMagick-7.0.10-60/coders/pwp.h
ImageMagick-7.0.10-60/coders/raw.h
ImageMagick-7.0.10-60/coders/rgb.h
ImageMagick-7.0.10-60/coders/rgf.h
ImageMagick-7.0.10-60/coders/rla.h
ImageMagick-7.0.10-60/coders/rle.h
ImageMagick-7.0.10-60/coders/screenshot.h
ImageMagick-7.0.10-60/coders/scr.h
ImageMagick-7.0.10-60/coders/sct.h
ImageMagick-7.0.10-60/coders/sfw.h
ImageMagick-7.0.10-60/coders/sgi.h
ImageMagick-7.0.10-60/coders/sixel.h
ImageMagick-7.0.10-60/coders/stegano.h
ImageMagick-7.0.10-60/coders/sun.h
ImageMagick-7.0.10-60/coders/svg.h
ImageMagick-7.0.10-60/coders/tga.h
ImageMagick-7.0.10-60/coders/thumbnail.h
ImageMagick-7.0.10-60/coders/tiff.h
ImageMagick-7.0.10-60/coders/tile.h
ImageMagick-7.0.10-60/coders/tim.h
ImageMagick-7.0.10-60/coders/tim2.h
ImageMagick-7.0.10-60/coders/ttf.h
ImageMagick-7.0.10-60/coders/txt.h
ImageMagick-7.0.10-60/coders/uil.h
ImageMagick-7.0.10-60/coders/url.h
ImageMagick-7.0.10-60/coders/uyvy.h
ImageMagick-7.0.10-60/coders/vicar.h
ImageMagick-7.0.10-60/coders/vid.h
ImageMagick-7.0.10-60/coders/video.h
ImageMagick-7.0.10-60/coders/viff.h
ImageMagick-7.0.10-60/coders/vips.h
ImageMagick-7.0.10-60/coders/wbmp.h
ImageMagick-7.0.10-60/coders/webp.h
ImageMagick-7.0.10-60/coders/wmf.h
ImageMagick-7.0.10-60/coders/wpg.h
ImageMagick-7.0.10-60/coders/xbm.h
ImageMagick-7.0.10-60/coders/xcf.h
ImageMagick-7.0.10-60/coders/xc.h
ImageMagick-7.0.10-60/coders/x.h
ImageMagick-7.0.10-60/coders/xpm.h
ImageMagick-7.0.10-60/coders/xps.h
ImageMagick-7.0.10-60/coders/xtrn.h
ImageMagick-7.0.10-60/coders/xwd.h
ImageMagick-7.0.10-60/coders/yaml.h
ImageMagick-7.0.10-60/coders/ycbcr.h
ImageMagick-7.0.10-60/coders/yuv.h
ImageMagick-7.0.10-60/coders/Makefile.am
ImageMagick-7.0.10-60/coders/aai.c
ImageMagick-7.0.10-60/coders/art.c
ImageMagick-7.0.10-60/coders/ashlar.c
ImageMagick-7.0.10-60/coders/avs.c
ImageMagick-7.0.10-60/coders/bgr.c
ImageMagick-7.0.10-60/coders/bmp.c
ImageMagick-7.0.10-60/coders/braille.c
ImageMagick-7.0.10-60/coders/cals.c
ImageMagick-7.0.10-60/coders/caption.c
ImageMagick-7.0.10-60/coders/cin.c
ImageMagick-7.0.10-60/coders/cip.c
ImageMagick-7.0.10-60/coders/clip.c
ImageMagick-7.0.10-60/coders/cmyk.c
ImageMagick-7.0.10-60/coders/cube.c
ImageMagick-7.0.10-60/coders/cut.c
ImageMagick-7.0.10-60/coders/dcm.c
ImageMagick-7.0.10-60/coders/dds.c
ImageMagick-7.0.10-60/coders/debug.c
ImageMagick-7.0.10-60/coders/dib.c
ImageMagick-7.0.10-60/coders/dng.c
ImageMagick-7.0.10-60/coders/dot.c
ImageMagick-7.0.10-60/coders/ps.c
ImageMagick-7.0.10-60/coders/dpx.c
ImageMagick-7.0.10-60/coders/farbfeld.c
ImageMagick-7.0.10-60/coders/fax.c
ImageMagick-7.0.10-60/coders/fits.c
ImageMagick-7.0.10-60/coders/fl32.c
ImageMagick-7.0.10-60/coders/gif.c
ImageMagick-7.0.10-60/coders/gradient.c
ImageMagick-7.0.10-60/coders/gray.c
ImageMagick-7.0.10-60/coders/hald.c
ImageMagick-7.0.10-60/coders/hdr.c
ImageMagick-7.0.10-60/coders/histogram.c
ImageMagick-7.0.10-60/coders/hrz.c
ImageMagick-7.0.10-60/coders/html.c
ImageMagick-7.0.10-60/coders/icon.c
ImageMagick-7.0.10-60/coders/info.c
ImageMagick-7.0.10-60/coders/inline.c
ImageMagick-7.0.10-60/coders/ipl.c
ImageMagick-7.0.10-60/coders/jnx.c
ImageMagick-7.0.10-60/coders/json.c
ImageMagick-7.0.10-60/coders/kernel.c
ImageMagick-7.0.10-60/coders/label.c
ImageMagick-7.0.10-60/coders/mac.c
ImageMagick-7.0.10-60/coders/magick.c
ImageMagick-7.0.10-60/coders/map.c
ImageMagick-7.0.10-60/coders/mask.c
ImageMagick-7.0.10-60/coders/mat.c
ImageMagick-7.0.10-60/coders/matte.c
ImageMagick-7.0.10-60/coders/meta.c
ImageMagick-7.0.10-60/coders/miff.c
ImageMagick-7.0.10-60/coders/mono.c
ImageMagick-7.0.10-60/coders/mpc.c
ImageMagick-7.0.10-60/coders/mpr.c
ImageMagick-7.0.10-60/coders/msl.c
ImageMagick-7.0.10-60/coders/mtv.c
ImageMagick-7.0.10-60/coders/mvg.c
ImageMagick-7.0.10-60/coders/null.c
ImageMagick-7.0.10-60/coders/ora.c
ImageMagick-7.0.10-60/coders/otb.c
ImageMagick-7.0.10-60/coders/palm.c
ImageMagick-7.0.10-60/coders/pango.c
ImageMagick-7.0.10-60/coders/pattern.c
ImageMagick-7.0.10-60/coders/pcd.c
ImageMagick-7.0.10-60/coders/pcl.c
ImageMagick-7.0.10-60/coders/pcx.c
ImageMagick-7.0.10-60/coders/pdb.c
ImageMagick-7.0.10-60/coders/pdf.c
ImageMagick-7.0.10-60/coders/pes.c
ImageMagick-7.0.10-60/coders/pgx.c
ImageMagick-7.0.10-60/coders/pict.c
ImageMagick-7.0.10-60/coders/pix.c
ImageMagick-7.0.10-60/coders/plasma.c
ImageMagick-7.0.10-60/coders/pnm.c
ImageMagick-7.0.10-60/coders/ps2.c
ImageMagick-7.0.10-60/coders/ps3.c
ImageMagick-7.0.10-60/coders/psd.c
ImageMagick-7.0.10-60/coders/pwp.c
ImageMagick-7.0.10-60/coders/raw.c
ImageMagick-7.0.10-60/coders/rgb.c
ImageMagick-7.0.10-60/coders/rgf.c
ImageMagick-7.0.10-60/coders/rla.c
ImageMagick-7.0.10-60/coders/rle.c
ImageMagick-7.0.10-60/coders/scr.c
ImageMagick-7.0.10-60/coders/screenshot.c
ImageMagick-7.0.10-60/coders/sct.c
ImageMagick-7.0.10-60/coders/sfw.c
ImageMagick-7.0.10-60/coders/sgi.c
ImageMagick-7.0.10-60/coders/sixel.c
ImageMagick-7.0.10-60/coders/stegano.c
ImageMagick-7.0.10-60/coders/sun.c
ImageMagick-7.0.10-60/coders/svg.c
ImageMagick-7.0.10-60/coders/tga.c
ImageMagick-7.0.10-60/coders/thumbnail.c
ImageMagick-7.0.10-60/coders/tile.c
ImageMagick-7.0.10-60/coders/tim2.c
ImageMagick-7.0.10-60/coders/tim.c
ImageMagick-7.0.10-60/coders/ttf.c
ImageMagick-7.0.10-60/coders/txt.c
ImageMagick-7.0.10-60/coders/uil.c
ImageMagick-7.0.10-60/coders/url.c
ImageMagick-7.0.10-60/coders/uyvy.c
ImageMagick-7.0.10-60/coders/vicar.c
ImageMagick-7.0.10-60/coders/vid.c
ImageMagick-7.0.10-60/coders/video.c
ImageMagick-7.0.10-60/coders/viff.c
ImageMagick-7.0.10-60/coders/vips.c
ImageMagick-7.0.10-60/coders/wbmp.c
ImageMagick-7.0.10-60/coders/wpg.c
ImageMagick-7.0.10-60/coders/xbm.c
ImageMagick-7.0.10-60/coders/xc.c
ImageMagick-7.0.10-60/coders/xcf.c
ImageMagick-7.0.10-60/coders/xpm.c
ImageMagick-7.0.10-60/coders/xps.c
ImageMagick-7.0.10-60/coders/xtrn.c
ImageMagick-7.0.10-60/coders/yaml.c
ImageMagick-7.0.10-60/coders/ycbcr.c
ImageMagick-7.0.10-60/coders/yuv.c
ImageMagick-7.0.10-60/coders/dps.c
ImageMagick-7.0.10-60/coders/djvu.c
ImageMagick-7.0.10-60/coders/exr.c
ImageMagick-7.0.10-60/coders/flif.c
ImageMagick-7.0.10-60/coders/fpx.c
ImageMagick-7.0.10-60/coders/clipboard.c
ImageMagick-7.0.10-60/coders/emf.c
ImageMagick-7.0.10-60/coders/heic.c
ImageMagick-7.0.10-60/coders/jbig.c
ImageMagick-7.0.10-60/coders/jpeg.c
ImageMagick-7.0.10-60/coders/jp2.c
ImageMagick-7.0.10-60/coders/jxl.c
ImageMagick-7.0.10-60/coders/png.c
ImageMagick-7.0.10-60/coders/ept.c
ImageMagick-7.0.10-60/coders/tiff.c
ImageMagick-7.0.10-60/coders/webp.c
ImageMagick-7.0.10-60/coders/wmf.c
ImageMagick-7.0.10-60/coders/x.c
ImageMagick-7.0.10-60/coders/xwd.c
ImageMagick-7.0.10-60/config/
ImageMagick-7.0.10-60/config/Makefile.am
ImageMagick-7.0.10-60/config/ImageMagick.rdf.in
ImageMagick-7.0.10-60/config/Magick++.dox.in
ImageMagick-7.0.10-60/config/MagickCore.dox.in
ImageMagick-7.0.10-60/config/MagickWand.dox.in
ImageMagick-7.0.10-60/config/ar-lib
ImageMagick-7.0.10-60/config/compile
ImageMagick-7.0.10-60/config/config.guess
ImageMagick-7.0.10-60/config/config.h.in
ImageMagick-7.0.10-60/config/config.sub
ImageMagick-7.0.10-60/config/configure.xml.in
ImageMagick-7.0.10-60/config/delegates.xml.in
ImageMagick-7.0.10-60/config/depcomp
ImageMagick-7.0.10-60/config/install-sh
ImageMagick-7.0.10-60/config/ltmain.sh
ImageMagick-7.0.10-60/config/missing
ImageMagick-7.0.10-60/config/mkinstalldirs
ImageMagick-7.0.10-60/config/tap-driver.sh
ImageMagick-7.0.10-60/config/test-driver
ImageMagick-7.0.10-60/config/type-apple.xml.in
ImageMagick-7.0.10-60/config/type-dejavu.xml.in
ImageMagick-7.0.10-60/config/type-ghostscript.xml.in
ImageMagick-7.0.10-60/config/type-urw-base35.xml.in
ImageMagick-7.0.10-60/config/type-windows.xml.in
ImageMagick-7.0.10-60/config/type.xml.in
ImageMagick-7.0.10-60/config/cmyk.icm
ImageMagick-7.0.10-60/config/colors.xml
ImageMagick-7.0.10-60/config/english.xml
ImageMagick-7.0.10-60/config/francais.xml
ImageMagick-7.0.10-60/config/ImageMagick.rc
ImageMagick-7.0.10-60/config/lndir.sh
ImageMagick-7.0.10-60/config/locale.md
ImageMagick-7.0.10-60/config/locale.xml
ImageMagick-7.0.10-60/config/log.xml
ImageMagick-7.0.10-60/config/mime.xml
ImageMagick-7.0.10-60/config/policy.xml
ImageMagick-7.0.10-60/config/quantization-table.xml
ImageMagick-7.0.10-60/config/sRGB.icm
ImageMagick-7.0.10-60/config/thresholds.xml
ImageMagick-7.0.10-60/filters/
ImageMagick-7.0.10-60/filters/Makefile.am
ImageMagick-7.0.10-60/filters/analyze.c
ImageMagick-7.0.10-60/m4/
ImageMagick-7.0.10-60/m4/ac_func_fseeko.m4
ImageMagick-7.0.10-60/m4/ax_c___attribute__.m4
ImageMagick-7.0.10-60/m4/ax_cflags_warn_all.m4
ImageMagick-7.0.10-60/m4/ax_check_compile_flag.m4
ImageMagick-7.0.10-60/m4/ax_check_framework.m4
ImageMagick-7.0.10-60/m4/ax_compare_version.m4
ImageMagick-7.0.10-60/m4/ax_compiler_vendor.m4
ImageMagick-7.0.10-60/m4/ax_cxx_bool.m4
ImageMagick-7.0.10-60/m4/ax_cxx_namespace_std.m4
ImageMagick-7.0.10-60/m4/ax_cxx_namespaces.m4
ImageMagick-7.0.10-60/m4/ax_gcc_archflag.m4
ImageMagick-7.0.10-60/m4/ax_gcc_x86_cpuid.m4
ImageMagick-7.0.10-60/m4/ax_have_opencl.m4
ImageMagick-7.0.10-60/m4/ax_prefix_config_h.m4
ImageMagick-7.0.10-60/m4/ax_prepend_flag.m4
ImageMagick-7.0.10-60/m4/ax_prog_perl_version.m4
ImageMagick-7.0.10-60/m4/ax_pthread.m4
ImageMagick-7.0.10-60/m4/ax_require_defined.m4
ImageMagick-7.0.10-60/m4/cxx_have_std_libs.m4
ImageMagick-7.0.10-60/m4/framework.m4
ImageMagick-7.0.10-60/m4/ld-version-script.m4
ImageMagick-7.0.10-60/m4/libtool.m4
ImageMagick-7.0.10-60/m4/ltoptions.m4
ImageMagick-7.0.10-60/m4/ltsugar.m4
ImageMagick-7.0.10-60/m4/ltversion.m4
ImageMagick-7.0.10-60/m4/lt~obsolete.m4
ImageMagick-7.0.10-60/m4/pkg.m4
ImageMagick-7.0.10-60/m4/version.m4
ImageMagick-7.0.10-60/m4/Makefile.am
ImageMagick-7.0.10-60/Magick++/
ImageMagick-7.0.10-60/Magick++/bin/
ImageMagick-7.0.10-60/Magick++/bin/Magick++-config.in
ImageMagick-7.0.10-60/Magick++/bin/Magick++-config.1
ImageMagick-7.0.10-60/Magick++/demo/
ImageMagick-7.0.10-60/Magick++/demo/analyze.cpp
ImageMagick-7.0.10-60/Magick++/demo/button.cpp
ImageMagick-7.0.10-60/Magick++/demo/demo.cpp
ImageMagick-7.0.10-60/Magick++/demo/detrans.cpp
ImageMagick-7.0.10-60/Magick++/demo/flip.cpp
ImageMagick-7.0.10-60/Magick++/demo/gravity.cpp
ImageMagick-7.0.10-60/Magick++/demo/piddle.cpp
ImageMagick-7.0.10-60/Magick++/demo/shapes.cpp
ImageMagick-7.0.10-60/Magick++/demo/zoom.cpp
ImageMagick-7.0.10-60/Magick++/demo/model.miff
ImageMagick-7.0.10-60/Magick++/demo/smile.miff
ImageMagick-7.0.10-60/Magick++/demo/smile_anim.miff
ImageMagick-7.0.10-60/Magick++/demo/tile.miff
ImageMagick-7.0.10-60/Magick++/demo/demos.tap
ImageMagick-7.0.10-60/Magick++/lib/
ImageMagick-7.0.10-60/Magick++/lib/Magick++/
ImageMagick-7.0.10-60/Magick++/lib/Magick++/Blob.h
ImageMagick-7.0.10-60/Magick++/lib/Magick++/CoderInfo.h
ImageMagick-7.0.10-60/Magick++/lib/Magick++/Color.h
ImageMagick-7.0.10-60/Magick++/lib/Magick++/Drawable.h
ImageMagick-7.0.10-60/Magick++/lib/Magick++/Exception.h
ImageMagick-7.0.10-60/Magick++/lib/Magick++/Functions.h
ImageMagick-7.0.10-60/Magick++/lib/Magick++/Geometry.h
ImageMagick-7.0.10-60/Magick++/lib/Magick++/Image.h
ImageMagick-7.0.10-60/Magick++/lib/Magick++/Include.h
ImageMagick-7.0.10-60/Magick++/lib/Magick++/Montage.h
ImageMagick-7.0.10-60/Magick++/lib/Magick++/Pixels.h
ImageMagick-7.0.10-60/Magick++/lib/Magick++/ResourceLimits.h
ImageMagick-7.0.10-60/Magick++/lib/Magick++/SecurityPolicy.h
ImageMagick-7.0.10-60/Magick++/lib/Magick++/Statistic.h
ImageMagick-7.0.10-60/Magick++/lib/Magick++/STL.h
ImageMagick-7.0.10-60/Magick++/lib/Magick++/TypeMetric.h
ImageMagick-7.0.10-60/Magick++/lib/Magick++/BlobRef.h
ImageMagick-7.0.10-60/Magick++/lib/Magick++/ImageRef.h
ImageMagick-7.0.10-60/Magick++/lib/Magick++/Options.h
ImageMagick-7.0.10-60/Magick++/lib/Magick++/Thread.h
ImageMagick-7.0.10-60/Magick++/lib/Magick++.h
ImageMagick-7.0.10-60/Magick++/lib/Magick++.pc.in
ImageMagick-7.0.10-60/Magick++/lib/Blob.cpp
ImageMagick-7.0.10-60/Magick++/lib/BlobRef.cpp
ImageMagick-7.0.10-60/Magick++/lib/CoderInfo.cpp
ImageMagick-7.0.10-60/Magick++/lib/Color.cpp
ImageMagick-7.0.10-60/Magick++/lib/Drawable.cpp
ImageMagick-7.0.10-60/Magick++/lib/Exception.cpp
ImageMagick-7.0.10-60/Magick++/lib/Functions.cpp
ImageMagick-7.0.10-60/Magick++/lib/Geometry.cpp
ImageMagick-7.0.10-60/Magick++/lib/Image.cpp
ImageMagick-7.0.10-60/Magick++/lib/ImageRef.cpp
ImageMagick-7.0.10-60/Magick++/lib/Montage.cpp
ImageMagick-7.0.10-60/Magick++/lib/Options.cpp
ImageMagick-7.0.10-60/Magick++/lib/Pixels.cpp
ImageMagick-7.0.10-60/Magick++/lib/ResourceLimits.cpp
ImageMagick-7.0.10-60/Magick++/lib/SecurityPolicy.cpp
ImageMagick-7.0.10-60/Magick++/lib/Statistic.cpp
ImageMagick-7.0.10-60/Magick++/lib/STL.cpp
ImageMagick-7.0.10-60/Magick++/lib/Thread.cpp
ImageMagick-7.0.10-60/Magick++/lib/TypeMetric.cpp
ImageMagick-7.0.10-60/Magick++/lib/libMagick++.map
ImageMagick-7.0.10-60/Magick++/tests/
ImageMagick-7.0.10-60/Magick++/tests/appendImages.cpp
ImageMagick-7.0.10-60/Magick++/tests/attributes.cpp
ImageMagick-7.0.10-60/Magick++/tests/averageImages.cpp
ImageMagick-7.0.10-60/Magick++/tests/coalesceImages.cpp
ImageMagick-7.0.10-60/Magick++/tests/coderInfo.cpp
ImageMagick-7.0.10-60/Magick++/tests/color.cpp
ImageMagick-7.0.10-60/Magick++/tests/colorHistogram.cpp
ImageMagick-7.0.10-60/Magick++/tests/exceptions.cpp
ImageMagick-7.0.10-60/Magick++/tests/geometry.cpp
ImageMagick-7.0.10-60/Magick++/tests/montageImages.cpp
ImageMagick-7.0.10-60/Magick++/tests/morphImages.cpp
ImageMagick-7.0.10-60/Magick++/tests/readWriteBlob.cpp
ImageMagick-7.0.10-60/Magick++/tests/readWriteImages.cpp
ImageMagick-7.0.10-60/Magick++/tests/tests.tap
ImageMagick-7.0.10-60/Magick++/tests/test_image.miff
ImageMagick-7.0.10-60/Magick++/tests/test_image_anim.miff
ImageMagick-7.0.10-60/Magick++/Makefile.am
ImageMagick-7.0.10-60/Magick++/AUTHORS
ImageMagick-7.0.10-60/Magick++/ChangeLog
ImageMagick-7.0.10-60/Magick++/INSTALL
ImageMagick-7.0.10-60/Magick++/LICENSE
ImageMagick-7.0.10-60/Magick++/NEWS
ImageMagick-7.0.10-60/Magick++/README
ImageMagick-7.0.10-60/MagickCore/
ImageMagick-7.0.10-60/MagickCore/MagickCore.h
ImageMagick-7.0.10-60/MagickCore/animate.h
ImageMagick-7.0.10-60/MagickCore/annotate.h
ImageMagick-7.0.10-60/MagickCore/artifact.h
ImageMagick-7.0.10-60/MagickCore/attribute.h
ImageMagick-7.0.10-60/MagickCore/blob.h
ImageMagick-7.0.10-60/MagickCore/cache.h
ImageMagick-7.0.10-60/MagickCore/cache-view.h
ImageMagick-7.0.10-60/MagickCore/channel.h
ImageMagick-7.0.10-60/MagickCore/cipher.h
ImageMagick-7.0.10-60/MagickCore/client.h
ImageMagick-7.0.10-60/MagickCore/coder.h
ImageMagick-7.0.10-60/MagickCore/color.h
ImageMagick-7.0.10-60/MagickCore/colormap.h
ImageMagick-7.0.10-60/MagickCore/colorspace.h
ImageMagick-7.0.10-60/MagickCore/compare.h
ImageMagick-7.0.10-60/MagickCore/composite.h
ImageMagick-7.0.10-60/MagickCore/compress.h
ImageMagick-7.0.10-60/MagickCore/configure.h
ImageMagick-7.0.10-60/MagickCore/constitute.h
ImageMagick-7.0.10-60/MagickCore/decorate.h
ImageMagick-7.0.10-60/MagickCore/delegate.h
ImageMagick-7.0.10-60/MagickCore/deprecate.h
ImageMagick-7.0.10-60/MagickCore/display.h
ImageMagick-7.0.10-60/MagickCore/distort.h
ImageMagick-7.0.10-60/MagickCore/distribute-cache.h
ImageMagick-7.0.10-60/MagickCore/draw.h
ImageMagick-7.0.10-60/MagickCore/effect.h
ImageMagick-7.0.10-60/MagickCore/enhance.h
ImageMagick-7.0.10-60/MagickCore/exception.h
ImageMagick-7.0.10-60/MagickCore/feature.h
ImageMagick-7.0.10-60/MagickCore/fourier.h
ImageMagick-7.0.10-60/MagickCore/fx.h
ImageMagick-7.0.10-60/MagickCore/gem.h
ImageMagick-7.0.10-60/MagickCore/geometry.h
ImageMagick-7.0.10-60/MagickCore/histogram.h
ImageMagick-7.0.10-60/MagickCore/identify.h
ImageMagick-7.0.10-60/MagickCore/image.h
ImageMagick-7.0.10-60/MagickCore/image-view.h
ImageMagick-7.0.10-60/MagickCore/layer.h
ImageMagick-7.0.10-60/MagickCore/linked-list.h
ImageMagick-7.0.10-60/MagickCore/list.h
ImageMagick-7.0.10-60/MagickCore/locale_.h
ImageMagick-7.0.10-60/MagickCore/log.h
ImageMagick-7.0.10-60/MagickCore/magic.h
ImageMagick-7.0.10-60/MagickCore/magick.h
ImageMagick-7.0.10-60/MagickCore/magick-config.h
ImageMagick-7.0.10-60/MagickCore/magick-type.h
ImageMagick-7.0.10-60/MagickCore/matrix.h
ImageMagick-7.0.10-60/MagickCore/memory_.h
ImageMagick-7.0.10-60/MagickCore/method-attribute.h
ImageMagick-7.0.10-60/MagickCore/methods.h
ImageMagick-7.0.10-60/MagickCore/mime.h
ImageMagick-7.0.10-60/MagickCore/module.h
ImageMagick-7.0.10-60/MagickCore/monitor.h
ImageMagick-7.0.10-60/MagickCore/montage.h
ImageMagick-7.0.10-60/MagickCore/morphology.h
ImageMagick-7.0.10-60/MagickCore/nt-base.h
ImageMagick-7.0.10-60/MagickCore/opencl.h
ImageMagick-7.0.10-60/MagickCore/option.h
ImageMagick-7.0.10-60/MagickCore/paint.h
ImageMagick-7.0.10-60/MagickCore/pixel.h
ImageMagick-7.0.10-60/MagickCore/pixel-accessor.h
ImageMagick-7.0.10-60/MagickCore/policy.h
ImageMagick-7.0.10-60/MagickCore/prepress.h
ImageMagick-7.0.10-60/MagickCore/profile.h
ImageMagick-7.0.10-60/MagickCore/property.h
ImageMagick-7.0.10-60/MagickCore/quantize.h
ImageMagick-7.0.10-60/MagickCore/quantum.h
ImageMagick-7.0.10-60/MagickCore/random_.h
ImageMagick-7.0.10-60/MagickCore/registry.h
ImageMagick-7.0.10-60/MagickCore/resample.h
ImageMagick-7.0.10-60/MagickCore/resize.h
ImageMagick-7.0.10-60/MagickCore/resource_.h
ImageMagick-7.0.10-60/MagickCore/segment.h
ImageMagick-7.0.10-60/MagickCore/semaphore.h
ImageMagick-7.0.10-60/MagickCore/shear.h
ImageMagick-7.0.10-60/MagickCore/signature.h
ImageMagick-7.0.10-60/MagickCore/splay-tree.h
ImageMagick-7.0.10-60/MagickCore/static.h
ImageMagick-7.0.10-60/MagickCore/statistic.h
ImageMagick-7.0.10-60/MagickCore/stream.h
ImageMagick-7.0.10-60/MagickCore/string_.h
ImageMagick-7.0.10-60/MagickCore/studio.h
ImageMagick-7.0.10-60/MagickCore/timer.h
ImageMagick-7.0.10-60/MagickCore/token.h
ImageMagick-7.0.10-60/MagickCore/transform.h
ImageMagick-7.0.10-60/MagickCore/threshold.h
ImageMagick-7.0.10-60/MagickCore/type.h
ImageMagick-7.0.10-60/MagickCore/utility.h
ImageMagick-7.0.10-60/MagickCore/version.h
ImageMagick-7.0.10-60/MagickCore/vision.h
ImageMagick-7.0.10-60/MagickCore/visual-effects.h
ImageMagick-7.0.10-60/MagickCore/widget.h
ImageMagick-7.0.10-60/MagickCore/xml-tree.h
ImageMagick-7.0.10-60/MagickCore/xwindow.h
ImageMagick-7.0.10-60/MagickCore/magick-baseconfig.h
ImageMagick-7.0.10-60/MagickCore/accelerate-private.h
ImageMagick-7.0.10-60/MagickCore/accelerate-kernels-private.h
ImageMagick-7.0.10-60/MagickCore/animate-private.h
ImageMagick-7.0.10-60/MagickCore/annotate-private.h
ImageMagick-7.0.10-60/MagickCore/blob-private.h
ImageMagick-7.0.10-60/MagickCore/cache-private.h
ImageMagick-7.0.10-60/MagickCore/coder-private.h
ImageMagick-7.0.10-60/MagickCore/colormap-private.h
ImageMagick-7.0.10-60/MagickCore/color-private.h
ImageMagick-7.0.10-60/MagickCore/colorspace-private.h
ImageMagick-7.0.10-60/MagickCore/composite-private.h
ImageMagick-7.0.10-60/MagickCore/configure-private.h
ImageMagick-7.0.10-60/MagickCore/constitute-private.h
ImageMagick-7.0.10-60/MagickCore/delegate-private.h
ImageMagick-7.0.10-60/MagickCore/display-private.h
ImageMagick-7.0.10-60/MagickCore/distribute-cache-private.h
ImageMagick-7.0.10-60/MagickCore/draw-private.h
ImageMagick-7.0.10-60/MagickCore/exception-private.h
ImageMagick-7.0.10-60/MagickCore/fx-private.h
ImageMagick-7.0.10-60/MagickCore/gem-private.h
ImageMagick-7.0.10-60/MagickCore/image-private.h
ImageMagick-7.0.10-60/MagickCore/locale-private.h
ImageMagick-7.0.10-60/MagickCore/log-private.h
ImageMagick-7.0.10-60/MagickCore/magick-private.h
ImageMagick-7.0.10-60/MagickCore/magic-private.h
ImageMagick-7.0.10-60/MagickCore/matrix-private.h
ImageMagick-7.0.10-60/MagickCore/memory-private.h
ImageMagick-7.0.10-60/MagickCore/methods-private.h
ImageMagick-7.0.10-60/MagickCore/mime-private.h
ImageMagick-7.0.10-60/MagickCore/module-private.h
ImageMagick-7.0.10-60/MagickCore/monitor-private.h
ImageMagick-7.0.10-60/MagickCore/morphology-private.h
ImageMagick-7.0.10-60/MagickCore/mutex.h
ImageMagick-7.0.10-60/MagickCore/nt-feature.h
ImageMagick-7.0.10-60/MagickCore/opencl-private.h
ImageMagick-7.0.10-60/MagickCore/option-private.h
ImageMagick-7.0.10-60/MagickCore/pixel-private.h
ImageMagick-7.0.10-60/MagickCore/policy-private.h
ImageMagick-7.0.10-60/MagickCore/profile-private.h
ImageMagick-7.0.10-60/MagickCore/quantum-private.h
ImageMagick-7.0.10-60/MagickCore/random-private.h
ImageMagick-7.0.10-60/MagickCore/registry-private.h
ImageMagick-7.0.10-60/MagickCore/resample-private.h
ImageMagick-7.0.10-60/MagickCore/resize-private.h
ImageMagick-7.0.10-60/MagickCore/resource-private.h
ImageMagick-7.0.10-60/MagickCore/semaphore-private.h
ImageMagick-7.0.10-60/MagickCore/signature-private.h
ImageMagick-7.0.10-60/MagickCore/stream-private.h
ImageMagick-7.0.10-60/MagickCore/string-private.h
ImageMagick-7.0.10-60/MagickCore/thread_.h
ImageMagick-7.0.10-60/MagickCore/thread-private.h
ImageMagick-7.0.10-60/MagickCore/timer-private.h
ImageMagick-7.0.10-60/MagickCore/token-private.h
ImageMagick-7.0.10-60/MagickCore/transform-private.h
ImageMagick-7.0.10-60/MagickCore/type-private.h
ImageMagick-7.0.10-60/MagickCore/utility-private.h
ImageMagick-7.0.10-60/MagickCore/version-private.h
ImageMagick-7.0.10-60/MagickCore/widget-private.h
ImageMagick-7.0.10-60/MagickCore/xml-tree-private.h
ImageMagick-7.0.10-60/MagickCore/xwindow-private.h
ImageMagick-7.0.10-60/MagickCore/Makefile.am
ImageMagick-7.0.10-60/MagickCore/ImageMagick.pc.in
ImageMagick-7.0.10-60/MagickCore/MagickCore-config.in
ImageMagick-7.0.10-60/MagickCore/MagickCore.pc.in
ImageMagick-7.0.10-60/MagickCore/version.h.in
ImageMagick-7.0.10-60/MagickCore/accelerate.c
ImageMagick-7.0.10-60/MagickCore/animate.c
ImageMagick-7.0.10-60/MagickCore/annotate.c
ImageMagick-7.0.10-60/MagickCore/artifact.c
ImageMagick-7.0.10-60/MagickCore/attribute.c
ImageMagick-7.0.10-60/MagickCore/blob.c
ImageMagick-7.0.10-60/MagickCore/cache.c
ImageMagick-7.0.10-60/MagickCore/cache-view.c
ImageMagick-7.0.10-60/MagickCore/channel.c
ImageMagick-7.0.10-60/MagickCore/cipher.c
ImageMagick-7.0.10-60/MagickCore/client.c
ImageMagick-7.0.10-60/MagickCore/coder.c
ImageMagick-7.0.10-60/MagickCore/color.c
ImageMagick-7.0.10-60/MagickCore/colormap.c
ImageMagick-7.0.10-60/MagickCore/colorspace.c
ImageMagick-7.0.10-60/MagickCore/compare.c
ImageMagick-7.0.10-60/MagickCore/composite.c
ImageMagick-7.0.10-60/MagickCore/compress.c
ImageMagick-7.0.10-60/MagickCore/configure.c
ImageMagick-7.0.10-60/MagickCore/constitute.c
ImageMagick-7.0.10-60/MagickCore/decorate.c
ImageMagick-7.0.10-60/MagickCore/delegate.c
ImageMagick-7.0.10-60/MagickCore/deprecate.c
ImageMagick-7.0.10-60/MagickCore/display.c
ImageMagick-7.0.10-60/MagickCore/distort.c
ImageMagick-7.0.10-60/MagickCore/distribute-cache.c
ImageMagick-7.0.10-60/MagickCore/draw.c
ImageMagick-7.0.10-60/MagickCore/effect.c
ImageMagick-7.0.10-60/MagickCore/enhance.c
ImageMagick-7.0.10-60/MagickCore/exception.c
ImageMagick-7.0.10-60/MagickCore/feature.c
ImageMagick-7.0.10-60/MagickCore/fourier.c
ImageMagick-7.0.10-60/MagickCore/fx.c
ImageMagick-7.0.10-60/MagickCore/gem.c
ImageMagick-7.0.10-60/MagickCore/geometry.c
ImageMagick-7.0.10-60/MagickCore/histogram.c
ImageMagick-7.0.10-60/MagickCore/identify.c
ImageMagick-7.0.10-60/MagickCore/image.c
ImageMagick-7.0.10-60/MagickCore/image-view.c
ImageMagick-7.0.10-60/MagickCore/layer.c
ImageMagick-7.0.10-60/MagickCore/linked-list.c
ImageMagick-7.0.10-60/MagickCore/list.c
ImageMagick-7.0.10-60/MagickCore/locale.c
ImageMagick-7.0.10-60/MagickCore/log.c
ImageMagick-7.0.10-60/MagickCore/magic.c
ImageMagick-7.0.10-60/MagickCore/magick.c
ImageMagick-7.0.10-60/MagickCore/matrix.c
ImageMagick-7.0.10-60/MagickCore/memory.c
ImageMagick-7.0.10-60/MagickCore/mime.c
ImageMagick-7.0.10-60/MagickCore/module.c
ImageMagick-7.0.10-60/MagickCore/monitor.c
ImageMagick-7.0.10-60/MagickCore/montage.c
ImageMagick-7.0.10-60/MagickCore/morphology.c
ImageMagick-7.0.10-60/MagickCore/nt-base-private.h
ImageMagick-7.0.10-60/MagickCore/opencl.c
ImageMagick-7.0.10-60/MagickCore/option.c
ImageMagick-7.0.10-60/MagickCore/paint.c
ImageMagick-7.0.10-60/MagickCore/pixel.c
ImageMagick-7.0.10-60/MagickCore/policy.c
ImageMagick-7.0.10-60/MagickCore/prepress.c
ImageMagick-7.0.10-60/MagickCore/property.c
ImageMagick-7.0.10-60/MagickCore/profile.c
ImageMagick-7.0.10-60/MagickCore/quantize.c
ImageMagick-7.0.10-60/MagickCore/quantum.c
ImageMagick-7.0.10-60/MagickCore/quantum-export.c
ImageMagick-7.0.10-60/MagickCore/quantum-import.c
ImageMagick-7.0.10-60/MagickCore/random.c
ImageMagick-7.0.10-60/MagickCore/registry.c
ImageMagick-7.0.10-60/MagickCore/resample.c
ImageMagick-7.0.10-60/MagickCore/resize.c
ImageMagick-7.0.10-60/MagickCore/resource.c
ImageMagick-7.0.10-60/MagickCore/segment.c
ImageMagick-7.0.10-60/MagickCore/semaphore.c
ImageMagick-7.0.10-60/MagickCore/shear.c
ImageMagick-7.0.10-60/MagickCore/signature.c
ImageMagick-7.0.10-60/MagickCore/splay-tree.c
ImageMagick-7.0.10-60/MagickCore/static.c
ImageMagick-7.0.10-60/MagickCore/statistic.c
ImageMagick-7.0.10-60/MagickCore/stream.c
ImageMagick-7.0.10-60/MagickCore/string.c
ImageMagick-7.0.10-60/MagickCore/thread.c
ImageMagick-7.0.10-60/MagickCore/timer.c
ImageMagick-7.0.10-60/MagickCore/token.c
ImageMagick-7.0.10-60/MagickCore/transform.c
ImageMagick-7.0.10-60/MagickCore/threshold.c
ImageMagick-7.0.10-60/MagickCore/type.c
ImageMagick-7.0.10-60/MagickCore/utility.c
ImageMagick-7.0.10-60/MagickCore/version.c
ImageMagick-7.0.10-60/MagickCore/visual-effects.c
ImageMagick-7.0.10-60/MagickCore/vision.c
ImageMagick-7.0.10-60/MagickCore/widget.c
ImageMagick-7.0.10-60/MagickCore/xml-tree.c
ImageMagick-7.0.10-60/MagickCore/xwindow.c
ImageMagick-7.0.10-60/MagickCore/nt-feature.c
ImageMagick-7.0.10-60/MagickCore/nt-base.c
ImageMagick-7.0.10-60/MagickCore/MagickCore-config.1
ImageMagick-7.0.10-60/MagickCore/libMagickCore.map
ImageMagick-7.0.10-60/MagickWand/
ImageMagick-7.0.10-60/MagickWand/MagickWand.h
ImageMagick-7.0.10-60/MagickWand/animate.h
ImageMagick-7.0.10-60/MagickWand/compare.h
ImageMagick-7.0.10-60/MagickWand/composite.h
ImageMagick-7.0.10-60/MagickWand/conjure.h
ImageMagick-7.0.10-60/MagickWand/convert.h
ImageMagick-7.0.10-60/MagickWand/deprecate.h
ImageMagick-7.0.10-60/MagickWand/display.h
ImageMagick-7.0.10-60/MagickWand/drawing-wand.h
ImageMagick-7.0.10-60/MagickWand/identify.h
ImageMagick-7.0.10-60/MagickWand/import.h
ImageMagick-7.0.10-60/MagickWand/magick-cli.h
ImageMagick-7.0.10-60/MagickWand/magick-image.h
ImageMagick-7.0.10-60/MagickWand/magick-property.h
ImageMagick-7.0.10-60/MagickWand/method-attribute.h
ImageMagick-7.0.10-60/MagickWand/mogrify.h
ImageMagick-7.0.10-60/MagickWand/montage.h
ImageMagick-7.0.10-60/MagickWand/operation.h
ImageMagick-7.0.10-60/MagickWand/pixel-iterator.h
ImageMagick-7.0.10-60/MagickWand/pixel-wand.h
ImageMagick-7.0.10-60/MagickWand/stream.h
ImageMagick-7.0.10-60/MagickWand/wandcli.h
ImageMagick-7.0.10-60/MagickWand/wand-view.h
ImageMagick-7.0.10-60/MagickWand/mogrify-private.h
ImageMagick-7.0.10-60/MagickWand/magick-wand-private.h
ImageMagick-7.0.10-60/MagickWand/operation-private.h
ImageMagick-7.0.10-60/MagickWand/pixel-wand-private.h
ImageMagick-7.0.10-60/MagickWand/script-token.h
ImageMagick-7.0.10-60/MagickWand/studio.h
ImageMagick-7.0.10-60/MagickWand/wand.h
ImageMagick-7.0.10-60/MagickWand/wandcli-private.h
ImageMagick-7.0.10-60/MagickWand/Makefile.am
ImageMagick-7.0.10-60/MagickWand/MagickWand-config.in
ImageMagick-7.0.10-60/MagickWand/MagickWand.pc.in
ImageMagick-7.0.10-60/MagickWand/animate.c
ImageMagick-7.0.10-60/MagickWand/compare.c
ImageMagick-7.0.10-60/MagickWand/composite.c
ImageMagick-7.0.10-60/MagickWand/conjure.c
ImageMagick-7.0.10-60/MagickWand/convert.c
ImageMagick-7.0.10-60/MagickWand/deprecate.c
ImageMagick-7.0.10-60/MagickWand/display.c
ImageMagick-7.0.10-60/MagickWand/drawing-wand.c
ImageMagick-7.0.10-60/MagickWand/identify.c
ImageMagick-7.0.10-60/MagickWand/import.c
ImageMagick-7.0.10-60/MagickWand/magick-cli.c
ImageMagick-7.0.10-60/MagickWand/magick-image.c
ImageMagick-7.0.10-60/MagickWand/magick-property.c
ImageMagick-7.0.10-60/MagickWand/magick-wand.c
ImageMagick-7.0.10-60/MagickWand/mogrify.c
ImageMagick-7.0.10-60/MagickWand/montage.c
ImageMagick-7.0.10-60/MagickWand/operation.c
ImageMagick-7.0.10-60/MagickWand/pixel-iterator.c
ImageMagick-7.0.10-60/MagickWand/pixel-wand.c
ImageMagick-7.0.10-60/MagickWand/script-token.c
ImageMagick-7.0.10-60/MagickWand/stream.c
ImageMagick-7.0.10-60/MagickWand/wand.c
ImageMagick-7.0.10-60/MagickWand/wandcli.c
ImageMagick-7.0.10-60/MagickWand/wand-view.c
ImageMagick-7.0.10-60/MagickWand/ChangeLog
ImageMagick-7.0.10-60/MagickWand/libMagickWand.map
ImageMagick-7.0.10-60/MagickWand/MagickWand-config.1
ImageMagick-7.0.10-60/PerlMagick/
ImageMagick-7.0.10-60/PerlMagick/default/
ImageMagick-7.0.10-60/PerlMagick/default/Magick.pm.in
ImageMagick-7.0.10-60/PerlMagick/default/Makefile.PL.in
ImageMagick-7.0.10-60/PerlMagick/default/Magick.pm
ImageMagick-7.0.10-60/PerlMagick/default/Makefile.PL
ImageMagick-7.0.10-60/PerlMagick/quantum/
ImageMagick-7.0.10-60/PerlMagick/quantum/Makefile.PL.in
ImageMagick-7.0.10-60/PerlMagick/quantum/quantum.pm.in
ImageMagick-7.0.10-60/PerlMagick/quantum/quantum.xs.in
ImageMagick-7.0.10-60/PerlMagick/quantum/typemap.in
ImageMagick-7.0.10-60/PerlMagick/quantum/Makefile.PL
ImageMagick-7.0.10-60/PerlMagick/quantum/quantum.pm
ImageMagick-7.0.10-60/PerlMagick/quantum/quantum.xs
ImageMagick-7.0.10-60/PerlMagick/quantum/typemap
ImageMagick-7.0.10-60/PerlMagick/Changelog
ImageMagick-7.0.10-60/PerlMagick/MANIFEST
ImageMagick-7.0.10-60/PerlMagick/MANIFEST.SKIP
ImageMagick-7.0.10-60/PerlMagick/Makefile.PL.in
ImageMagick-7.0.10-60/PerlMagick/Makefile.am
ImageMagick-7.0.10-60/PerlMagick/Makefile.nt
ImageMagick-7.0.10-60/PerlMagick/README.txt
ImageMagick-7.0.10-60/PerlMagick/check.sh.in
ImageMagick-7.0.10-60/PerlMagick/demo/
ImageMagick-7.0.10-60/PerlMagick/demo/Generic.ttf
ImageMagick-7.0.10-60/PerlMagick/demo/Makefile
ImageMagick-7.0.10-60/PerlMagick/demo/README
ImageMagick-7.0.10-60/PerlMagick/demo/Turtle.pm
ImageMagick-7.0.10-60/PerlMagick/demo/annotate.pl
ImageMagick-7.0.10-60/PerlMagick/demo/annotate_words.pl
ImageMagick-7.0.10-60/PerlMagick/demo/button.pl
ImageMagick-7.0.10-60/PerlMagick/demo/compose-specials.pl
ImageMagick-7.0.10-60/PerlMagick/demo/composite.pl
ImageMagick-7.0.10-60/PerlMagick/demo/demo.pl
ImageMagick-7.0.10-60/PerlMagick/demo/dst.png
ImageMagick-7.0.10-60/PerlMagick/demo/lsys.pl
ImageMagick-7.0.10-60/PerlMagick/demo/model.gif
ImageMagick-7.0.10-60/PerlMagick/demo/piddle.pl
ImageMagick-7.0.10-60/PerlMagick/demo/pink-flower.gif
ImageMagick-7.0.10-60/PerlMagick/demo/pixel-fx.pl
ImageMagick-7.0.10-60/PerlMagick/demo/red-flower.gif
ImageMagick-7.0.10-60/PerlMagick/demo/settings.pl
ImageMagick-7.0.10-60/PerlMagick/demo/shadow-text.pl
ImageMagick-7.0.10-60/PerlMagick/demo/shapes.pl
ImageMagick-7.0.10-60/PerlMagick/demo/single-pixels.pl
ImageMagick-7.0.10-60/PerlMagick/demo/smile.gif
ImageMagick-7.0.10-60/PerlMagick/demo/src.png
ImageMagick-7.0.10-60/PerlMagick/demo/steganography.pl
ImageMagick-7.0.10-60/PerlMagick/demo/tile.gif
ImageMagick-7.0.10-60/PerlMagick/demo/tree.pl
ImageMagick-7.0.10-60/PerlMagick/demo/yellow-flower.gif
ImageMagick-7.0.10-60/PerlMagick/t/
ImageMagick-7.0.10-60/PerlMagick/t/Generic.ttf
ImageMagick-7.0.10-60/PerlMagick/t/MasterImage_70x46.ppm
ImageMagick-7.0.10-60/PerlMagick/t/blob.t
ImageMagick-7.0.10-60/PerlMagick/t/bzlib/
ImageMagick-7.0.10-60/PerlMagick/t/bzlib/input.miff
ImageMagick-7.0.10-60/PerlMagick/t/bzlib/input.miff.bz2
ImageMagick-7.0.10-60/PerlMagick/t/bzlib/read.t
ImageMagick-7.0.10-60/PerlMagick/t/bzlib/write.t
ImageMagick-7.0.10-60/PerlMagick/t/cgm/
ImageMagick-7.0.10-60/PerlMagick/t/cgm/input.cgm
ImageMagick-7.0.10-60/PerlMagick/t/cgm/read.t
ImageMagick-7.0.10-60/PerlMagick/t/composite.t
ImageMagick-7.0.10-60/PerlMagick/t/filter.t
ImageMagick-7.0.10-60/PerlMagick/t/fpx/
ImageMagick-7.0.10-60/PerlMagick/t/fpx/input_256.fpx
ImageMagick-7.0.10-60/PerlMagick/t/fpx/input_bw.fpx
ImageMagick-7.0.10-60/PerlMagick/t/fpx/input_grayscale.fpx
ImageMagick-7.0.10-60/PerlMagick/t/fpx/input_jpeg.fpx
ImageMagick-7.0.10-60/PerlMagick/t/fpx/input_truecolor.fpx
ImageMagick-7.0.10-60/PerlMagick/t/fpx/read.t
ImageMagick-7.0.10-60/PerlMagick/t/fpx/write.t
ImageMagick-7.0.10-60/PerlMagick/t/getattribute.t
ImageMagick-7.0.10-60/PerlMagick/t/hdf/
ImageMagick-7.0.10-60/PerlMagick/t/hdf/input_256.hdf
ImageMagick-7.0.10-60/PerlMagick/t/hdf/input_truecolor.hdf
ImageMagick-7.0.10-60/PerlMagick/t/hdf/read.t
ImageMagick-7.0.10-60/PerlMagick/t/hdf/write.t
ImageMagick-7.0.10-60/PerlMagick/t/hpgl/
ImageMagick-7.0.10-60/PerlMagick/t/hpgl/input.hpgl
ImageMagick-7.0.10-60/PerlMagick/t/hpgl/read.t
ImageMagick-7.0.10-60/PerlMagick/t/input.avs
ImageMagick-7.0.10-60/PerlMagick/t/input.bie
ImageMagick-7.0.10-60/PerlMagick/t/input.bmp
ImageMagick-7.0.10-60/PerlMagick/t/input.bmp24
ImageMagick-7.0.10-60/PerlMagick/t/input.dcx
ImageMagick-7.0.10-60/PerlMagick/t/input.dib
ImageMagick-7.0.10-60/PerlMagick/t/input.fits
ImageMagick-7.0.10-60/PerlMagick/t/input.gif
ImageMagick-7.0.10-60/PerlMagick/t/input.gif87
ImageMagick-7.0.10-60/PerlMagick/t/input.ico
ImageMagick-7.0.10-60/PerlMagick/t/input.im1
ImageMagick-7.0.10-60/PerlMagick/t/input.im24
ImageMagick-7.0.10-60/PerlMagick/t/input.im8
ImageMagick-7.0.10-60/PerlMagick/t/input.mat
ImageMagick-7.0.10-60/PerlMagick/t/input.miff
ImageMagick-7.0.10-60/PerlMagick/t/input.mtv
ImageMagick-7.0.10-60/PerlMagick/t/input.p7
ImageMagick-7.0.10-60/PerlMagick/t/input.pcx
ImageMagick-7.0.10-60/PerlMagick/t/input.pict
ImageMagick-7.0.10-60/PerlMagick/t/input.psd
ImageMagick-7.0.10-60/PerlMagick/t/input.rle
ImageMagick-7.0.10-60/PerlMagick/t/input.sgi
ImageMagick-7.0.10-60/PerlMagick/t/input.tga
ImageMagick-7.0.10-60/PerlMagick/t/input.tim
ImageMagick-7.0.10-60/PerlMagick/t/input.viff
ImageMagick-7.0.10-60/PerlMagick/t/input.wbmp
ImageMagick-7.0.10-60/PerlMagick/t/input.wpg
ImageMagick-7.0.10-60/PerlMagick/t/input.xbm
ImageMagick-7.0.10-60/PerlMagick/t/input.xpm
ImageMagick-7.0.10-60/PerlMagick/t/input_16.miff
ImageMagick-7.0.10-60/PerlMagick/t/input_70x46.cmyk
ImageMagick-7.0.10-60/PerlMagick/t/input_70x46.gray
ImageMagick-7.0.10-60/PerlMagick/t/input_70x46.rgb
ImageMagick-7.0.10-60/PerlMagick/t/input_70x46.rgba
ImageMagick-7.0.10-60/PerlMagick/t/input_70x46.uyvy
ImageMagick-7.0.10-60/PerlMagick/t/input_70x46.yuv
ImageMagick-7.0.10-60/PerlMagick/t/input_gray_lsb_08bit.mat
ImageMagick-7.0.10-60/PerlMagick/t/input_gray_lsb_double.mat
ImageMagick-7.0.10-60/PerlMagick/t/input_gray_msb_08bit.mat
ImageMagick-7.0.10-60/PerlMagick/t/input_p1.pbm
ImageMagick-7.0.10-60/PerlMagick/t/input_p2.pgm
ImageMagick-7.0.10-60/PerlMagick/t/input_p3.ppm
ImageMagick-7.0.10-60/PerlMagick/t/input_p4.pbm
ImageMagick-7.0.10-60/PerlMagick/t/input_p5.pgm
ImageMagick-7.0.10-60/PerlMagick/t/input_p6.ppm
ImageMagick-7.0.10-60/PerlMagick/t/input_p7.p7
ImageMagick-7.0.10-60/PerlMagick/t/input_rgb_lsb_08bit.mat
ImageMagick-7.0.10-60/PerlMagick/t/jbig/
ImageMagick-7.0.10-60/PerlMagick/t/jbig/input.jbig
ImageMagick-7.0.10-60/PerlMagick/t/jbig/read.t
ImageMagick-7.0.10-60/PerlMagick/t/jbig/write.t
ImageMagick-7.0.10-60/PerlMagick/t/jng/
ImageMagick-7.0.10-60/PerlMagick/t/jng/input_gray.jng
ImageMagick-7.0.10-60/PerlMagick/t/jng/input_gray_idat.jng
ImageMagick-7.0.10-60/PerlMagick/t/jng/input_gray_jdaa.jng
ImageMagick-7.0.10-60/PerlMagick/t/jng/input_gray_prog.jng
ImageMagick-7.0.10-60/PerlMagick/t/jng/input_gray_prog_idat.jng
ImageMagick-7.0.10-60/PerlMagick/t/jng/input_gray_prog_jdaa.jng
ImageMagick-7.0.10-60/PerlMagick/t/jng/input_idat.jng
ImageMagick-7.0.10-60/PerlMagick/t/jng/input_jdaa.jng
ImageMagick-7.0.10-60/PerlMagick/t/jng/input_prog.jng
ImageMagick-7.0.10-60/PerlMagick/t/jng/input_prog_idat.jng
ImageMagick-7.0.10-60/PerlMagick/t/jng/input_prog_jdaa.jng
ImageMagick-7.0.10-60/PerlMagick/t/jng/input_rose.jng
ImageMagick-7.0.10-60/PerlMagick/t/jng/read.t
ImageMagick-7.0.10-60/PerlMagick/t/jng/write.t
ImageMagick-7.0.10-60/PerlMagick/t/jpeg/
ImageMagick-7.0.10-60/PerlMagick/t/jpeg/input.jpg
ImageMagick-7.0.10-60/PerlMagick/t/jpeg/input_plane.jpg
ImageMagick-7.0.10-60/PerlMagick/t/jpeg/read.t
ImageMagick-7.0.10-60/PerlMagick/t/jpeg/write.t
ImageMagick-7.0.10-60/PerlMagick/t/montage.t
ImageMagick-7.0.10-60/PerlMagick/t/mpeg/
ImageMagick-7.0.10-60/PerlMagick/t/mpeg/input.m2v
ImageMagick-7.0.10-60/PerlMagick/t/mpeg/input.mpg
ImageMagick-7.0.10-60/PerlMagick/t/mpeg/read.t
ImageMagick-7.0.10-60/PerlMagick/t/openjp2/
ImageMagick-7.0.10-60/PerlMagick/t/openjp2/input.j2k
ImageMagick-7.0.10-60/PerlMagick/t/openjp2/input.jp2
ImageMagick-7.0.10-60/PerlMagick/t/openjp2/input.jpc
ImageMagick-7.0.10-60/PerlMagick/t/openjp2/read.t
ImageMagick-7.0.10-60/PerlMagick/t/ping.t
ImageMagick-7.0.10-60/PerlMagick/t/png/
ImageMagick-7.0.10-60/PerlMagick/t/png/input.mng
ImageMagick-7.0.10-60/PerlMagick/t/png/input_16.png
ImageMagick-7.0.10-60/PerlMagick/t/png/input_256.png
ImageMagick-7.0.10-60/PerlMagick/t/png/input_bw.png
ImageMagick-7.0.10-60/PerlMagick/t/png/input_mono.png
ImageMagick-7.0.10-60/PerlMagick/t/png/input_truecolor.png
ImageMagick-7.0.10-60/PerlMagick/t/png/read-16.t
ImageMagick-7.0.10-60/PerlMagick/t/png/read.t
ImageMagick-7.0.10-60/PerlMagick/t/png/write-16.t
ImageMagick-7.0.10-60/PerlMagick/t/png/write.t
ImageMagick-7.0.10-60/PerlMagick/t/ps/
ImageMagick-7.0.10-60/PerlMagick/t/ps/input.eps
ImageMagick-7.0.10-60/PerlMagick/t/ps/input.miff
ImageMagick-7.0.10-60/PerlMagick/t/ps/input.ps
ImageMagick-7.0.10-60/PerlMagick/t/ps/read.t
ImageMagick-7.0.10-60/PerlMagick/t/ps/write.t
ImageMagick-7.0.10-60/PerlMagick/t/rad/
ImageMagick-7.0.10-60/PerlMagick/t/rad/input.rad
ImageMagick-7.0.10-60/PerlMagick/t/rad/read.t
ImageMagick-7.0.10-60/PerlMagick/t/rad/write.t
ImageMagick-7.0.10-60/PerlMagick/t/read.t
ImageMagick-7.0.10-60/PerlMagick/t/reference/
ImageMagick-7.0.10-60/PerlMagick/t/reference/cgm/
ImageMagick-7.0.10-60/PerlMagick/t/reference/cgm/read.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/composite/
ImageMagick-7.0.10-60/PerlMagick/t/reference/composite/Add.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/composite/Atop.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/composite/Bumpmap.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/composite/Clear.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/composite/Copy.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/composite/CopyAlpha.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/composite/CopyBlue.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/composite/CopyGreen.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/composite/CopyRed.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/composite/Difference.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/composite/In.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/composite/Minus.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/composite/Multiply.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/composite/Out.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/composite/Over.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/composite/Plus.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/composite/Rotate.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/composite/Subtract.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/composite/Xor.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/filter/
ImageMagick-7.0.10-60/PerlMagick/t/reference/filter/AdaptiveThreshold.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/filter/Annotate.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/filter/Blur.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/filter/Border.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/filter/Channel.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/filter/Charcoal.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/filter/Chop.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/filter/ColorFloodfill.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/filter/Colorize.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/filter/Contrast.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/filter/Convolve.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/filter/Crop.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/filter/Despeckle.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/filter/Draw.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/filter/Edge.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/filter/Emboss.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/filter/Equalize.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/filter/Flip.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/filter/Flop.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/filter/Frame.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/filter/Gamma.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/filter/GaussianBlur.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/filter/Implode.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/filter/Level.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/filter/Magnify.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/filter/MatteFloodfill.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/filter/MedianFilter.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/filter/Minify.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/filter/Modulate.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/filter/MotionBlur.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/filter/Negate.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/filter/Normalize.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/filter/OilPaint.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/filter/Opaque.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/filter/Quantize.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/filter/QuantizeMono.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/filter/RadialBlur.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/filter/Raise.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/filter/ReduceNoise.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/filter/Resize.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/filter/Roll.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/filter/Rotate.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/filter/Sample.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/filter/Scale.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/filter/Segment.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/filter/Set.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/filter/Shade.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/filter/Sharpen.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/filter/Shave.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/filter/Shear.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/filter/SigmoidalContrast.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/filter/Solarize.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/filter/Swirl.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/filter/Threshold.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/filter/Trim.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/filter/UnsharpMask.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/filter/Wave.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/jng/
ImageMagick-7.0.10-60/PerlMagick/t/reference/jng/gray_idat_tmp.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/jng/gray_jdaa_tmp.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/jng/gray_prog_idat_tmp.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/jng/gray_prog_jdaa_tmp.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/jng/gray_prog_tmp.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/jng/gray_tmp.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/jng/idat_tmp.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/jng/input_gray.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/jng/input_gray_idat.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/jng/input_gray_jdaa.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/jng/input_gray_prog.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/jng/input_gray_prog_idat.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/jng/input_gray_prog_jdaa.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/jng/input_idat.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/jng/input_jdaa.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/jng/input_prog.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/jng/input_prog_idat.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/jng/input_prog_jdaa.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/jng/input_rose.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/jng/jdaa_tmp.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/jng/prog_idat_tmp.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/jng/prog_jdaa_tmp.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/jng/prog_tmp.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/jng/read_gray.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/jng/read_gray_idat.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/jng/read_gray_jdaa.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/jng/read_gray_prog.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/jng/read_gray_prog_idat.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/jng/read_gray_prog_jdaa.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/jng/read_idat.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/jng/read_jdaa.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/jng/read_prog.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/jng/read_prog_idat.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/jng/read_prog_jdaa.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/jng/write_gray.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/jng/write_gray_idat.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/jng/write_gray_jdaa.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/jng/write_gray_prog.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/jng/write_gray_prog_idat.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/jng/write_gray_prog_jdaa.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/jng/write_idat.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/jng/write_jdaa.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/jng/write_prog.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/jng/write_prog_idat.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/jng/write_prog_jdaa.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/jpeg/
ImageMagick-7.0.10-60/PerlMagick/t/reference/jpeg/read_non_interlaced.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/jpeg/read_plane_interlaced.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/jpeg/write_non_interlaced.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/jpeg/write_plane_interlaced.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/openjp2/
ImageMagick-7.0.10-60/PerlMagick/t/reference/openjp2/read_j2k.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/openjp2/read_jp2.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/openjp2/read_jpc.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/read/
ImageMagick-7.0.10-60/PerlMagick/t/reference/read/gradient.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/read/granite.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/read/input_avs.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/read/input_bmp.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/read/input_bmp24.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/read/input_cmyk.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/read/input_dcx.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/read/input_dib.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/read/input_fits.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/read/input_gif.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/read/input_gif87.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/read/input_gray.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/read/input_gray_lsb_08bit_mat.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/read/input_gray_lsb_double_mat.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/read/input_gray_msb_08bit_mat.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/read/input_ico.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/read/input_im1.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/read/input_im24.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/read/input_im8.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/read/input_mat.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/read/input_miff.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/read/input_mtv.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/read/input_null_DarkOrange.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/read/input_null_black.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/read/input_null_white.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/read/input_p7.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/read/input_pbm_p1.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/read/input_pbm_p4.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/read/input_pcx.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/read/input_pgm_p2.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/read/input_pgm_p5.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/read/input_pict.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/read/input_ppm_p3.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/read/input_ppm_p6.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/read/input_psd.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/read/input_rgb.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/read/input_rgb_lsb_08bit_mat.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/read/input_rgba.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/read/input_rle.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/read/input_sgi.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/read/input_tga.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/read/input_tile.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/read/input_tim.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/read/input_uyvy.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/read/input_viff.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/read/input_wbmp.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/read/input_wpg.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/read/input_xbm.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/read/input_xc_black.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/read/input_xpm.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/read/input_xwd.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/ttf/
ImageMagick-7.0.10-60/PerlMagick/t/reference/ttf/annotate.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/ttf/label.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/ttf/read.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/wmf/
ImageMagick-7.0.10-60/PerlMagick/t/reference/wmf/clock.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/wmf/wizard.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/cgm/
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/cgm/read.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/composite/
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/composite/Add.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/composite/Atop.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/composite/Bumpmap.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/composite/Clear.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/composite/Copy.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/composite/CopyAlpha.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/composite/CopyBlue.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/composite/CopyGreen.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/composite/CopyRed.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/composite/Difference.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/composite/In.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/composite/Minus.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/composite/Multiply.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/composite/Out.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/composite/Over.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/composite/Plus.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/composite/Rotate.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/composite/Subtract.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/composite/Xor.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/filter/
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/filter/AdaptiveThreshold.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/filter/Annotate.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/filter/Blur.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/filter/Border.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/filter/Channel.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/filter/Charcoal.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/filter/Chop.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/filter/ColorFloodfill.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/filter/Colorize.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/filter/Contrast.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/filter/Convolve.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/filter/Crop.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/filter/Despeckle.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/filter/Draw.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/filter/Edge.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/filter/Emboss.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/filter/Equalize.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/filter/Flip.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/filter/Flop.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/filter/Frame.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/filter/Gamma.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/filter/GaussianBlur.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/filter/Implode.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/filter/Level.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/filter/Magnify.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/filter/MatteFloodfill.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/filter/MedianFilter.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/filter/Minify.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/filter/Modulate.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/filter/MotionBlur.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/filter/Negate.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/filter/Normalize.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/filter/OilPaint.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/filter/Opaque.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/filter/Quantize.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/filter/RadialBlur.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/filter/Raise.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/filter/ReduceNoise.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/filter/Resize.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/filter/Roll.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/filter/Rotate.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/filter/Sample.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/filter/Scale.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/filter/Segment.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/filter/Set.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/filter/Shade.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/filter/Sharpen.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/filter/Shave.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/filter/Shear.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/filter/SigmoidalContrast.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/filter/Solarize.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/filter/Swirl.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/filter/Threshold.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/filter/Trim.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/filter/UnsharpMask.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/filter/Wave.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/jng/
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/jng/gray_idat_tmp.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/jng/gray_jdaa_tmp.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/jng/gray_prog_idat_tmp.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/jng/gray_prog_jdaa_tmp.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/jng/gray_prog_tmp.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/jng/gray_tmp.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/jng/idat_tmp.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/jng/input_gray.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/jng/input_gray_idat.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/jng/input_gray_jdaa.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/jng/input_gray_prog.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/jng/input_gray_prog_idat.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/jng/input_gray_prog_jdaa.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/jng/input_idat.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/jng/input_jdaa.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/jng/input_prog.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/jng/input_prog_idat.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/jng/input_prog_jdaa.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/jng/input_rose.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/jng/jdaa_tmp.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/jng/prog_idat_tmp.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/jng/prog_jdaa_tmp.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/jng/prog_tmp.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/jng/read_gray.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/jng/read_gray_idat.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/jng/read_gray_jdaa.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/jng/read_gray_prog.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/jng/read_gray_prog_idat.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/jng/read_gray_prog_jdaa.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/jng/read_idat.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/jng/read_jdaa.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/jng/read_prog.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/jng/read_prog_idat.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/jng/read_prog_jdaa.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/jng/write_gray.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/jng/write_gray_idat.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/jng/write_gray_jdaa.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/jng/write_gray_prog.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/jng/write_gray_prog_idat.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/jng/write_gray_prog_jdaa.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/jng/write_idat.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/jng/write_jdaa.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/jng/write_prog.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/jng/write_prog_idat.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/jng/write_prog_jdaa.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/jp2/
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/jp2/read_jp2.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/jp2/read_jpc.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/jp2/read_pgx.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/jpeg/
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/jpeg/read_non_interlaced.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/jpeg/read_plane_interlaced.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/jpeg/write_non_interlaced.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/jpeg/write_plane_interlaced.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/output_p7.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/read/
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/read/gradient.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/read/granite.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/read/input_avs.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/read/input_bmp.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/read/input_bmp24.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/read/input_cmyk.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/read/input_dcx.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/read/input_dib.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/read/input_fits.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/read/input_gif.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/read/input_gif87.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/read/input_gray.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/read/input_ico.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/read/input_im1.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/read/input_im24.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/read/input_im8.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/read/input_mat.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/read/input_miff.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/read/input_mtv.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/read/input_null_DarkOrange.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/read/input_null_black.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/read/input_null_white.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/read/input_p7.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/read/input_pbm_p1.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/read/input_pbm_p4.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/read/input_pcx.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/read/input_pgm_p2.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/read/input_pgm_p5.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/read/input_pict.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/read/input_ppm_p3.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/read/input_ppm_p6.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/read/input_psd.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/read/input_rgb.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/read/input_rgba.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/read/input_rle.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/read/input_sgi.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/read/input_tga.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/read/input_tile.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/read/input_tim.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/read/input_uyvy.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/read/input_viff.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/read/input_wbmp.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/read/input_wpg.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/read/input_xbm.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/read/input_xc_black.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/read/input_xpm.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/read/input_xwd.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/ttf/
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/ttf/annotate.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/ttf/label.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/ttf/read.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/wmf/
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/wmf/clock.miff
ImageMagick-7.0.10-60/PerlMagick/t/reference/write/wmf/wizard.miff
ImageMagick-7.0.10-60/PerlMagick/t/setattribute.t
ImageMagick-7.0.10-60/PerlMagick/t/subroutines.pl
ImageMagick-7.0.10-60/PerlMagick/t/tiff/
ImageMagick-7.0.10-60/PerlMagick/t/tiff/input_16.tiff
ImageMagick-7.0.10-60/PerlMagick/t/tiff/input_16_matte.tiff
ImageMagick-7.0.10-60/PerlMagick/t/tiff/input_256.tiff
ImageMagick-7.0.10-60/PerlMagick/t/tiff/input_256_matte.tiff
ImageMagick-7.0.10-60/PerlMagick/t/tiff/input_256_planar_contig.tiff
ImageMagick-7.0.10-60/PerlMagick/t/tiff/input_256_planar_separate.tiff
ImageMagick-7.0.10-60/PerlMagick/t/tiff/input_gray_12bit.tiff
ImageMagick-7.0.10-60/PerlMagick/t/tiff/input_gray_16bit.tiff
ImageMagick-7.0.10-60/PerlMagick/t/tiff/input_gray_4bit.tiff
ImageMagick-7.0.10-60/PerlMagick/t/tiff/input_gray_4bit_matte.tiff
ImageMagick-7.0.10-60/PerlMagick/t/tiff/input_gray_8bit.tiff
ImageMagick-7.0.10-60/PerlMagick/t/tiff/input_gray_8bit_matte.tiff
ImageMagick-7.0.10-60/PerlMagick/t/tiff/input_mono.tiff
ImageMagick-7.0.10-60/PerlMagick/t/tiff/input_truecolor.tiff
ImageMagick-7.0.10-60/PerlMagick/t/tiff/input_truecolor_16.tiff
ImageMagick-7.0.10-60/PerlMagick/t/tiff/input_truecolor_stripped.tiff
ImageMagick-7.0.10-60/PerlMagick/t/tiff/input_truecolor_tiled32x32.tiff
ImageMagick-7.0.10-60/PerlMagick/t/tiff/read.t
ImageMagick-7.0.10-60/PerlMagick/t/tiff/write.t
ImageMagick-7.0.10-60/PerlMagick/t/ttf/
ImageMagick-7.0.10-60/PerlMagick/t/ttf/input.ttf
ImageMagick-7.0.10-60/PerlMagick/t/ttf/read.t
ImageMagick-7.0.10-60/PerlMagick/t/wmf/
ImageMagick-7.0.10-60/PerlMagick/t/wmf/clock.wmf
ImageMagick-7.0.10-60/PerlMagick/t/wmf/read.t
ImageMagick-7.0.10-60/PerlMagick/t/wmf/wizard.wmf
ImageMagick-7.0.10-60/PerlMagick/t/write.t
ImageMagick-7.0.10-60/PerlMagick/t/x11/
ImageMagick-7.0.10-60/PerlMagick/t/x11/congrats.fig
ImageMagick-7.0.10-60/PerlMagick/t/x11/congrats.miff
ImageMagick-7.0.10-60/PerlMagick/t/x11/input.xwd
ImageMagick-7.0.10-60/PerlMagick/t/x11/read.t
ImageMagick-7.0.10-60/PerlMagick/t/x11/write.t
ImageMagick-7.0.10-60/PerlMagick/t/xfig/
ImageMagick-7.0.10-60/PerlMagick/t/xfig/input.fig
ImageMagick-7.0.10-60/PerlMagick/t/xfig/read.t
ImageMagick-7.0.10-60/PerlMagick/t/zlib/
ImageMagick-7.0.10-60/PerlMagick/t/zlib/input.miff
ImageMagick-7.0.10-60/PerlMagick/t/zlib/input.miff.gz
ImageMagick-7.0.10-60/PerlMagick/t/zlib/read.t
ImageMagick-7.0.10-60/PerlMagick/t/zlib/write.t
ImageMagick-7.0.10-60/PerlMagick/typemap
ImageMagick-7.0.10-60/PerlMagick/check.sh
ImageMagick-7.0.10-60/PerlMagick/Makefile.PL
ImageMagick-7.0.10-60/tests/
ImageMagick-7.0.10-60/tests/Makefile.am
ImageMagick-7.0.10-60/tests/drawtest.c
ImageMagick-7.0.10-60/tests/validate.c
ImageMagick-7.0.10-60/tests/validate.h
ImageMagick-7.0.10-60/tests/wandtest.c
ImageMagick-7.0.10-60/tests/common.shi
ImageMagick-7.0.10-60/tests/rose.pnm
ImageMagick-7.0.10-60/tests/input_256c.miff
ImageMagick-7.0.10-60/tests/input_bilevel.miff
ImageMagick-7.0.10-60/tests/input_gray.miff
ImageMagick-7.0.10-60/tests/input_truecolor.miff
ImageMagick-7.0.10-60/tests/sequence.miff
ImageMagick-7.0.10-60/tests/cli-colorspace.tap
ImageMagick-7.0.10-60/tests/cli-pipe.tap
ImageMagick-7.0.10-60/tests/validate-colorspace.tap
ImageMagick-7.0.10-60/tests/validate-compare.tap
ImageMagick-7.0.10-60/tests/validate-composite.tap
ImageMagick-7.0.10-60/tests/validate-convert.tap
ImageMagick-7.0.10-60/tests/validate-formats-disk.tap
ImageMagick-7.0.10-60/tests/validate-formats-map.tap
ImageMagick-7.0.10-60/tests/validate-formats-memory.tap
ImageMagick-7.0.10-60/tests/validate-identify.tap
ImageMagick-7.0.10-60/tests/validate-import.tap
ImageMagick-7.0.10-60/tests/validate-montage.tap
ImageMagick-7.0.10-60/tests/validate-stream.tap
ImageMagick-7.0.10-60/tests/drawtest.tap
ImageMagick-7.0.10-60/tests/wandtest.tap
ImageMagick-7.0.10-60/utilities/
ImageMagick-7.0.10-60/utilities/Makefile.am
ImageMagick-7.0.10-60/utilities/ImageMagick.1.in
ImageMagick-7.0.10-60/utilities/animate.1.in
ImageMagick-7.0.10-60/utilities/compare.1.in
ImageMagick-7.0.10-60/utilities/composite.1.in
ImageMagick-7.0.10-60/utilities/conjure.1.in
ImageMagick-7.0.10-60/utilities/convert.1.in
ImageMagick-7.0.10-60/utilities/display.1.in
ImageMagick-7.0.10-60/utilities/identify.1.in
ImageMagick-7.0.10-60/utilities/import.1.in
ImageMagick-7.0.10-60/utilities/magick-script.1.in
ImageMagick-7.0.10-60/utilities/magick.1.in
ImageMagick-7.0.10-60/utilities/mogrify.1.in
ImageMagick-7.0.10-60/utilities/montage.1.in
ImageMagick-7.0.10-60/utilities/stream.1.in
ImageMagick-7.0.10-60/utilities/magick.c
ImageMagick-7.0.10-60/utilities/ImageMagick.1
ImageMagick-7.0.10-60/utilities/animate.1
ImageMagick-7.0.10-60/utilities/compare.1
ImageMagick-7.0.10-60/utilities/composite.1
ImageMagick-7.0.10-60/utilities/conjure.1
ImageMagick-7.0.10-60/utilities/convert.1
ImageMagick-7.0.10-60/utilities/display.1
ImageMagick-7.0.10-60/utilities/identify.1
ImageMagick-7.0.10-60/utilities/import.1
ImageMagick-7.0.10-60/utilities/magick.1
ImageMagick-7.0.10-60/utilities/magick-script.1
ImageMagick-7.0.10-60/utilities/mogrify.1
ImageMagick-7.0.10-60/utilities/montage.1
ImageMagick-7.0.10-60/utilities/stream.1
ImageMagick-7.0.10-60/Makefile.am
ImageMagick-7.0.10-60/configure
ImageMagick-7.0.10-60/configure.ac
ImageMagick-7.0.10-60/ChangeLog
ImageMagick-7.0.10-60/aclocal.m4
ImageMagick-7.0.10-60/ImageMagick.spec.in
ImageMagick-7.0.10-60/Makefile.in
ImageMagick-7.0.10-60/common.shi.in
ImageMagick-7.0.10-60/magick.sh.in
ImageMagick-7.0.10-60/AUTHORS.txt
ImageMagick-7.0.10-60/LICENSE
ImageMagick-7.0.10-60/QuickStart.txt
ImageMagick-7.0.10-60/NOTICE
ImageMagick-7.0.10-60/Install-mac.txt
ImageMagick-7.0.10-60/Install-unix.txt
ImageMagick-7.0.10-60/Install-vms.txt
ImageMagick-7.0.10-60/Install-windows.txt
ImageMagick-7.0.10-60/Magickshr.opt
ImageMagick-7.0.10-60/NEWS.txt
ImageMagick-7.0.10-60/README.txt
ImageMagick-7.0.10-60/index.html
ImageMagick-7.0.10-60/winpath.sh
ImageMagick-7.0.10-60/images/
ImageMagick-7.0.10-60/images/ImageMagick.ico
ImageMagick-7.0.10-60/images/affine.png
ImageMagick-7.0.10-60/images/annotate.png
ImageMagick-7.0.10-60/images/arc.png
ImageMagick-7.0.10-60/images/atop.gif
ImageMagick-7.0.10-60/images/background.jpg
ImageMagick-7.0.10-60/images/bitcoin.svg
ImageMagick-7.0.10-60/images/black.png
ImageMagick-7.0.10-60/images/bluebells_clipped.jpg
ImageMagick-7.0.10-60/images/bluebells_darker.jpg
ImageMagick-7.0.10-60/images/bluebells_lin.jpg
ImageMagick-7.0.10-60/images/bluebells_log.jpg
ImageMagick-7.0.10-60/images/button.gif
ImageMagick-7.0.10-60/images/color-thresholding-gray.gif
ImageMagick-7.0.10-60/images/color-thresholding-hsv-rgb.gif
ImageMagick-7.0.10-60/images/color-thresholding-hsv.gif
ImageMagick-7.0.10-60/images/color-thresholding-rgb.gif
ImageMagick-7.0.10-60/images/color-thresholding.gif
ImageMagick-7.0.10-60/images/color-thresholding.jpg
ImageMagick-7.0.10-60/images/configure.jpg
ImageMagick-7.0.10-60/images/convex-hull-barn-closure.jpg
ImageMagick-7.0.10-60/images/convex-hull-barn.jpg
ImageMagick-7.0.10-60/images/convex-hull-blocks-closure.png
ImageMagick-7.0.10-60/images/convex-hull-blocks.png
ImageMagick-7.0.10-60/images/convex-hull.png
ImageMagick-7.0.10-60/images/cylinder_shaded.png
ImageMagick-7.0.10-60/images/difference.png
ImageMagick-7.0.10-60/images/examples.jpg
ImageMagick-7.0.10-60/images/frame.jpg
ImageMagick-7.0.10-60/images/fuzzy-magick.png
ImageMagick-7.0.10-60/images/gaussian-blur.png
ImageMagick-7.0.10-60/images/granite.png
ImageMagick-7.0.10-60/images/imade_art2.jpg
ImageMagick-7.0.10-60/images/label.gif
ImageMagick-7.0.10-60/images/logo-sm-flop.png
ImageMagick-7.0.10-60/images/logo-sm-fx.png
ImageMagick-7.0.10-60/images/logo-sm.png
ImageMagick-7.0.10-60/images/logo.jpg
ImageMagick-7.0.10-60/images/logo.png
ImageMagick-7.0.10-60/images/montage.jpg
ImageMagick-7.0.10-60/images/mountains-clahe.jpg
ImageMagick-7.0.10-60/images/mountains-equalize.jpg
ImageMagick-7.0.10-60/images/mountains.jpg
ImageMagick-7.0.10-60/images/navy.png
ImageMagick-7.0.10-60/images/objects.gif
ImageMagick-7.0.10-60/images/objects.jpg
ImageMagick-7.0.10-60/images/objects.png
ImageMagick-7.0.10-60/images/over.gif
ImageMagick-7.0.10-60/images/patterns/
ImageMagick-7.0.10-60/images/patterns/bricks.png
ImageMagick-7.0.10-60/images/patterns/checkerboard.png
ImageMagick-7.0.10-60/images/patterns/circles.png
ImageMagick-7.0.10-60/images/patterns/crosshatch.png
ImageMagick-7.0.10-60/images/patterns/crosshatch30.png
ImageMagick-7.0.10-60/images/patterns/crosshatch45.png
ImageMagick-7.0.10-60/images/patterns/fishscales.png
ImageMagick-7.0.10-60/images/patterns/gray0.png
ImageMagick-7.0.10-60/images/patterns/gray10.png
ImageMagick-7.0.10-60/images/patterns/gray100.png
ImageMagick-7.0.10-60/images/patterns/gray15.png
ImageMagick-7.0.10-60/images/patterns/gray20.png
ImageMagick-7.0.10-60/images/patterns/gray25.png
ImageMagick-7.0.10-60/images/patterns/gray30.png
ImageMagick-7.0.10-60/images/patterns/gray35.png
ImageMagick-7.0.10-60/images/patterns/gray40.png
ImageMagick-7.0.10-60/images/patterns/gray45.png
ImageMagick-7.0.10-60/images/patterns/gray5.png
ImageMagick-7.0.10-60/images/patterns/gray50.png
ImageMagick-7.0.10-60/images/patterns/gray55.png
ImageMagick-7.0.10-60/images/patterns/gray60.png
ImageMagick-7.0.10-60/images/patterns/gray65.png
ImageMagick-7.0.10-60/images/patterns/gray70.png
ImageMagick-7.0.10-60/images/patterns/gray75.png
ImageMagick-7.0.10-60/images/patterns/gray80.png
ImageMagick-7.0.10-60/images/patterns/gray85.png
ImageMagick-7.0.10-60/images/patterns/gray90.png
ImageMagick-7.0.10-60/images/patterns/gray95.png
ImageMagick-7.0.10-60/images/patterns/hexagons.png
ImageMagick-7.0.10-60/images/patterns/horizontal.png
ImageMagick-7.0.10-60/images/patterns/horizontal2.png
ImageMagick-7.0.10-60/images/patterns/horizontal3.png
ImageMagick-7.0.10-60/images/patterns/horizontalsaw.png
ImageMagick-7.0.10-60/images/patterns/hs_bdiagonal.png
ImageMagick-7.0.10-60/images/patterns/hs_cross.png
ImageMagick-7.0.10-60/images/patterns/hs_diagcross.png
ImageMagick-7.0.10-60/images/patterns/hs_fdiagonal.png
ImageMagick-7.0.10-60/images/patterns/hs_horizontal.png
ImageMagick-7.0.10-60/images/patterns/hs_vertical.png
ImageMagick-7.0.10-60/images/patterns/left30.png
ImageMagick-7.0.10-60/images/patterns/left45.png
ImageMagick-7.0.10-60/images/patterns/leftshingle.png
ImageMagick-7.0.10-60/images/patterns/octagons.png
ImageMagick-7.0.10-60/images/patterns/right30.png
ImageMagick-7.0.10-60/images/patterns/right45.png
ImageMagick-7.0.10-60/images/patterns/rightshingle.png
ImageMagick-7.0.10-60/images/patterns/smallfishscales.png
ImageMagick-7.0.10-60/images/patterns/vertical.png
ImageMagick-7.0.10-60/images/patterns/vertical2.png
ImageMagick-7.0.10-60/images/patterns/vertical3.png
ImageMagick-7.0.10-60/images/patterns/verticalbricks.png
ImageMagick-7.0.10-60/images/patterns/verticalleftshingle.png
ImageMagick-7.0.10-60/images/patterns/verticalrightshingle.png
ImageMagick-7.0.10-60/images/patterns/verticalsaw.png
ImageMagick-7.0.10-60/images/piechart.png
ImageMagick-7.0.10-60/images/radial-gradient.png
ImageMagick-7.0.10-60/images/reconstruct.jpg
ImageMagick-7.0.10-60/images/red-ball.png
ImageMagick-7.0.10-60/images/red-circle.png
ImageMagick-7.0.10-60/images/right.gif
ImageMagick-7.0.10-60/images/rose-over.png
ImageMagick-7.0.10-60/images/rose-sigmoidal.png
ImageMagick-7.0.10-60/images/rose.jpg
ImageMagick-7.0.10-60/images/rose.png
ImageMagick-7.0.10-60/images/rose.pnm
ImageMagick-7.0.10-60/images/script.png
ImageMagick-7.0.10-60/images/smile.gif
ImageMagick-7.0.10-60/images/sponsor.jpg
ImageMagick-7.0.10-60/images/sprite.jpg
ImageMagick-7.0.10-60/images/t-shirt.png
ImageMagick-7.0.10-60/images/wand.ico
ImageMagick-7.0.10-60/images/wand.png
ImageMagick-7.0.10-60/images/white-highlight.png
ImageMagick-7.0.10-60/images/wizard.jpg
ImageMagick-7.0.10-60/images/wizard.png
ImageMagick-7.0.10-60/scripts/
ImageMagick-7.0.10-60/scripts/Makefile.am
ImageMagick-7.0.10-60/scripts/format_c_api_docs
ImageMagick-7.0.10-60/scripts/txt2html
ImageMagick-7.0.10-60/scripts/xsnap
ImageMagick-7.0.10-60/www/
ImageMagick-7.0.10-60/www/Magick++/
ImageMagick-7.0.10-60/www/Magick++/Blob.html
ImageMagick-7.0.10-60/www/Magick++/COPYING
ImageMagick-7.0.10-60/www/Magick++/Cache.fig
ImageMagick-7.0.10-60/www/Magick++/Cache.png
ImageMagick-7.0.10-60/www/Magick++/Cache.svg
ImageMagick-7.0.10-60/www/Magick++/ChangeLog.html
ImageMagick-7.0.10-60/www/Magick++/CoderInfo.html
ImageMagick-7.0.10-60/www/Magick++/Color.html
ImageMagick-7.0.10-60/www/Magick++/Documentation.html
ImageMagick-7.0.10-60/www/Magick++/Drawable.html
ImageMagick-7.0.10-60/www/Magick++/Drawable_example_1.png
ImageMagick-7.0.10-60/www/Magick++/Enumerations.html
ImageMagick-7.0.10-60/www/Magick++/Exception.html
ImageMagick-7.0.10-60/www/Magick++/FormatCharacters.html
ImageMagick-7.0.10-60/www/Magick++/Future.html
ImageMagick-7.0.10-60/www/Magick++/Geometry.html
ImageMagick-7.0.10-60/www/Magick++/Image++.html
ImageMagick-7.0.10-60/www/Magick++/Image.fig
ImageMagick-7.0.10-60/www/Magick++/Image.html
ImageMagick-7.0.10-60/www/Magick++/Image.png
ImageMagick-7.0.10-60/www/Magick++/ImageDesign.html
ImageMagick-7.0.10-60/www/Magick++/ImageMagick.png
ImageMagick-7.0.10-60/www/Magick++/Install.html
ImageMagick-7.0.10-60/www/Magick++/Magick++.png
ImageMagick-7.0.10-60/www/Magick++/Montage.html
ImageMagick-7.0.10-60/www/Magick++/NEWS.html
ImageMagick-7.0.10-60/www/Magick++/PixelPacket.html
ImageMagick-7.0.10-60/www/Magick++/Pixels.html
ImageMagick-7.0.10-60/www/Magick++/Quantum.html
ImageMagick-7.0.10-60/www/Magick++/README.txt
ImageMagick-7.0.10-60/www/Magick++/STL.html
ImageMagick-7.0.10-60/www/Magick++/TypeMetric.html
ImageMagick-7.0.10-60/www/Magick++/index.html
ImageMagick-7.0.10-60/www/Magick++/magick.css
ImageMagick-7.0.10-60/www/Magick++/montage-sample-framed.jpg
ImageMagick-7.0.10-60/www/Magick++/right_triangle.png
ImageMagick-7.0.10-60/www/Magick++/thumbnail-anatomy-framed.fig
ImageMagick-7.0.10-60/www/Magick++/thumbnail-anatomy-framed.jpg
ImageMagick-7.0.10-60/www/Magick++/thumbnail-anatomy-plain.fig
ImageMagick-7.0.10-60/www/Magick++/thumbnail-anatomy-plain.jpg
ImageMagick-7.0.10-60/www/Magick++/thumbnail-sample-framed.jpg
ImageMagick-7.0.10-60/www/Magick++/thumbnail-sample-plain.jpg
ImageMagick-7.0.10-60/www/api/
ImageMagick-7.0.10-60/www/api/Magick++/
ImageMagick-7.0.10-60/www/api/Magick++/BlobRef_8cpp.html
ImageMagick-7.0.10-60/www/api/Magick++/BlobRef_8cpp_source.html
ImageMagick-7.0.10-60/www/api/Magick++/BlobRef_8h.html
ImageMagick-7.0.10-60/www/api/Magick++/BlobRef_8h_source.html
ImageMagick-7.0.10-60/www/api/Magick++/Blob_8cpp.html
ImageMagick-7.0.10-60/www/api/Magick++/Blob_8cpp_source.html
ImageMagick-7.0.10-60/www/api/Magick++/Blob_8h.html
ImageMagick-7.0.10-60/www/api/Magick++/Blob_8h_source.html
ImageMagick-7.0.10-60/www/api/Magick++/CoderInfo_8cpp.html
ImageMagick-7.0.10-60/www/api/Magick++/CoderInfo_8cpp_source.html
ImageMagick-7.0.10-60/www/api/Magick++/CoderInfo_8h.html
ImageMagick-7.0.10-60/www/api/Magick++/CoderInfo_8h_source.html
ImageMagick-7.0.10-60/www/api/Magick++/Color_8cpp.html
ImageMagick-7.0.10-60/www/api/Magick++/Color_8cpp_source.html
ImageMagick-7.0.10-60/www/api/Magick++/Color_8h.html
ImageMagick-7.0.10-60/www/api/Magick++/Color_8h_source.html
ImageMagick-7.0.10-60/www/api/Magick++/Drawable_8cpp.html
ImageMagick-7.0.10-60/www/api/Magick++/Drawable_8cpp_source.html
ImageMagick-7.0.10-60/www/api/Magick++/Drawable_8h.html
ImageMagick-7.0.10-60/www/api/Magick++/Drawable_8h_source.html
ImageMagick-7.0.10-60/www/api/Magick++/Exception_8cpp.html
ImageMagick-7.0.10-60/www/api/Magick++/Exception_8cpp_source.html
ImageMagick-7.0.10-60/www/api/Magick++/Exception_8h.html
ImageMagick-7.0.10-60/www/api/Magick++/Exception_8h_source.html
ImageMagick-7.0.10-60/www/api/Magick++/Functions_8cpp.html
ImageMagick-7.0.10-60/www/api/Magick++/Functions_8cpp_source.html
ImageMagick-7.0.10-60/www/api/Magick++/Functions_8h.html
ImageMagick-7.0.10-60/www/api/Magick++/Functions_8h_source.html
ImageMagick-7.0.10-60/www/api/Magick++/Geometry_8cpp.html
ImageMagick-7.0.10-60/www/api/Magick++/Geometry_8cpp_source.html
ImageMagick-7.0.10-60/www/api/Magick++/Geometry_8h.html
ImageMagick-7.0.10-60/www/api/Magick++/Geometry_8h_source.html
ImageMagick-7.0.10-60/www/api/Magick++/ImageRef_8cpp.html
ImageMagick-7.0.10-60/www/api/Magick++/ImageRef_8cpp_source.html
ImageMagick-7.0.10-60/www/api/Magick++/ImageRef_8h.html
ImageMagick-7.0.10-60/www/api/Magick++/ImageRef_8h_source.html
ImageMagick-7.0.10-60/www/api/Magick++/Image_8cpp.html
ImageMagick-7.0.10-60/www/api/Magick++/Image_8cpp_source.html
ImageMagick-7.0.10-60/www/api/Magick++/Image_8h.html
ImageMagick-7.0.10-60/www/api/Magick++/Image_8h_source.html
ImageMagick-7.0.10-60/www/api/Magick++/Include_8h.html
ImageMagick-7.0.10-60/www/api/Magick++/Include_8h_source.html
ImageMagick-7.0.10-60/www/api/Magick++/Magick_09_09_8h.html
ImageMagick-7.0.10-60/www/api/Magick++/Magick_09_09_8h_source.html
ImageMagick-7.0.10-60/www/api/Magick++/Montage_8cpp.html
ImageMagick-7.0.10-60/www/api/Magick++/Montage_8cpp_source.html
ImageMagick-7.0.10-60/www/api/Magick++/Montage_8h.html
ImageMagick-7.0.10-60/www/api/Magick++/Montage_8h_source.html
ImageMagick-7.0.10-60/www/api/Magick++/Options_8cpp.html
ImageMagick-7.0.10-60/www/api/Magick++/Options_8cpp_source.html
ImageMagick-7.0.10-60/www/api/Magick++/Options_8h.html
ImageMagick-7.0.10-60/www/api/Magick++/Options_8h_source.html
ImageMagick-7.0.10-60/www/api/Magick++/Pixels_8cpp.html
ImageMagick-7.0.10-60/www/api/Magick++/Pixels_8cpp_source.html
ImageMagick-7.0.10-60/www/api/Magick++/Pixels_8h.html
ImageMagick-7.0.10-60/www/api/Magick++/Pixels_8h_source.html
ImageMagick-7.0.10-60/www/api/Magick++/ResourceLimits_8cpp.html
ImageMagick-7.0.10-60/www/api/Magick++/ResourceLimits_8cpp_source.html
ImageMagick-7.0.10-60/www/api/Magick++/ResourceLimits_8h.html
ImageMagick-7.0.10-60/www/api/Magick++/ResourceLimits_8h_source.html
ImageMagick-7.0.10-60/www/api/Magick++/STL_8cpp.html
ImageMagick-7.0.10-60/www/api/Magick++/STL_8cpp_source.html
ImageMagick-7.0.10-60/www/api/Magick++/STL_8h.html
ImageMagick-7.0.10-60/www/api/Magick++/STL_8h_source.html
ImageMagick-7.0.10-60/www/api/Magick++/SecurityPolicy_8cpp.html
ImageMagick-7.0.10-60/www/api/Magick++/SecurityPolicy_8cpp_source.html
ImageMagick-7.0.10-60/www/api/Magick++/SecurityPolicy_8h.html
ImageMagick-7.0.10-60/www/api/Magick++/SecurityPolicy_8h_source.html
ImageMagick-7.0.10-60/www/api/Magick++/Statistic_8cpp.html
ImageMagick-7.0.10-60/www/api/Magick++/Statistic_8cpp_source.html
ImageMagick-7.0.10-60/www/api/Magick++/Statistic_8h.html
ImageMagick-7.0.10-60/www/api/Magick++/Statistic_8h_source.html
ImageMagick-7.0.10-60/www/api/Magick++/Thread_8cpp.html
ImageMagick-7.0.10-60/www/api/Magick++/Thread_8cpp_source.html
ImageMagick-7.0.10-60/www/api/Magick++/Thread_8h.html
ImageMagick-7.0.10-60/www/api/Magick++/Thread_8h_source.html
ImageMagick-7.0.10-60/www/api/Magick++/TypeMetric_8cpp.html
ImageMagick-7.0.10-60/www/api/Magick++/TypeMetric_8cpp_source.html
ImageMagick-7.0.10-60/www/api/Magick++/TypeMetric_8h.html
ImageMagick-7.0.10-60/www/api/Magick++/TypeMetric_8h_source.html
ImageMagick-7.0.10-60/www/api/Magick++/analyze_8cpp.html
ImageMagick-7.0.10-60/www/api/Magick++/analyze_8cpp_source.html
ImageMagick-7.0.10-60/www/api/Magick++/annotated.html
ImageMagick-7.0.10-60/www/api/Magick++/button_8cpp.html
ImageMagick-7.0.10-60/www/api/Magick++/button_8cpp_source.html
ImageMagick-7.0.10-60/www/api/Magick++/classEncoderFormat.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1Blob.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1BlobRef.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1ChannelMoments.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1ChannelPerceptualHash.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1ChannelStatistics.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1CoderInfo.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1Color.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1ColorCMYK.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1ColorGray.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1ColorHSL.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1ColorMono.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1ColorRGB.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1ColorYUV.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1Coordinate.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1Drawable.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1DrawableAffine.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1DrawableAlpha.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1DrawableArc.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1DrawableBase.html
ImageMagick-7.0.10-60/www/api/Magick++/classes.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1DrawableBezier.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1DrawableBorderColor.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1DrawableCircle.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1DrawableClipPath.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1DrawableClipRule.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1DrawableClipUnits.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1DrawableColor.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1DrawableCompositeImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1DrawableDensity.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1DrawableEllipse.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1DrawableFillColor.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1DrawableFillOpacity.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1DrawableFillPatternUrl.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1DrawableFillRule.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1DrawableFont.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1DrawableGravity.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1DrawableLine.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1DrawableMiterLimit.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1DrawablePath.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1DrawablePoint.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1DrawablePointSize.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1DrawablePolygon.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1DrawablePolyline.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1DrawablePopClipPath.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1DrawablePopGraphicContext.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1DrawablePopPattern.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1DrawablePushClipPath.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1DrawablePushGraphicContext.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1DrawablePushPattern.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1DrawableRectangle.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1DrawableRotation.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1DrawableRoundRectangle.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1DrawableScaling.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1DrawableSkewX.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1DrawableSkewY.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1DrawableStrokeAntialias.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1DrawableStrokeColor.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1DrawableStrokeDashArray.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1DrawableStrokeDashOffset.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1DrawableStrokeLineCap.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1DrawableStrokeLineJoin.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1DrawableStrokeOpacity.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1DrawableStrokePatternUrl.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1DrawableStrokeWidth.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1DrawableText.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1DrawableTextAlignment.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1DrawableTextAntialias.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1DrawableTextDecoration.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1DrawableTextDirection.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1DrawableTextInterlineSpacing.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1DrawableTextInterwordSpacing.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1DrawableTextKerning.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1DrawableTextUnderColor.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1DrawableTranslation.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1DrawableViewbox.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1Error.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1ErrorBlob.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1ErrorCache.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1ErrorCoder.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1ErrorConfigure.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1ErrorCorruptImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1ErrorDelegate.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1ErrorDraw.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1ErrorFileOpen.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1ErrorImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1ErrorMissingDelegate.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1ErrorModule.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1ErrorMonitor.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1ErrorOption.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1ErrorPolicy.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1ErrorRegistry.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1ErrorResourceLimit.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1ErrorStream.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1ErrorType.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1ErrorUndefined.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1ErrorXServer.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1Exception.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1Geometry.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1Image.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1ImageMoments.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1ImagePerceptualHash.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1ImageRef.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1ImageStatistics.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1Montage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1MontageFramed.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1MutexLock.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1Offset.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1Options.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1PathArcAbs.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1PathArcArgs.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1PathArcRel.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1PathClosePath.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1PathCurvetoAbs.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1PathCurvetoArgs.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1PathCurvetoRel.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1PathLinetoAbs.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1PathLinetoHorizontalAbs.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1PathLinetoHorizontalRel.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1PathLinetoRel.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1PathLinetoVerticalAbs.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1PathLinetoVerticalRel.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1PathMovetoAbs.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1PathMovetoRel.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1PathQuadraticCurvetoAbs.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1PathQuadraticCurvetoArgs.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1PathQuadraticCurvetoRel.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1PathSmoothCurvetoAbs.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1PathSmoothCurvetoRel.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1PathSmoothQuadraticCurvetoAbs.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1PathSmoothQuadraticCurvetoRel.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1PixelData.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1Pixels.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1Point.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1ReadOptions.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1ResourceLimits.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1SecurityPolicy.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1TypeMetric.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1VPath.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1VPathBase.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1Warning.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1WarningBlob.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1WarningCache.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1WarningCoder.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1WarningConfigure.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1WarningCorruptImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1WarningDelegate.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1WarningDraw.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1WarningFileOpen.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1WarningImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1WarningMissingDelegate.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1WarningModule.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1WarningMonitor.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1WarningOption.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1WarningPolicy.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1WarningRegistry.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1WarningResourceLimit.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1WarningStream.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1WarningType.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1WarningUndefined.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1WarningXServer.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1adaptiveBlurImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1adaptiveThresholdImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1addNoiseImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1adjoinImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1affineTransformImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1alphaFlagImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1alphaImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1animationDelayImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1animationIterationsImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1annotateImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1backgroundColorImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1backgroundTextureImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1blurImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1borderColorImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1borderImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1boxColorImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1cdlImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1channelImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1mapImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1charcoalImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1chopImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1chromaBluePrimaryImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1chromaGreenPrimaryImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1chromaRedPrimaryImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1chromaWhitePointImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1colorFuzzImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1colorMapImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1colorMatrixImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1colorSpaceImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1colorizeImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1commentImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1composeImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1compositeImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1compressTypeImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1contrastImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1cropImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1cycleColormapImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1densityImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1depthImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1despeckleImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1distortImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1drawImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1edgeImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1embossImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1endianImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1enhanceImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1equalizeImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1fileNameImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1fillColorImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1filterTypeImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1flipImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1floodFillAlphaImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1floodFillColorImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1floodFillTextureImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1flopImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1fontImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1fontPointsizeImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1frameImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1gammaImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1gaussianBlurImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1gifDisposeMethodImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1haldClutImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1implodeImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1interlaceTypeImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1inverseFourierTransformImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1isValidImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1labelImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1levelImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1magickImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1magnifyImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1matteColorImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1medianConvolveImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1mergeLayersImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1minifyImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1modulateImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1monochromeImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1negateImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1normalizeImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1oilPaintImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1opaqueImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1pageImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1penColorImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1penTextureImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1pixelColorImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1qualityImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1quantizeColorSpaceImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1quantizeColorsImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1quantizeDitherImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1quantizeImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1quantizeTreeDepthImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1raiseImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1reduceNoiseImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1renderingIntentImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1resizeImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1resolutionUnitsImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1rollImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1rotateImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1sampleImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1scaleImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1sceneImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1segmentImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1shadeImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1shadowImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1sharpenImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1shaveImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1shearImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1sigmoidalContrastImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1sizeImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1solarizeImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1spliceImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1spreadImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1steganoImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1stereoImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1stripImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1strokeColorImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1subImageImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1subRangeImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1swirlImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1textAntiAliasImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1textureImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1thresholdImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1transparentImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1trimImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1typeImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1verboseImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1waveImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1x11DisplayImage.html
ImageMagick-7.0.10-60/www/api/Magick++/classMagick_1_1zoomImage.html
ImageMagick-7.0.10-60/www/api/Magick++/demo_8cpp.html
ImageMagick-7.0.10-60/www/api/Magick++/demo_8cpp_source.html
ImageMagick-7.0.10-60/www/api/Magick++/detrans_8cpp.html
ImageMagick-7.0.10-60/www/api/Magick++/detrans_8cpp_source.html
ImageMagick-7.0.10-60/www/api/Magick++/encoder__format_8h.html
ImageMagick-7.0.10-60/www/api/Magick++/encoder__format_8h_source.html
ImageMagick-7.0.10-60/www/api/Magick++/files.html
ImageMagick-7.0.10-60/www/api/Magick++/flip_8cpp.html
ImageMagick-7.0.10-60/www/api/Magick++/flip_8cpp_source.html
ImageMagick-7.0.10-60/www/api/Magick++/functions.html
ImageMagick-7.0.10-60/www/api/Magick++/globals.html
ImageMagick-7.0.10-60/www/api/Magick++/gravity_8cpp.html
ImageMagick-7.0.10-60/www/api/Magick++/gravity_8cpp_source.html
ImageMagick-7.0.10-60/www/api/Magick++/hierarchy.html
ImageMagick-7.0.10-60/www/api/Magick++/index.html
ImageMagick-7.0.10-60/www/api/Magick++/inherits.html
ImageMagick-7.0.10-60/www/api/Magick++/namespaceMagick.html
ImageMagick-7.0.10-60/www/api/Magick++/namespaceMagickCore.html
ImageMagick-7.0.10-60/www/api/Magick++/namespacemembers.html
ImageMagick-7.0.10-60/www/api/Magick++/namespaces.html
ImageMagick-7.0.10-60/www/api/Magick++/piddle_8cpp.html
ImageMagick-7.0.10-60/www/api/Magick++/piddle_8cpp_source.html
ImageMagick-7.0.10-60/www/api/Magick++/shapes_8cpp.html
ImageMagick-7.0.10-60/www/api/Magick++/shapes_8cpp_source.html
ImageMagick-7.0.10-60/www/api/Magick++/zoom_8cpp.html
ImageMagick-7.0.10-60/www/api/Magick++/zoom_8cpp_source.html
ImageMagick-7.0.10-60/www/api/magick++-classes.html
ImageMagick-7.0.10-60/www/api/magick-deprecate.html
ImageMagick-7.0.10-60/www/api/magick.html
ImageMagick-7.0.10-60/www/api/magick-image.html
ImageMagick-7.0.10-60/www/api/magick-property.html
ImageMagick-7.0.10-60/www/api/magick-wand.html
ImageMagick-7.0.10-60/www/api/memory.html
ImageMagick-7.0.10-60/www/api/mime.html
ImageMagick-7.0.10-60/www/api/module.html
ImageMagick-7.0.10-60/www/api/mogrify.html
ImageMagick-7.0.10-60/www/api/monitor.html
ImageMagick-7.0.10-60/www/api/montage.html
ImageMagick-7.0.10-60/www/api/morphology.html
ImageMagick-7.0.10-60/www/api/paint.html
ImageMagick-7.0.10-60/www/api/pixel-iterator.html
ImageMagick-7.0.10-60/www/api/pixel-wand.html
ImageMagick-7.0.10-60/www/api/profile.html
ImageMagick-7.0.10-60/www/api/property.html
ImageMagick-7.0.10-60/www/api/quantize.html
ImageMagick-7.0.10-60/www/api/registry.html
ImageMagick-7.0.10-60/www/api/resize.html
ImageMagick-7.0.10-60/www/api/resource.html
ImageMagick-7.0.10-60/www/api/segment.html
ImageMagick-7.0.10-60/www/api/shear.html
ImageMagick-7.0.10-60/www/api/signature.html
ImageMagick-7.0.10-60/www/api/statistic.html
ImageMagick-7.0.10-60/www/api/stream.html
ImageMagick-7.0.10-60/www/api/transform.html
ImageMagick-7.0.10-60/www/api/version.html
ImageMagick-7.0.10-60/www/api/wand-view.html
ImageMagick-7.0.10-60/www/api/animate.html
ImageMagick-7.0.10-60/www/api/annotate.html
ImageMagick-7.0.10-60/www/api/attribute.html
ImageMagick-7.0.10-60/www/api/blob.html
ImageMagick-7.0.10-60/www/api/cache.html
ImageMagick-7.0.10-60/www/api/cache-view.html
ImageMagick-7.0.10-60/www/api/channel.html
ImageMagick-7.0.10-60/www/api/cipher.html
ImageMagick-7.0.10-60/www/api/color.html
ImageMagick-7.0.10-60/www/api/colormap.html
ImageMagick-7.0.10-60/www/api/colorspace.html
ImageMagick-7.0.10-60/www/api/compare.html
ImageMagick-7.0.10-60/www/api/composite.html
ImageMagick-7.0.10-60/www/api/constitute.html
ImageMagick-7.0.10-60/www/api/decorate.html
ImageMagick-7.0.10-60/www/api/deprecate.html
ImageMagick-7.0.10-60/www/api/display.html
ImageMagick-7.0.10-60/www/api/distort.html
ImageMagick-7.0.10-60/www/api/draw.html
ImageMagick-7.0.10-60/www/api/drawing-wand.html
ImageMagick-7.0.10-60/www/api/effect.html
ImageMagick-7.0.10-60/www/api/enhance.html
ImageMagick-7.0.10-60/www/api/exception.html
ImageMagick-7.0.10-60/www/api/feature.html
ImageMagick-7.0.10-60/www/api/fourier.html
ImageMagick-7.0.10-60/www/api/fx.html
ImageMagick-7.0.10-60/www/api/histogram.html
ImageMagick-7.0.10-60/www/api/image.html
ImageMagick-7.0.10-60/www/api/Image++.html
ImageMagick-7.0.10-60/www/api/image-view.html
ImageMagick-7.0.10-60/www/api/layer.html
ImageMagick-7.0.10-60/www/api/list.html
ImageMagick-7.0.10-60/www/assets/
ImageMagick-7.0.10-60/www/assets/.magick-template.css.swp
ImageMagick-7.0.10-60/www/assets/magick.css
ImageMagick-7.0.10-60/www/assets/magick.js
ImageMagick-7.0.10-60/www/contact.html
ImageMagick-7.0.10-60/www/convex-hull.html
ImageMagick-7.0.10-60/www/develop.html
ImageMagick-7.0.10-60/www/distribute-pixel-cache.html
ImageMagick-7.0.10-60/www/examples.html
ImageMagick-7.0.10-60/www/export.html
ImageMagick-7.0.10-60/www/fx.html
ImageMagick-7.0.10-60/www/history.html
ImageMagick-7.0.10-60/www/ImageMagickObject.html
ImageMagick-7.0.10-60/www/support.html
ImageMagick-7.0.10-60/www/contrib/
ImageMagick-7.0.10-60/www/contrib/color-converter.html
ImageMagick-7.0.10-60/www/contrib/color-swatch.html
ImageMagick-7.0.10-60/www/gradient.html
ImageMagick-7.0.10-60/www/identify.html
ImageMagick-7.0.10-60/www/index.html
ImageMagick-7.0.10-60/www/favicon.ico
ImageMagick-7.0.10-60/www/install-source.html
ImageMagick-7.0.10-60/www/jp2.html
ImageMagick-7.0.10-60/www/license.html
ImageMagick-7.0.10-60/www/links.html
ImageMagick-7.0.10-60/www/magick++.html
ImageMagick-7.0.10-60/www/magick.html
ImageMagick-7.0.10-60/www/magick-script.html
ImageMagick-7.0.10-60/www/magick-vector-graphics.html
ImageMagick-7.0.10-60/www/magick-wand.html
ImageMagick-7.0.10-60/www/miff.html
ImageMagick-7.0.10-60/www/mirror.html
ImageMagick-7.0.10-60/www/mogrify.html
ImageMagick-7.0.10-60/www/montage.html
ImageMagick-7.0.10-60/www/motion-picture.html
ImageMagick-7.0.10-60/www/news.html
ImageMagick-7.0.10-60/www/opencl.html
ImageMagick-7.0.10-60/www/openmp.html
ImageMagick-7.0.10-60/www/perl-magick.html
ImageMagick-7.0.10-60/www/porting.html
ImageMagick-7.0.10-60/www/quantize.html
ImageMagick-7.0.10-60/www/resources.html
ImageMagick-7.0.10-60/www/search.html
ImageMagick-7.0.10-60/www/security-policy.html
ImageMagick-7.0.10-60/www/sitemap.html
ImageMagick-7.0.10-60/www/stream.html
ImageMagick-7.0.10-60/www/webp.html
ImageMagick-7.0.10-60/www/source/
ImageMagick-7.0.10-60/www/source/analyze.c
ImageMagick-7.0.10-60/www/source/coder.xml
ImageMagick-7.0.10-60/www/source/colors.xml
ImageMagick-7.0.10-60/www/source/configure.xml
ImageMagick-7.0.10-60/www/source/contrast.c
ImageMagick-7.0.10-60/www/source/core.c
ImageMagick-7.0.10-60/www/source/core/
ImageMagick-7.0.10-60/www/source/core/sigmoidal-contrast.c
ImageMagick-7.0.10-60/www/source/delegates.xml
ImageMagick-7.0.10-60/www/source/english.xml
ImageMagick-7.0.10-60/www/source/examples.pl
ImageMagick-7.0.10-60/www/source/francais.xml
ImageMagick-7.0.10-60/www/source/incantation.msl
ImageMagick-7.0.10-60/www/source/locale.xml
ImageMagick-7.0.10-60/www/source/log.xml
ImageMagick-7.0.10-60/www/source/magic.xml
ImageMagick-7.0.10-60/www/source/mgk.c
ImageMagick-7.0.10-60/www/source/mime.xml
ImageMagick-7.0.10-60/www/source/piechart.mvg
ImageMagick-7.0.10-60/www/source/piechart.svg
ImageMagick-7.0.10-60/www/source/policy.xml
ImageMagick-7.0.10-60/www/source/quantization-table.xml
ImageMagick-7.0.10-60/www/source/thresholds.xml
ImageMagick-7.0.10-60/www/source/type-apple.xml
ImageMagick-7.0.10-60/www/source/type-dejavu.xml
ImageMagick-7.0.10-60/www/source/type-ghostscript.xml
ImageMagick-7.0.10-60/www/source/type-urw-base35.xml
ImageMagick-7.0.10-60/www/source/type-windows.xml
ImageMagick-7.0.10-60/www/source/type.xml
ImageMagick-7.0.10-60/www/source/wand.c
ImageMagick-7.0.10-60/www/source/wand/
ImageMagick-7.0.10-60/www/source/wand/sigmoidal-contrast.c
ImageMagick-7.0.10-60/www/wand.png
ImageMagick-7.0.10-60/www/advanced-unix-installation.html
ImageMagick-7.0.10-60/www/advanced-windows-installation.html
ImageMagick-7.0.10-60/www/animate.html
ImageMagick-7.0.10-60/www/architecture.html
ImageMagick-7.0.10-60/www/changelog.html
ImageMagick-7.0.10-60/www/cipher.html
ImageMagick-7.0.10-60/www/cite.html
ImageMagick-7.0.10-60/www/clahe.html
ImageMagick-7.0.10-60/www/color.html
ImageMagick-7.0.10-60/www/color-management.html
ImageMagick-7.0.10-60/www/color-thresholding.html
ImageMagick-7.0.10-60/www/command-line-options.html
ImageMagick-7.0.10-60/www/command-line-processing.html
ImageMagick-7.0.10-60/www/command-line-tools.html
ImageMagick-7.0.10-60/www/compare.html
ImageMagick-7.0.10-60/www/compose.html
ImageMagick-7.0.10-60/www/composite.html
ImageMagick-7.0.10-60/www/conjure.html
ImageMagick-7.0.10-60/www/connected-components.html
ImageMagick-7.0.10-60/www/convert.html
ImageMagick-7.0.10-60/www/defines.html
ImageMagick-7.0.10-60/www/display.html
ImageMagick-7.0.10-60/www/download.html
ImageMagick-7.0.10-60/www/escape.html
ImageMagick-7.0.10-60/www/exception.html
ImageMagick-7.0.10-60/www/formats.html
ImageMagick-7.0.10-60/www/high-dynamic-range.html
ImageMagick-7.0.10-60/www/import.html
ImageMagick-7.0.10-60/www/magick-core.html
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool$ cd ImageMagick-7.0.10-60/
```

## configure

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/ImageMagick-7.0.10-60$ ./configure
checking build system type... x86_64-pc-linux-gnu
checking host system type... x86_64-pc-linux-gnu
checking target system type... x86_64-pc-linux-gnu
checking for a BSD-compatible install... /usr/bin/install -c
checking whether build environment is sane... yes
checking for a thread-safe mkdir -p... /usr/bin/mkdir -p
checking for gawk... no
checking for mawk... mawk
checking whether make sets $(MAKE)... yes
checking whether make supports nested variables... yes
checking whether UID '1001' is supported by ustar format... yes
checking whether GID '1001' is supported by ustar format... yes
checking how to create a ustar tar archive... gnutar
checking whether make supports nested variables... (cached) yes
Configuring ImageMagick 7.0.10-60
checking whether build environment is sane... yes
checking whether make supports the include directive... yes (GNU style)
checking for gcc... gcc
checking whether the C compiler works... yes
checking for C compiler default output file name... a.out
checking for suffix of executables... 
checking whether we are cross compiling... no
checking for suffix of object files... o
checking whether we are using the GNU C compiler... yes
checking whether gcc accepts -g... yes
checking for gcc option to accept ISO C89... none needed
checking whether gcc understands -c and -o together... yes
checking dependency style of gcc... gcc3
checking how to run the C preprocessor... gcc -E
checking for grep that handles long lines and -e... /usr/bin/grep
checking for egrep... /usr/bin/grep -E
checking for ANSI C header files... yes
checking for sys/types.h... yes
checking for sys/stat.h... yes
checking for stdlib.h... yes
checking for string.h... yes
checking for memory.h... yes
checking for strings.h... yes
checking for inttypes.h... yes
checking for stdint.h... yes
checking for unistd.h... yes
checking minix/config.h usability... no
checking minix/config.h presence... no
checking for minix/config.h... no
checking whether it is safe to define __EXTENSIONS__... yes
checking for ar... ar
checking the archiver (ar) interface... ar
checking for gcc... (cached) gcc
checking whether we are using the GNU C compiler... (cached) yes
checking whether gcc accepts -g... (cached) yes
checking for gcc option to accept ISO C89... (cached) none needed
checking whether gcc understands -c and -o together... (cached) yes
checking dependency style of gcc... (cached) gcc3
checking how to run the C preprocessor... gcc -E
checking for a sed that does not truncate output... /usr/bin/sed
checking for fgrep... /usr/bin/grep -F
checking how to print strings... printf
checking for ld used by gcc... /usr/bin/ld
checking if the linker (/usr/bin/ld) is GNU ld... yes
checking for ld used by gcc... (cached) /usr/bin/ld
checking if the linker (/usr/bin/ld) is GNU ld... (cached) yes
checking for gcc option to accept ISO C99... none needed
checking for C compiler vendor... gnu
checking CFLAGS for most reasonable warnings... -Wall
checking whether make sets $(MAKE)... (cached) yes
checking whether ln -s works... yes
checking for a sed that does not truncate output... (cached) /usr/bin/sed
checking for gawk... (cached) mawk
checking if malloc debugging is wanted... no
checking for __attribute__... yes
checking for gcc architecture flag... 
checking for x86 cpuid 0 output... 16:756e6547:6c65746e:49656e69
checking for x86 cpuid 1 output... 906ed:2100800:7ffafbff:bfebfbff
checking whether C compiler accepts -mtune=core2... yes
checking for gcc architecture flag... -mtune=core2
checking for pkg-config... /usr/bin/pkg-config
checking pkg-config is at least version 0.20... yes
checking for C compiler vendor... (cached) gnu
checking if LD -Wl,--version-script works... yes
checking for linker lazyload option... none
checking whether gcc is Clang... no
checking whether pthreads work with "-pthread" and "-lpthread"... yes
checking for joinable pthread attribute... PTHREAD_CREATE_JOINABLE
checking whether more special flags are required for pthreads... no
checking for PTHREAD_PRIO_INHERIT... yes
checking for gcc option to support OpenMP... -fopenmp
checking for OpenCL library... disabled
checking for special C compiler options needed for large files... no
checking for _FILE_OFFSET_BITS value needed for large files... no
checking for _LARGEFILE_SOURCE value needed for large files... no
checking Linux compatible sendfile()... yes
checking for BSD- or MS-compatible name lister (nm)... /usr/bin/nm -B
checking the name lister (/usr/bin/nm -B) interface... BSD nm
checking the maximum length of command line arguments... 1572864
checking how to convert x86_64-pc-linux-gnu file names to x86_64-pc-linux-gnu format... func_convert_file_noop
checking how to convert x86_64-pc-linux-gnu file names to toolchain format... func_convert_file_noop
checking for /usr/bin/ld option to reload object files... -r
checking for objdump... objdump
checking how to recognize dependent libraries... pass_all
checking for dlltool... no
checking how to associate runtime and link libraries... printf %s\n
checking for archiver @FILE support... @
checking for strip... strip
checking for ranlib... ranlib
checking command to parse /usr/bin/nm -B output from gcc object... ok
checking for sysroot... no
checking for a working dd... /usr/bin/dd
checking how to truncate binary pipes... /usr/bin/dd bs=4096 count=1
checking for mt... mt
checking if mt is a manifest tool... no
checking for dlfcn.h... yes
checking for objdir... .libs
checking if gcc supports -fno-rtti -fno-exceptions... no
checking for gcc option to produce PIC... -fPIC -DPIC
checking if gcc PIC flag -fPIC -DPIC works... yes
checking if gcc static flag -static works... yes
checking if gcc supports -c -o file.o... yes
checking if gcc supports -c -o file.o... (cached) yes
checking whether the gcc linker (/usr/bin/ld -m elf_x86_64) supports shared libraries... yes
checking whether -lc should be explicitly linked in... no
checking dynamic linker characteristics... GNU/Linux ld.so
checking how to hardcode library paths into programs... immediate
checking for shl_load... no
checking for shl_load in -ldld... no
checking for dlopen... no
checking for dlopen in -ldl... yes
checking whether a program can dlopen itself... yes
checking whether a statically linked program can dlopen itself... no
checking whether stripping libraries is possible... yes
checking if libtool supports shared libraries... yes
checking whether to build shared libraries... yes
checking whether to build static libraries... yes
checking for g++... g++
checking whether we are using the GNU C++ compiler... yes
checking whether g++ accepts -g... yes
checking dependency style of g++... gcc3
checking how to run the C++ preprocessor... g++ -E
checking for ld used by g++... /usr/bin/ld -m elf_x86_64
checking if the linker (/usr/bin/ld -m elf_x86_64) is GNU ld... yes
checking whether the g++ linker (/usr/bin/ld -m elf_x86_64) supports shared libraries... yes
checking for g++ option to produce PIC... -fPIC -DPIC
checking if g++ PIC flag -fPIC -DPIC works... yes
checking if g++ static flag -static works... yes
checking if g++ supports -c -o file.o... yes
checking if g++ supports -c -o file.o... (cached) yes
checking whether the g++ linker (/usr/bin/ld -m elf_x86_64) supports shared libraries... yes
checking dynamic linker characteristics... (cached) GNU/Linux ld.so
checking how to hardcode library paths into programs... immediate
checking whether to enable maintainer-specific portions of Makefiles... no
checking whether gcc needs -traditional... no
checking for ANSI C header files... (cached) yes
checking whether to enable assertions... yes
checking for dirent.h that defines DIR... yes
checking for library containing opendir... none required
checking arm/limits.h usability... no
checking arm/limits.h presence... no
checking for arm/limits.h... no
checking arpa/inet.h usability... yes
checking arpa/inet.h presence... yes
checking for arpa/inet.h... yes
checking complex.h usability... yes
checking complex.h presence... yes
checking for complex.h... yes
checking errno.h usability... yes
checking errno.h presence... yes
checking for errno.h... yes
checking fcntl.h usability... yes
checking fcntl.h presence... yes
checking for fcntl.h... yes
checking limits.h usability... yes
checking limits.h presence... yes
checking for limits.h... yes
checking linux/unistd.h usability... yes
checking linux/unistd.h presence... yes
checking for linux/unistd.h... yes
checking locale.h usability... yes
checking locale.h presence... yes
checking for locale.h... yes
checking machine/param.h usability... no
checking machine/param.h presence... no
checking for machine/param.h... no
checking mach-o/dyld.h usability... no
checking mach-o/dyld.h presence... no
checking for mach-o/dyld.h... no
checking netinet/in.h usability... yes
checking netinet/in.h presence... yes
checking for netinet/in.h... yes
checking OS.h usability... no
checking OS.h presence... no
checking for OS.h... no
checking process.h usability... no
checking process.h presence... no
checking for process.h... no
checking sun_prefetch.h usability... no
checking sun_prefetch.h presence... no
checking for sun_prefetch.h... no
checking stdarg.h usability... yes
checking stdarg.h presence... yes
checking for stdarg.h... yes
checking sys/ipc.h usability... yes
checking sys/ipc.h presence... yes
checking for sys/ipc.h... yes
checking sys/mman.h usability... yes
checking sys/mman.h presence... yes
checking for sys/mman.h... yes
checking sys/resource.h usability... yes
checking sys/resource.h presence... yes
checking for sys/resource.h... yes
checking sys/sendfile.h usability... yes
checking sys/sendfile.h presence... yes
checking for sys/sendfile.h... yes
checking sys/socket.h usability... yes
checking sys/socket.h presence... yes
checking for sys/socket.h... yes
checking sys/syslimits.h usability... no
checking sys/syslimits.h presence... no
checking for sys/syslimits.h... no
checking sys/time.h usability... yes
checking sys/time.h presence... yes
checking for sys/time.h... yes
checking sys/timeb.h usability... yes
checking sys/timeb.h presence... yes
checking for sys/timeb.h... yes
checking sys/times.h usability... yes
checking sys/times.h presence... yes
checking for sys/times.h... yes
checking sys/uio.h usability... yes
checking sys/uio.h presence... yes
checking for sys/uio.h... yes
checking sys/wait.h usability... yes
checking sys/wait.h presence... yes
checking for sys/wait.h... yes
checking utime.h usability... yes
checking utime.h presence... yes
checking for utime.h... yes
checking wchar.h usability... yes
checking wchar.h presence... yes
checking for wchar.h... yes
checking xlocale.h usability... no
checking xlocale.h presence... no
checking for xlocale.h... no
checking for stdbool.h that conforms to C99... yes
checking for _Bool... yes
checking for working volatile... yes
checking for preprocessor stringizing operator... yes
checking whether stat file-mode macros are broken... no
checking whether time.h and sys/time.h may both be included... yes
checking whether struct tm is in sys/time.h or time.h... time.h
checking for struct tm.tm_zone... yes
checking whether #! works in shell scripts... yes
checking whether char is unsigned... no
checking for an ANSI C-conforming const... yes
checking for inline... inline
checking for C/C++ restrict keyword... __restrict
checking for working volatile... (cached) yes
checking whether byte ordering is bigendian... no
checking for int8_t... yes
checking for int16_t... yes
checking for int32_t... yes
checking for int64_t... yes
checking for unsigned long long int... yes
checking for long long int... yes
checking for intmax_t... yes
checking for intptr_t... yes
checking for mbstate_t... yes
checking for mode_t... yes
checking for off_t... yes
checking for pid_t... yes
checking for size_t... yes
checking for ssize_t... yes
checking for uid_t in sys/types.h... yes
checking for uint8_t... yes
checking for uint16_t... yes
checking for uint32_t... yes
checking for uint64_t... yes
checking for uintmax_t... yes
checking for uintptr_t... yes
checking size of float_t... 4
checking size of double_t... 8
checking size of float... 4
checking size of double... 8
checking size of long double... 16
checking size of unsigned long long... 8
checking size of ssize_t... 8
checking size of void *... 8
checking whether our compiler supports __func__... yes
checking whether closedir returns void... no
checking for stdlib.h... (cached) yes
checking for unistd.h... (cached) yes
checking for sys/param.h... yes
checking for getpagesize... yes
checking for working mmap... yes
checking vfork.h usability... no
checking vfork.h presence... no
checking for vfork.h... no
checking for fork... yes
checking for vfork... yes
checking for working fork... yes
checking for working vfork... (cached) yes
checking for working memcmp... yes
checking sys/select.h usability... yes
checking sys/select.h presence... yes
checking for sys/select.h... yes
checking for sys/socket.h... (cached) yes
checking types of arguments for select... int,fd_set *,struct timeval *
checking for working strtod... yes
checking whether strerror_r is declared... yes
checking for strerror_r... yes
checking whether strerror_r returns char *... yes
checking for vprintf... yes
checking for _doprnt... no
checking for sqrt in -lm... yes
checking for library containing gethostbyname... none required
checking for library containing socket... none required
checking for library containing clock_gettime... none required
checking whether clock_gettime supports CLOCK_REALTIME... yes
checking whether pread is declared... yes
checking whether pwrite is declared... yes
checking whether strlcpy is declared... no
checking whether vsnprintf is declared... yes
checking whether we are using the GNU C++ compiler... (cached) yes
checking whether g++ accepts -g... (cached) yes
checking dependency style of g++... (cached) gcc3
checking whether the compiler recognizes bool as a built-in type... yes
checking whether the compiler implements namespaces... yes
checking if g++ supports namespace std... yes
checking whether the compiler supports ISO C++ standard library... yes
checking for g++ option to support OpenMP... -fopenmp
checking whether C++ compiler is sufficient for Magick++... yes
checking for X11 configure files... 
checking for GOMP_parallel_start in -lgomp... yes
-------------------------------------------------------------
checking for BZLIB... 
checking bzlib.h usability... no
checking bzlib.h presence... no
checking for bzlib.h... no
checking for BZ2_bzDecompress in -lbz2... no
checking if BZLIB package is complete... no
checking for X... libraries , headers 
checking for gethostbyname... yes
checking for connect... yes
checking for remove... yes
checking for shmat... yes
checking for IceConnectionNumber in -lICE... yes
-------------------------------------------------------------
checking for X11... 
checking for shmctl... yes
checking for XShmAttach in -lXext... no
checking for XShapeCombineMask in -lXext... no
checking for XtSetEventDispatcher in -lXt... yes
-------------------------------------------------------------
checking for libzip >= 1.0.0... no

-------------------------------------------------------------
checking for zlib >= 1.0.0... yes

-------------------------------------------------------------
checking for libzstd >= 1.0.0... no

-------------------------------------------------------------
checking for DPS... 
checking DPS/dpsXclient.h usability... no
checking DPS/dpsXclient.h presence... no
checking for DPS/dpsXclient.h... no
checking for DPSInitialize in -ldps... no
checking for DPSInitialize in -ldps... no
checking for XDPSPixelsPerPoint in -ldpstk... no
checking if DPS package is complete... no
-------------------------------------------------------------
checking for fftw3 >= 3.0.0... no

-------------------------------------------------------------
checking for FLIF... 
checking flif.h usability... no
checking flif.h presence... no
checking for flif.h... no
checking for flif_create_decoder in -lflif... no
checking if FLIF package is complete... no
-------------------------------------------------------------
checking for FlashPIX... 
checking fpxlib.h usability... no
checking fpxlib.h presence... no
checking for fpxlib.h... no
checking for FPX_OpenImageByFilename in -lfpx... no
checking if FlashPIX package is complete... no
-------------------------------------------------------------
checking for ddjvuapi >= 3.5.0... no

-------------------------------------------------------------
checking for fontconfig >= 2.1.0... no

-------------------------------------------------------------
checking for freetype2... no

-------------------------------------------------------------
checking for raqm... no

checking for Windows GDI32 support... 
checking windows.h usability... no
checking windows.h presence... no
checking for windows.h... no
checking for winuser.h... no
checking for wingdi.h... no
checking if Windows GDI32 support is complete... no
-------------------------------------------------------------
checking for libgvc >= 2.9.0... no

-------------------------------------------------------------
checking for libheif... no

-------------------------------------------------------------
checking for JBIG... 
checking jbig.h usability... no
checking jbig.h presence... no
checking for jbig.h... no
checking for jbg_dec_init in -ljbig... no
checking if JBIG package is complete... no
-------------------------------------------------------------
checking for JPEG... 
checking jconfig.h usability... no
checking jconfig.h presence... no
checking for jconfig.h... no
checking jerror.h usability... no
checking jerror.h presence... no
checking for jerror.h... no
checking jmorecfg.h usability... no
checking jmorecfg.h presence... no
checking for jmorecfg.h... no
checking jpeglib.h usability... no
checking jpeglib.h presence... no
checking for jpeglib.h... no
checking for jpeg_read_header in -ljpeg... no
checking if JPEG package is complete... no
-------------------------------------------------------------
checking for lcms2 >= 2.0.0... no

-------------------------------------------------------------
checking for libopenjp2 >= 2.1.0... no

-------------------------------------------------------------
checking for lqr-1 >= 0.1.0... no

-------------------------------------------------------------
checking for liblzma >= 2.9.0... no

-------------------------------------------------------------
checking for OpenEXR >= 1.0.6... no

-------------------------------------------------------------
checking for pangocairo >= 1.28.1... no

checking for pango >= 1.28.1... no

-------------------------------------------------------------
checking for libpng >= 1.0.0... no

-------------------------------------------------------------
checking for libraw_r >= 0.14.8... no

-------------------------------------------------------------
checking for TIFF... 
checking tiff.h usability... no
checking tiff.h presence... no
checking for tiff.h... no
checking tiffio.h usability... no
checking tiffio.h presence... no
checking for tiffio.h... no
checking for TIFFOpen in -ltiff... no
checking for TIFFClientOpen in -ltiff... no
checking for TIFFIsByteSwapped in -ltiff... no
checking for TIFFReadRGBATile in -ltiff... no
checking for TIFFReadRGBAStrip in -ltiff... no
checking if TIFF package is complete... no
-------------------------------------------------------------
checking for libwebp... no
checking for libwebpmux >= 0.5.0 libwebpdemux >= 0.5.0... no

checking if WMF package is complete ... no
-------------------------------------------------------------
checking for libxml-2.0 >= 2.0.0... no

checking for acosh... yes
checking for _aligned_malloc... no
checking for aligned_malloc... no
checking for asinh... yes
checking for atanh... yes
checking for atoll... yes
checking for atexit... yes
checking for cabs... yes
checking for carg... yes
checking for cimag... yes
checking for creal... yes
checking for clock... yes
checking for clock_getres... yes
checking for clock_gettime... yes
checking for ctime_r... yes
checking for directio... no
checking for erf... yes
checking for _exit... yes
checking for execvp... yes
checking for fchmod... yes
checking for floor... yes
checking for fork... (cached) yes
checking for ftime... yes
checking for ftruncate... yes
checking for getc_unlocked... yes
checking for getcwd... yes
checking for getpid... yes
checking for getexecname... no
checking for getdtablesize... yes
checking for getpagesize... (cached) yes
checking for getpwnam_r... yes
checking for getrlimit... yes
checking for getrusage... yes
checking for gettimeofday... yes
checking for gmtime_r... yes
checking for isnan... yes
checking for j0... yes
checking for j1... yes
checking for lltostr... no
checking for localtime_r... yes
checking for lstat... yes
checking for memmove... yes
checking for memset... yes
checking for mkstemp... yes
checking for munmap... yes
checking for nanosleep... yes
checking for newlocale... yes
checking for _NSGetExecutablePath... no
checking for pclose... yes
checking for _pclose... no
checking for poll... yes
checking for popen... yes
checking for _popen... no
checking for posix_fadvise... yes
checking for posix_fallocate... yes
checking for posix_madvise... yes
checking for posix_memalign... yes
checking for posix_spawnp... yes
checking for pow... yes
checking for pread... yes
checking for pwrite... yes
checking for qsort_r... yes
checking for raise... yes
checking for rand_r... yes
checking for readlink... yes
checking for realpath... yes
checking for select... yes
checking for seekdir... yes
checking for sendfile... yes
checking for setlocale... yes
checking for socket... yes
checking for sqrt... yes
checking for setvbuf... yes
checking for stat... yes
checking for strcasestr... yes
checking for strchr... yes
checking for strrchr... yes
checking for strcspn... yes
checking for strdup... yes
checking for strpbrk... yes
checking for strspn... yes
checking for strstr... yes
checking for strtod... (cached) yes
checking for strtod_l... yes
checking for strtol... yes
checking for strtoul... yes
checking for symlink... yes
checking for sysconf... yes
checking for sigemptyset... yes
checking for sigaction... yes
checking for spawnvp... no
checking for strerror... yes
checking for strlcat... no
checking for strlcpy... no
checking for strcasecmp... yes
checking for strncasecmp... yes
checking for telldir... yes
checking for tempnam... yes
checking for times... yes
checking for ulltostr... no
checking for uselocale... yes
checking for usleep... yes
checking for utime... yes
checking for vfprintf... yes
checking for vfprintf_l... no
checking for vsprintf... yes
checking for vsnprintf... yes
checking for vsnprintf_l... no
checking for waitpid... yes
checking for _wfopen... no
checking for _wstat... no
-------------------------------------------------------------
checking for ImageMagick delegate programs... 
checking for bpgdec...  bpgdec
checking for bpgenc...  bpgenc
checking for blender...  blender
checking for xdg-open... /usr/bin/xdg-open
checking for ufraw-batch...  ufraw-batch
checking for libreoffice... /usr/bin/libreoffice
checking for dvips... /usr/bin/dvips
checking for magick...  magick
checking for magick...  magick
checking for xterm...  xterm
checking for dot... /usr/bin/dot
checking for hp2xx...  hp2xx
checking for html2ps...  html2ps
checking for ilbmtoppm...  ilbmtoppm
checking for ppmtoilbm...  ppmtoilbm
checking for JxrDecApp...  JxrDecApp
checking for JxrEncApp...  JxrEncApp
checking for lepton...  lepton
checking for lp... /usr/bin/lp
checking for lpr... /usr/bin/lpr
checking for gimp...  gimp
checking for magick...  magick
checking for ffmpeg...  ffmpeg
checking for ffmpeg...  ffmpeg
checking for mrsidgeodecode...  mrsidgeodecode
checking for mv... /usr/bin/mv
checking for pcl6...  pcl6
checking for gsx... no
checking for gsc... no
checking for gs... /usr/bin/gs
checking for rm... /usr/bin/rm
checking for rsvg-convert...  rsvg-convert
checking for inkscape...  inkscape
checking for tesseract...  tesseract
checking for potrace...  potrace
checking for fig2dev...  fig2dev
checking for dwebp...  dwebp
checking for cwebp...  cwebp
checking for curl... /home/ye/anaconda3/bin/curl
checking for gxps...  gxps
checking for Apple fonts directory... not found!
checking for Dejavu fonts directory... not found!
checking for Ghostscript fonts directory... /usr/share/ghostscript/fonts/
checking for URW-base35 fonts directory... /usr/share/fonts/type1/urw-base35/
checking for Windows fonts directory... not found!
checking for gnutar... no
checking for gtar... no
checking for tar... tar
checking for perl... perl
checking for rpmbuild... no
checking for rpm... no
checking for 7za... 7za
checking for zip... zip
-------------------------------------------------------------
checking for PCL... 
checking for pcl color device... ppmraw
checking for pcl CMYK device... ppmraw
checking for pcl mono device... ppmraw
-------------------------------------------------------------
checking for XPS... 
checking for xps color device... ppmraw
checking for xps CMYK device... ppmraw
checking for xps mono device... ppmraw
-------------------------------------------------------------
checking for Ghostscript... 
checking for Ghostscript version... 9.52
checking for gs color device... png16m
checking for gs alpha device... pngalpha
checking for gs CMYK device... pamcmyk32
checking for gs mono device... pbmraw
checking for gs PDF writing device... pdfwrite
checking for gs PS writing device... ps2write
checking for gs EPS writing device... eps2write
-------------------------------------------------------------
Update ImageMagick configuration
checking that generated files are newer than configure... done
checking that generated files are newer than configure... done
configure: creating ./config.status
config.status: creating common.shi
config.status: creating config/configure.xml
config.status: creating config/delegates.xml
config.status: creating config/ImageMagick.rdf
config.status: creating config/MagickCore.dox
config.status: creating config/MagickWand.dox
config.status: creating config/Magick++.dox
config.status: creating config/type-apple.xml
config.status: creating config/type-dejavu.xml
config.status: creating config/type-ghostscript.xml
config.status: creating config/type-urw-base35.xml
config.status: creating config/type-windows.xml
config.status: creating config/type.xml
config.status: creating ImageMagick.spec
config.status: creating Magick++/bin/Magick++-config
config.status: creating MagickCore/ImageMagick.pc
config.status: creating Magick++/lib/Magick++.pc
config.status: creating MagickCore/MagickCore-config
config.status: creating MagickCore/MagickCore.pc
config.status: creating MagickCore/version.h
config.status: creating Makefile
config.status: creating magick.sh
config.status: creating PerlMagick/check.sh
config.status: creating PerlMagick/default/Magick.pm
config.status: creating PerlMagick/Makefile.PL
config.status: creating PerlMagick/default/Makefile.PL
config.status: creating PerlMagick/quantum/Makefile.PL
config.status: creating PerlMagick/quantum/quantum.pm
config.status: creating PerlMagick/quantum/quantum.xs
config.status: creating PerlMagick/quantum/typemap
config.status: creating utilities/animate.1
config.status: creating utilities/compare.1
config.status: creating utilities/composite.1
config.status: creating utilities/conjure.1
config.status: creating utilities/convert.1
config.status: creating utilities/display.1
config.status: creating utilities/identify.1
config.status: creating utilities/ImageMagick.1
config.status: creating utilities/import.1
config.status: creating utilities/magick.1
config.status: creating utilities/magick-script.1
config.status: creating utilities/mogrify.1
config.status: creating utilities/montage.1
config.status: creating utilities/stream.1
config.status: creating MagickWand/MagickWand-config
config.status: creating MagickWand/MagickWand.pc
config.status: creating config/config.h
config.status: executing MagickCore/magick-baseconfig.h commands
config.status: creating MagickCore/magick-baseconfig.h - prefix MAGICKCORE for config/config.h defines
config.status: executing depfiles commands
config.status: executing libtool commands
config.status: executing default commands
config.status: executing magick.sh.in commands
config.status: executing MagickCore-config.in commands
config.status: executing MagickWand-config.in commands
config.status: executing Magick++-config.in commands
config.status: executing PerlMagick/check.sh.in commands
configure:
==============================================================================
ImageMagick 7.0.10-60 is configured as follows. Please verify that this
configuration matches your expectations.

Host system type: x86_64-pc-linux-gnu
Build system type: x86_64-pc-linux-gnu

                  Option                        Value
------------------------------------------------------------------------------
Shared libraries  --enable-shared=yes		yes
Static libraries  --enable-static=yes		yes
Build utilities   --with-utilities=yes		yes
Module support    --with-modules=no		no
GNU ld            --with-gnu-ld=yes		yes
Quantum depth     --with-quantum-depth=16	16
High Dynamic Range Imagery
                  --enable-hdri=yes		yes

Install documentation:				yes

Memory allocation library:
  JEMalloc          --with-jemalloc=no		no
  TCMalloc          --with-tcmalloc=no		no
  UMem              --with-umem=no		no

Delegate library configuration:
  BZLIB             --with-bzlib=yes		no
  Autotrace         --with-autotrace=no		no
  DJVU              --with-djvu=yes		no
  DPS               --with-dps=yes		no
  FFTW              --with-fftw=yes		no
  FLIF              --with-flif=yes		no
  FlashPIX          --with-fpx=yes		no
  FontConfig        --with-fontconfig=yes	no
  FreeType          --with-freetype=yes		no
  Ghostscript lib   --with-gslib=no		no
  Graphviz          --with-gvc=yes		no
  HEIC              --with-heic=yes		no
  JBIG              --with-jbig=yes		no
  JPEG v1           --with-jpeg=yes		no
  JPEG XL           --with-jxl=no		no
  LCMS              --with-lcms=yes		no
  LQR               --with-lqr=yes		no
  LTDL              --with-ltdl=no		no
  LZMA              --with-lzma=yes		no
  Magick++          --with-magick-plus-plus=yes	yes
  OpenEXR           --with-openexr=yes		no
  OpenJP2           --with-openjp2=yes		no
  PANGO             --with-pango=yes		no
  PERL              --with-perl=no		no
  PNG               --with-png=yes		no
  RAQM              --with-raqm=yes		no
  RAW               --with-raw=yes		no
  RSVG              --with-rsvg=no		no
  TIFF              --with-tiff=yes		no
  WEBP              --with-webp=yes		no
  WMF               --with-wmf=no		no
  X11               --with-x=			yes
  XML               --with-xml=yes		no
  ZIP               --with-ziplib=yes		no
  ZLIB              --with-zlib=yes		yes
  ZSTD              --with-zstd=yes		no

Delegate program configuration:
  GhostPCL          None			pcl6 (unknown)
  GhostXPS          None			gxps (unknown)
  Ghostscript       None			gs (9.52)

Font configuration:
  Apple fonts       --with-apple-font-dir=default	
  Dejavu fonts      --with-dejavu-font-dir=default	none
  Ghostscript fonts --with-gs-font-dir=default		/usr/share/ghostscript/fonts/
  URW-base35 fonts  --with-urw-base35-font-dir=default	/usr/share/fonts/type1/urw-base35/
  Windows fonts     --with-windows-font-dir=default	none

X11 configuration:
  X_CFLAGS        = 
  X_PRE_LIBS      =  -lSM -lICE
  X_LIBS          = 
  X_EXTRA_LIBS    = 

Options used to compile and link:
  PREFIX          = /usr/local
  EXEC-PREFIX     = /usr/local
  VERSION         = 7.0.10-60
  CC              = gcc
  CFLAGS          =  -fopenmp -Wall -g -O2 -mtune=core2 -fexceptions -pthread -DMAGICKCORE_HDRI_ENABLE=1 -DMAGICKCORE_QUANTUM_DEPTH=16
  CPPFLAGS        =  -DMAGICKCORE_HDRI_ENABLE=1 -DMAGICKCORE_QUANTUM_DEPTH=16 
  PCFLAGS         = 
  DEFS            = -DHAVE_CONFIG_H
  LDFLAGS         =  
  LIBS            =                        -lXt   -lSM -lICE -lX11           -lz -lz    -lm    -lpthread 
  CXX             = g++
  CXXFLAGS        =  -pthread
  FEATURES        = DPC HDRI Cipher OpenMP
  DELEGATES       = ps video x zlib
==============================================================================

(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/ImageMagick-7.0.10-60$
```

## make install

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/ImageMagick-7.0.10-60$ sudo make install
[sudo] password for ye: 
make  install-am
make[1]: Entering directory '/home/ye/tool/ImageMagick-7.0.10-60'
make[2]: Entering directory '/home/ye/tool/ImageMagick-7.0.10-60'
 /usr/bin/mkdir -p '/usr/local/lib'
 /bin/bash ./libtool   --mode=install /usr/bin/install -c   MagickCore/libMagickCore-7.Q16HDRI.la MagickWand/libMagickWand-7.Q16HDRI.la Magick++/lib/libMagick++-7.Q16HDRI.la '/usr/local/lib'
libtool: install: /usr/bin/install -c MagickCore/.libs/libMagickCore-7.Q16HDRI.so.8.0.0 /usr/local/lib/libMagickCore-7.Q16HDRI.so.8.0.0
libtool: install: (cd /usr/local/lib && { ln -s -f libMagickCore-7.Q16HDRI.so.8.0.0 libMagickCore-7.Q16HDRI.so.8 || { rm -f libMagickCore-7.Q16HDRI.so.8 && ln -s libMagickCore-7.Q16HDRI.so.8.0.0 libMagickCore-7.Q16HDRI.so.8; }; })
libtool: install: (cd /usr/local/lib && { ln -s -f libMagickCore-7.Q16HDRI.so.8.0.0 libMagickCore-7.Q16HDRI.so || { rm -f libMagickCore-7.Q16HDRI.so && ln -s libMagickCore-7.Q16HDRI.so.8.0.0 libMagickCore-7.Q16HDRI.so; }; })
libtool: install: /usr/bin/install -c MagickCore/.libs/libMagickCore-7.Q16HDRI.lai /usr/local/lib/libMagickCore-7.Q16HDRI.la
libtool: warning: relinking 'MagickWand/libMagickWand-7.Q16HDRI.la'
libtool: install: (cd /home/ye/tool/ImageMagick-7.0.10-60; /bin/bash "/home/ye/tool/ImageMagick-7.0.10-60/libtool"  --silent --tag CC --mode=relink gcc -fopenmp -Wall -g -O2 -mtune=core2 -fexceptions -pthread -DMAGICKCORE_HDRI_ENABLE=1 -DMAGICKCORE_QUANTUM_DEPTH=16 -no-undefined -Wl,--version-script=./MagickWand/libMagickWand.map -version-info 8:0:0 -o MagickWand/libMagickWand-7.Q16HDRI.la -rpath /usr/local/lib MagickWand/libMagickWand_7_Q16HDRI_la-animate.lo MagickWand/libMagickWand_7_Q16HDRI_la-compare.lo MagickWand/libMagickWand_7_Q16HDRI_la-composite.lo MagickWand/libMagickWand_7_Q16HDRI_la-conjure.lo MagickWand/libMagickWand_7_Q16HDRI_la-convert.lo MagickWand/libMagickWand_7_Q16HDRI_la-deprecate.lo MagickWand/libMagickWand_7_Q16HDRI_la-display.lo MagickWand/libMagickWand_7_Q16HDRI_la-drawing-wand.lo MagickWand/libMagickWand_7_Q16HDRI_la-identify.lo MagickWand/libMagickWand_7_Q16HDRI_la-import.lo MagickWand/libMagickWand_7_Q16HDRI_la-magick-cli.lo MagickWand/libMagickWand_7_Q16HDRI_la-magick-image.lo MagickWand/libMagickWand_7_Q16HDRI_la-magick-property.lo MagickWand/libMagickWand_7_Q16HDRI_la-magick-wand.lo MagickWand/libMagickWand_7_Q16HDRI_la-mogrify.lo MagickWand/libMagickWand_7_Q16HDRI_la-montage.lo MagickWand/libMagickWand_7_Q16HDRI_la-operation.lo MagickWand/libMagickWand_7_Q16HDRI_la-pixel-iterator.lo MagickWand/libMagickWand_7_Q16HDRI_la-pixel-wand.lo MagickWand/libMagickWand_7_Q16HDRI_la-script-token.lo MagickWand/libMagickWand_7_Q16HDRI_la-stream.lo MagickWand/libMagickWand_7_Q16HDRI_la-wand.lo MagickWand/libMagickWand_7_Q16HDRI_la-wandcli.lo MagickWand/libMagickWand_7_Q16HDRI_la-wand-view.lo MagickCore/libMagickCore-7.Q16HDRI.la -lSM -lICE -lX11 -lgomp -lm )
libtool: install: /usr/bin/install -c MagickWand/.libs/libMagickWand-7.Q16HDRI.so.8.0.0T /usr/local/lib/libMagickWand-7.Q16HDRI.so.8.0.0
libtool: install: (cd /usr/local/lib && { ln -s -f libMagickWand-7.Q16HDRI.so.8.0.0 libMagickWand-7.Q16HDRI.so.8 || { rm -f libMagickWand-7.Q16HDRI.so.8 && ln -s libMagickWand-7.Q16HDRI.so.8.0.0 libMagickWand-7.Q16HDRI.so.8; }; })
libtool: install: (cd /usr/local/lib && { ln -s -f libMagickWand-7.Q16HDRI.so.8.0.0 libMagickWand-7.Q16HDRI.so || { rm -f libMagickWand-7.Q16HDRI.so && ln -s libMagickWand-7.Q16HDRI.so.8.0.0 libMagickWand-7.Q16HDRI.so; }; })
libtool: install: /usr/bin/install -c MagickWand/.libs/libMagickWand-7.Q16HDRI.lai /usr/local/lib/libMagickWand-7.Q16HDRI.la
libtool: warning: relinking 'Magick++/lib/libMagick++-7.Q16HDRI.la'
libtool: install: (cd /home/ye/tool/ImageMagick-7.0.10-60; /bin/bash "/home/ye/tool/ImageMagick-7.0.10-60/libtool"  --silent --tag CXX --mode=relink g++ -pthread -no-undefined -version-info 4:0:0 -o Magick++/lib/libMagick++-7.Q16HDRI.la -rpath /usr/local/lib Magick++/lib/libMagick___7_Q16HDRI_la-Blob.lo Magick++/lib/libMagick___7_Q16HDRI_la-BlobRef.lo Magick++/lib/libMagick___7_Q16HDRI_la-CoderInfo.lo Magick++/lib/libMagick___7_Q16HDRI_la-Color.lo Magick++/lib/libMagick___7_Q16HDRI_la-Drawable.lo Magick++/lib/libMagick___7_Q16HDRI_la-Exception.lo Magick++/lib/libMagick___7_Q16HDRI_la-Functions.lo Magick++/lib/libMagick___7_Q16HDRI_la-Geometry.lo Magick++/lib/libMagick___7_Q16HDRI_la-Image.lo Magick++/lib/libMagick___7_Q16HDRI_la-ImageRef.lo Magick++/lib/libMagick___7_Q16HDRI_la-Montage.lo Magick++/lib/libMagick___7_Q16HDRI_la-Options.lo Magick++/lib/libMagick___7_Q16HDRI_la-Pixels.lo Magick++/lib/libMagick___7_Q16HDRI_la-ResourceLimits.lo Magick++/lib/libMagick___7_Q16HDRI_la-SecurityPolicy.lo Magick++/lib/libMagick___7_Q16HDRI_la-Statistic.lo Magick++/lib/libMagick___7_Q16HDRI_la-STL.lo Magick++/lib/libMagick___7_Q16HDRI_la-Thread.lo Magick++/lib/libMagick___7_Q16HDRI_la-TypeMetric.lo MagickCore/libMagickCore-7.Q16HDRI.la MagickWand/libMagickWand-7.Q16HDRI.la )
libtool: install: /usr/bin/install -c Magick++/lib/.libs/libMagick++-7.Q16HDRI.so.4.0.0T /usr/local/lib/libMagick++-7.Q16HDRI.so.4.0.0
libtool: install: (cd /usr/local/lib && { ln -s -f libMagick++-7.Q16HDRI.so.4.0.0 libMagick++-7.Q16HDRI.so.4 || { rm -f libMagick++-7.Q16HDRI.so.4 && ln -s libMagick++-7.Q16HDRI.so.4.0.0 libMagick++-7.Q16HDRI.so.4; }; })
libtool: install: (cd /usr/local/lib && { ln -s -f libMagick++-7.Q16HDRI.so.4.0.0 libMagick++-7.Q16HDRI.so || { rm -f libMagick++-7.Q16HDRI.so && ln -s libMagick++-7.Q16HDRI.so.4.0.0 libMagick++-7.Q16HDRI.so; }; })
libtool: install: /usr/bin/install -c Magick++/lib/.libs/libMagick++-7.Q16HDRI.lai /usr/local/lib/libMagick++-7.Q16HDRI.la
libtool: install: /usr/bin/install -c MagickCore/.libs/libMagickCore-7.Q16HDRI.a /usr/local/lib/libMagickCore-7.Q16HDRI.a
libtool: install: chmod 644 /usr/local/lib/libMagickCore-7.Q16HDRI.a
libtool: install: ranlib /usr/local/lib/libMagickCore-7.Q16HDRI.a
libtool: install: /usr/bin/install -c MagickWand/.libs/libMagickWand-7.Q16HDRI.a /usr/local/lib/libMagickWand-7.Q16HDRI.a
libtool: install: chmod 644 /usr/local/lib/libMagickWand-7.Q16HDRI.a
libtool: install: ranlib /usr/local/lib/libMagickWand-7.Q16HDRI.a
libtool: install: /usr/bin/install -c Magick++/lib/.libs/libMagick++-7.Q16HDRI.a /usr/local/lib/libMagick++-7.Q16HDRI.a
libtool: install: chmod 644 /usr/local/lib/libMagick++-7.Q16HDRI.a
libtool: install: ranlib /usr/local/lib/libMagick++-7.Q16HDRI.a
libtool: finish: PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin:/sbin" ldconfig -n /usr/local/lib
----------------------------------------------------------------------
Libraries have been installed in:
   /usr/local/lib

If you ever happen to want to link against installed libraries
in a given directory, LIBDIR, you must either use libtool, and
specify the full pathname of the library, or use the '-LLIBDIR'
flag during linking and do at least one of the following:
   - add LIBDIR to the 'LD_LIBRARY_PATH' environment variable
     during execution
   - add LIBDIR to the 'LD_RUN_PATH' environment variable
     during linking
   - use the '-Wl,-rpath -Wl,LIBDIR' linker flag
   - have your system administrator add LIBDIR to '/etc/ld.so.conf'

See any operating system documentation about shared libraries for
more information, such as the ld(1) and ld.so(8) manual pages.
----------------------------------------------------------------------
 /usr/bin/mkdir -p '/usr/local/bin'
  /bin/bash ./libtool   --mode=install /usr/bin/install -c utilities/magick '/usr/local/bin'
libtool: install: /usr/bin/install -c utilities/.libs/magick /usr/local/bin/magick
 /usr/bin/mkdir -p '/usr/local/bin'
 /usr/bin/install -c MagickCore/MagickCore-config MagickWand/MagickWand-config Magick++/bin/Magick++-config '/usr/local/bin'
/bin/bash ./config/mkinstalldirs /usr/local/bin
cd /usr/local/bin ; \
magick=`echo "magick" | sed 's,^.*/,,;s/$//;s,x,x,;s/$//'`; \
for name in animate compare composite conjure convert display identify import magick-script mogrify montage stream ; \
do \
  target=`echo "$name" | sed 's,^.*/,,;s/$//;s,x,x,;s/$//'`; \
  rm -f $target ; \
  ln -s $magick $target ; \
done
 /usr/bin/mkdir -p '/usr/local/include/ImageMagick-7/MagickCore'
 /usr/bin/install -c -m 644 MagickCore/MagickCore.h MagickCore/animate.h MagickCore/annotate.h MagickCore/artifact.h MagickCore/attribute.h MagickCore/blob.h MagickCore/cache.h MagickCore/cache-view.h MagickCore/channel.h MagickCore/cipher.h MagickCore/client.h MagickCore/coder.h MagickCore/color.h MagickCore/colormap.h MagickCore/colorspace.h MagickCore/compare.h MagickCore/composite.h MagickCore/compress.h MagickCore/configure.h MagickCore/constitute.h MagickCore/decorate.h MagickCore/delegate.h MagickCore/deprecate.h MagickCore/display.h MagickCore/distort.h MagickCore/distribute-cache.h MagickCore/draw.h MagickCore/effect.h MagickCore/enhance.h MagickCore/exception.h MagickCore/feature.h MagickCore/fourier.h MagickCore/fx.h MagickCore/gem.h MagickCore/geometry.h MagickCore/histogram.h MagickCore/identify.h MagickCore/image.h MagickCore/image-view.h MagickCore/layer.h '/usr/local/include/ImageMagick-7/MagickCore'
 /usr/bin/install -c -m 644 MagickCore/linked-list.h MagickCore/list.h MagickCore/locale_.h MagickCore/log.h MagickCore/magic.h MagickCore/magick.h MagickCore/magick-config.h MagickCore/magick-type.h MagickCore/matrix.h MagickCore/memory_.h MagickCore/method-attribute.h MagickCore/methods.h MagickCore/mime.h MagickCore/module.h MagickCore/monitor.h MagickCore/montage.h MagickCore/morphology.h MagickCore/nt-base.h MagickCore/opencl.h MagickCore/option.h MagickCore/paint.h MagickCore/pixel.h MagickCore/pixel-accessor.h MagickCore/policy.h MagickCore/prepress.h MagickCore/profile.h MagickCore/property.h MagickCore/quantize.h MagickCore/quantum.h MagickCore/random_.h MagickCore/registry.h MagickCore/resample.h MagickCore/resize.h MagickCore/resource_.h MagickCore/segment.h MagickCore/semaphore.h MagickCore/shear.h MagickCore/signature.h MagickCore/splay-tree.h MagickCore/static.h '/usr/local/include/ImageMagick-7/MagickCore'
 /usr/bin/install -c -m 644 MagickCore/statistic.h MagickCore/stream.h MagickCore/string_.h MagickCore/studio.h MagickCore/timer.h MagickCore/token.h MagickCore/transform.h MagickCore/threshold.h MagickCore/type.h MagickCore/utility.h MagickCore/version.h MagickCore/vision.h MagickCore/visual-effects.h MagickCore/widget.h MagickCore/xml-tree.h MagickCore/xwindow.h '/usr/local/include/ImageMagick-7/MagickCore'
 /usr/bin/mkdir -p '/usr/local/include/ImageMagick-7/MagickCore'
 /usr/bin/install -c -m 644 MagickCore/magick-baseconfig.h '/usr/local/include/ImageMagick-7/MagickCore'
 /usr/bin/mkdir -p '/usr/local/include/ImageMagick-7/MagickWand'
 /usr/bin/install -c -m 644 MagickWand/MagickWand.h MagickWand/animate.h MagickWand/compare.h MagickWand/composite.h MagickWand/conjure.h MagickWand/convert.h MagickWand/deprecate.h MagickWand/display.h MagickWand/drawing-wand.h MagickWand/identify.h MagickWand/import.h MagickWand/magick-cli.h MagickWand/magick-image.h MagickWand/magick-property.h MagickWand/method-attribute.h MagickWand/mogrify.h MagickWand/montage.h MagickWand/operation.h MagickWand/pixel-iterator.h MagickWand/pixel-wand.h MagickWand/stream.h MagickWand/wandcli.h MagickWand/wand-view.h '/usr/local/include/ImageMagick-7/MagickWand'
 /usr/bin/mkdir -p '/usr/local/etc/ImageMagick-7/'
 /usr/bin/install -c -m 644 config/colors.xml config/delegates.xml config/log.xml config/mime.xml config/policy.xml config/quantization-table.xml config/thresholds.xml config/type.xml config/type-apple.xml config/type-dejavu.xml config/type-ghostscript.xml config/type-urw-base35.xml config/type-windows.xml '/usr/local/etc/ImageMagick-7/'
 /usr/bin/mkdir -p '/usr/local/share/ImageMagick-7'
 /usr/bin/install -c -m 644 config/english.xml config/francais.xml config/locale.xml '/usr/local/share/ImageMagick-7'
 /usr/bin/mkdir -p '/usr/local/lib/ImageMagick-7.0.10/config-Q16HDRI'
 /usr/bin/install -c -m 644 config/configure.xml '/usr/local/lib/ImageMagick-7.0.10/config-Q16HDRI'
/bin/bash ./config/mkinstalldirs /usr/local/share/doc/ImageMagick-7
mkdir -p -- /usr/local/share/doc/ImageMagick-7
/usr/bin/install -c -m 644 ./index.html /usr/local/share/doc/ImageMagick-7
mkdir -p -- /usr/local/share/doc/ImageMagick-7/images
/usr/bin/install -c -m 644 ./images/affine.png /usr/local/share/doc/ImageMagick-7/images
/usr/bin/install -c -m 644 ./images/annotate.png /usr/local/share/doc/ImageMagick-7/images
/usr/bin/install -c -m 644 ./images/arc.png /usr/local/share/doc/ImageMagick-7/images
/usr/bin/install -c -m 644 ./images/atop.gif /usr/local/share/doc/ImageMagick-7/images
/usr/bin/install -c -m 644 ./images/background.jpg /usr/local/share/doc/ImageMagick-7/images
/usr/bin/install -c -m 644 ./images/bitcoin.svg /usr/local/share/doc/ImageMagick-7/images
/usr/bin/install -c -m 644 ./images/black.png /usr/local/share/doc/ImageMagick-7/images
/usr/bin/install -c -m 644 ./images/bluebells_clipped.jpg /usr/local/share/doc/ImageMagick-7/images
/usr/bin/install -c -m 644 ./images/bluebells_darker.jpg /usr/local/share/doc/ImageMagick-7/images
/usr/bin/install -c -m 644 ./images/bluebells_lin.jpg /usr/local/share/doc/ImageMagick-7/images
/usr/bin/install -c -m 644 ./images/bluebells_log.jpg /usr/local/share/doc/ImageMagick-7/images
/usr/bin/install -c -m 644 ./images/button.gif /usr/local/share/doc/ImageMagick-7/images
/usr/bin/install -c -m 644 ./images/color-thresholding.gif /usr/local/share/doc/ImageMagick-7/images
/usr/bin/install -c -m 644 ./images/color-thresholding-gray.gif /usr/local/share/doc/ImageMagick-7/images
/usr/bin/install -c -m 644 ./images/color-thresholding-hsv.gif /usr/local/share/doc/ImageMagick-7/images
/usr/bin/install -c -m 644 ./images/color-thresholding-hsv-rgb.gif /usr/local/share/doc/ImageMagick-7/images
/usr/bin/install -c -m 644 ./images/color-thresholding.jpg /usr/local/share/doc/ImageMagick-7/images
/usr/bin/install -c -m 644 ./images/color-thresholding-rgb.gif /usr/local/share/doc/ImageMagick-7/images
/usr/bin/install -c -m 644 ./images/configure.jpg /usr/local/share/doc/ImageMagick-7/images
/usr/bin/install -c -m 644 ./images/convex-hull-barn-closure.jpg /usr/local/share/doc/ImageMagick-7/images
/usr/bin/install -c -m 644 ./images/convex-hull-barn.jpg /usr/local/share/doc/ImageMagick-7/images
/usr/bin/install -c -m 644 ./images/convex-hull-blocks-closure.png /usr/local/share/doc/ImageMagick-7/images
/usr/bin/install -c -m 644 ./images/convex-hull-blocks.png /usr/local/share/doc/ImageMagick-7/images
/usr/bin/install -c -m 644 ./images/convex-hull.png /usr/local/share/doc/ImageMagick-7/images
/usr/bin/install -c -m 644 ./images/cylinder_shaded.png /usr/local/share/doc/ImageMagick-7/images
/usr/bin/install -c -m 644 ./images/difference.png /usr/local/share/doc/ImageMagick-7/images
/usr/bin/install -c -m 644 ./images/examples.jpg /usr/local/share/doc/ImageMagick-7/images
/usr/bin/install -c -m 644 ./images/frame.jpg /usr/local/share/doc/ImageMagick-7/images
/usr/bin/install -c -m 644 ./images/fuzzy-magick.png /usr/local/share/doc/ImageMagick-7/images
/usr/bin/install -c -m 644 ./images/gaussian-blur.png /usr/local/share/doc/ImageMagick-7/images
/usr/bin/install -c -m 644 ./images/granite.png /usr/local/share/doc/ImageMagick-7/images
/usr/bin/install -c -m 644 ./images/imade_art2.jpg /usr/local/share/doc/ImageMagick-7/images
/usr/bin/install -c -m 644 ./images/ImageMagick.ico /usr/local/share/doc/ImageMagick-7/images
/usr/bin/install -c -m 644 ./images/label.gif /usr/local/share/doc/ImageMagick-7/images
/usr/bin/install -c -m 644 ./images/logo.jpg /usr/local/share/doc/ImageMagick-7/images
/usr/bin/install -c -m 644 ./images/logo.png /usr/local/share/doc/ImageMagick-7/images
/usr/bin/install -c -m 644 ./images/logo-sm-flop.png /usr/local/share/doc/ImageMagick-7/images
/usr/bin/install -c -m 644 ./images/logo-sm-fx.png /usr/local/share/doc/ImageMagick-7/images
/usr/bin/install -c -m 644 ./images/logo-sm.png /usr/local/share/doc/ImageMagick-7/images
/usr/bin/install -c -m 644 ./images/montage.jpg /usr/local/share/doc/ImageMagick-7/images
/usr/bin/install -c -m 644 ./images/mountains-clahe.jpg /usr/local/share/doc/ImageMagick-7/images
/usr/bin/install -c -m 644 ./images/mountains-equalize.jpg /usr/local/share/doc/ImageMagick-7/images
/usr/bin/install -c -m 644 ./images/mountains.jpg /usr/local/share/doc/ImageMagick-7/images
/usr/bin/install -c -m 644 ./images/navy.png /usr/local/share/doc/ImageMagick-7/images
/usr/bin/install -c -m 644 ./images/objects.gif /usr/local/share/doc/ImageMagick-7/images
/usr/bin/install -c -m 644 ./images/objects.jpg /usr/local/share/doc/ImageMagick-7/images
/usr/bin/install -c -m 644 ./images/objects.png /usr/local/share/doc/ImageMagick-7/images
/usr/bin/install -c -m 644 ./images/over.gif /usr/local/share/doc/ImageMagick-7/images
/usr/bin/install -c -m 644 ./images/piechart.png /usr/local/share/doc/ImageMagick-7/images
/usr/bin/install -c -m 644 ./images/radial-gradient.png /usr/local/share/doc/ImageMagick-7/images
/usr/bin/install -c -m 644 ./images/reconstruct.jpg /usr/local/share/doc/ImageMagick-7/images
/usr/bin/install -c -m 644 ./images/red-ball.png /usr/local/share/doc/ImageMagick-7/images
/usr/bin/install -c -m 644 ./images/red-circle.png /usr/local/share/doc/ImageMagick-7/images
/usr/bin/install -c -m 644 ./images/right.gif /usr/local/share/doc/ImageMagick-7/images
/usr/bin/install -c -m 644 ./images/rose.jpg /usr/local/share/doc/ImageMagick-7/images
/usr/bin/install -c -m 644 ./images/rose-over.png /usr/local/share/doc/ImageMagick-7/images
/usr/bin/install -c -m 644 ./images/rose.png /usr/local/share/doc/ImageMagick-7/images
/usr/bin/install -c -m 644 ./images/rose.pnm /usr/local/share/doc/ImageMagick-7/images
/usr/bin/install -c -m 644 ./images/rose-sigmoidal.png /usr/local/share/doc/ImageMagick-7/images
/usr/bin/install -c -m 644 ./images/script.png /usr/local/share/doc/ImageMagick-7/images
/usr/bin/install -c -m 644 ./images/smile.gif /usr/local/share/doc/ImageMagick-7/images
/usr/bin/install -c -m 644 ./images/sponsor.jpg /usr/local/share/doc/ImageMagick-7/images
/usr/bin/install -c -m 644 ./images/sprite.jpg /usr/local/share/doc/ImageMagick-7/images
/usr/bin/install -c -m 644 ./images/t-shirt.png /usr/local/share/doc/ImageMagick-7/images
/usr/bin/install -c -m 644 ./images/wand.ico /usr/local/share/doc/ImageMagick-7/images
/usr/bin/install -c -m 644 ./images/wand.png /usr/local/share/doc/ImageMagick-7/images
/usr/bin/install -c -m 644 ./images/white-highlight.png /usr/local/share/doc/ImageMagick-7/images
/usr/bin/install -c -m 644 ./images/wizard.jpg /usr/local/share/doc/ImageMagick-7/images
/usr/bin/install -c -m 644 ./images/wizard.png /usr/local/share/doc/ImageMagick-7/images
mkdir -p -- /usr/local/share/doc/ImageMagick-7/images/patterns
/usr/bin/install -c -m 644 ./images/patterns/bricks.png /usr/local/share/doc/ImageMagick-7/images/patterns
/usr/bin/install -c -m 644 ./images/patterns/checkerboard.png /usr/local/share/doc/ImageMagick-7/images/patterns
/usr/bin/install -c -m 644 ./images/patterns/circles.png /usr/local/share/doc/ImageMagick-7/images/patterns
/usr/bin/install -c -m 644 ./images/patterns/crosshatch30.png /usr/local/share/doc/ImageMagick-7/images/patterns
/usr/bin/install -c -m 644 ./images/patterns/crosshatch45.png /usr/local/share/doc/ImageMagick-7/images/patterns
/usr/bin/install -c -m 644 ./images/patterns/crosshatch.png /usr/local/share/doc/ImageMagick-7/images/patterns
/usr/bin/install -c -m 644 ./images/patterns/fishscales.png /usr/local/share/doc/ImageMagick-7/images/patterns
/usr/bin/install -c -m 644 ./images/patterns/gray0.png /usr/local/share/doc/ImageMagick-7/images/patterns
/usr/bin/install -c -m 644 ./images/patterns/gray100.png /usr/local/share/doc/ImageMagick-7/images/patterns
/usr/bin/install -c -m 644 ./images/patterns/gray10.png /usr/local/share/doc/ImageMagick-7/images/patterns
/usr/bin/install -c -m 644 ./images/patterns/gray15.png /usr/local/share/doc/ImageMagick-7/images/patterns
/usr/bin/install -c -m 644 ./images/patterns/gray20.png /usr/local/share/doc/ImageMagick-7/images/patterns
/usr/bin/install -c -m 644 ./images/patterns/gray25.png /usr/local/share/doc/ImageMagick-7/images/patterns
/usr/bin/install -c -m 644 ./images/patterns/gray30.png /usr/local/share/doc/ImageMagick-7/images/patterns
/usr/bin/install -c -m 644 ./images/patterns/gray35.png /usr/local/share/doc/ImageMagick-7/images/patterns
/usr/bin/install -c -m 644 ./images/patterns/gray40.png /usr/local/share/doc/ImageMagick-7/images/patterns
/usr/bin/install -c -m 644 ./images/patterns/gray45.png /usr/local/share/doc/ImageMagick-7/images/patterns
/usr/bin/install -c -m 644 ./images/patterns/gray50.png /usr/local/share/doc/ImageMagick-7/images/patterns
/usr/bin/install -c -m 644 ./images/patterns/gray55.png /usr/local/share/doc/ImageMagick-7/images/patterns
/usr/bin/install -c -m 644 ./images/patterns/gray5.png /usr/local/share/doc/ImageMagick-7/images/patterns
/usr/bin/install -c -m 644 ./images/patterns/gray60.png /usr/local/share/doc/ImageMagick-7/images/patterns
/usr/bin/install -c -m 644 ./images/patterns/gray65.png /usr/local/share/doc/ImageMagick-7/images/patterns
/usr/bin/install -c -m 644 ./images/patterns/gray70.png /usr/local/share/doc/ImageMagick-7/images/patterns
/usr/bin/install -c -m 644 ./images/patterns/gray75.png /usr/local/share/doc/ImageMagick-7/images/patterns
/usr/bin/install -c -m 644 ./images/patterns/gray80.png /usr/local/share/doc/ImageMagick-7/images/patterns
/usr/bin/install -c -m 644 ./images/patterns/gray85.png /usr/local/share/doc/ImageMagick-7/images/patterns
/usr/bin/install -c -m 644 ./images/patterns/gray90.png /usr/local/share/doc/ImageMagick-7/images/patterns
/usr/bin/install -c -m 644 ./images/patterns/gray95.png /usr/local/share/doc/ImageMagick-7/images/patterns
/usr/bin/install -c -m 644 ./images/patterns/hexagons.png /usr/local/share/doc/ImageMagick-7/images/patterns
/usr/bin/install -c -m 644 ./images/patterns/horizontal2.png /usr/local/share/doc/ImageMagick-7/images/patterns
/usr/bin/install -c -m 644 ./images/patterns/horizontal3.png /usr/local/share/doc/ImageMagick-7/images/patterns
/usr/bin/install -c -m 644 ./images/patterns/horizontal.png /usr/local/share/doc/ImageMagick-7/images/patterns
/usr/bin/install -c -m 644 ./images/patterns/horizontalsaw.png /usr/local/share/doc/ImageMagick-7/images/patterns
/usr/bin/install -c -m 644 ./images/patterns/hs_bdiagonal.png /usr/local/share/doc/ImageMagick-7/images/patterns
/usr/bin/install -c -m 644 ./images/patterns/hs_cross.png /usr/local/share/doc/ImageMagick-7/images/patterns
/usr/bin/install -c -m 644 ./images/patterns/hs_diagcross.png /usr/local/share/doc/ImageMagick-7/images/patterns
/usr/bin/install -c -m 644 ./images/patterns/hs_fdiagonal.png /usr/local/share/doc/ImageMagick-7/images/patterns
/usr/bin/install -c -m 644 ./images/patterns/hs_horizontal.png /usr/local/share/doc/ImageMagick-7/images/patterns
/usr/bin/install -c -m 644 ./images/patterns/hs_vertical.png /usr/local/share/doc/ImageMagick-7/images/patterns
/usr/bin/install -c -m 644 ./images/patterns/left30.png /usr/local/share/doc/ImageMagick-7/images/patterns
/usr/bin/install -c -m 644 ./images/patterns/left45.png /usr/local/share/doc/ImageMagick-7/images/patterns
/usr/bin/install -c -m 644 ./images/patterns/leftshingle.png /usr/local/share/doc/ImageMagick-7/images/patterns
/usr/bin/install -c -m 644 ./images/patterns/octagons.png /usr/local/share/doc/ImageMagick-7/images/patterns
/usr/bin/install -c -m 644 ./images/patterns/right30.png /usr/local/share/doc/ImageMagick-7/images/patterns
/usr/bin/install -c -m 644 ./images/patterns/right45.png /usr/local/share/doc/ImageMagick-7/images/patterns
/usr/bin/install -c -m 644 ./images/patterns/rightshingle.png /usr/local/share/doc/ImageMagick-7/images/patterns
/usr/bin/install -c -m 644 ./images/patterns/smallfishscales.png /usr/local/share/doc/ImageMagick-7/images/patterns
/usr/bin/install -c -m 644 ./images/patterns/vertical2.png /usr/local/share/doc/ImageMagick-7/images/patterns
/usr/bin/install -c -m 644 ./images/patterns/vertical3.png /usr/local/share/doc/ImageMagick-7/images/patterns
/usr/bin/install -c -m 644 ./images/patterns/verticalbricks.png /usr/local/share/doc/ImageMagick-7/images/patterns
/usr/bin/install -c -m 644 ./images/patterns/verticalleftshingle.png /usr/local/share/doc/ImageMagick-7/images/patterns
/usr/bin/install -c -m 644 ./images/patterns/vertical.png /usr/local/share/doc/ImageMagick-7/images/patterns
/usr/bin/install -c -m 644 ./images/patterns/verticalrightshingle.png /usr/local/share/doc/ImageMagick-7/images/patterns
/usr/bin/install -c -m 644 ./images/patterns/verticalsaw.png /usr/local/share/doc/ImageMagick-7/images/patterns
mkdir -p -- /usr/local/share/doc/ImageMagick-7/www
/usr/bin/install -c -m 644 ./www/advanced-unix-installation.html /usr/local/share/doc/ImageMagick-7/www
/usr/bin/install -c -m 644 ./www/advanced-windows-installation.html /usr/local/share/doc/ImageMagick-7/www
/usr/bin/install -c -m 644 ./www/animate.html /usr/local/share/doc/ImageMagick-7/www
/usr/bin/install -c -m 644 ./www/architecture.html /usr/local/share/doc/ImageMagick-7/www
/usr/bin/install -c -m 644 ./www/changelog.html /usr/local/share/doc/ImageMagick-7/www
/usr/bin/install -c -m 644 ./www/cipher.html /usr/local/share/doc/ImageMagick-7/www
/usr/bin/install -c -m 644 ./www/cite.html /usr/local/share/doc/ImageMagick-7/www
/usr/bin/install -c -m 644 ./www/clahe.html /usr/local/share/doc/ImageMagick-7/www
/usr/bin/install -c -m 644 ./www/color.html /usr/local/share/doc/ImageMagick-7/www
/usr/bin/install -c -m 644 ./www/color-management.html /usr/local/share/doc/ImageMagick-7/www
/usr/bin/install -c -m 644 ./www/color-thresholding.html /usr/local/share/doc/ImageMagick-7/www
/usr/bin/install -c -m 644 ./www/command-line-options.html /usr/local/share/doc/ImageMagick-7/www
/usr/bin/install -c -m 644 ./www/command-line-processing.html /usr/local/share/doc/ImageMagick-7/www
/usr/bin/install -c -m 644 ./www/command-line-tools.html /usr/local/share/doc/ImageMagick-7/www
/usr/bin/install -c -m 644 ./www/compare.html /usr/local/share/doc/ImageMagick-7/www
/usr/bin/install -c -m 644 ./www/compose.html /usr/local/share/doc/ImageMagick-7/www
/usr/bin/install -c -m 644 ./www/composite.html /usr/local/share/doc/ImageMagick-7/www
/usr/bin/install -c -m 644 ./www/conjure.html /usr/local/share/doc/ImageMagick-7/www
/usr/bin/install -c -m 644 ./www/connected-components.html /usr/local/share/doc/ImageMagick-7/www
/usr/bin/install -c -m 644 ./www/contact.html /usr/local/share/doc/ImageMagick-7/www
/usr/bin/install -c -m 644 ./www/convert.html /usr/local/share/doc/ImageMagick-7/www
/usr/bin/install -c -m 644 ./www/convex-hull.html /usr/local/share/doc/ImageMagick-7/www
/usr/bin/install -c -m 644 ./www/defines.html /usr/local/share/doc/ImageMagick-7/www
/usr/bin/install -c -m 644 ./www/develop.html /usr/local/share/doc/ImageMagick-7/www
/usr/bin/install -c -m 644 ./www/display.html /usr/local/share/doc/ImageMagick-7/www
/usr/bin/install -c -m 644 ./www/distribute-pixel-cache.html /usr/local/share/doc/ImageMagick-7/www
/usr/bin/install -c -m 644 ./www/download.html /usr/local/share/doc/ImageMagick-7/www
/usr/bin/install -c -m 644 ./www/escape.html /usr/local/share/doc/ImageMagick-7/www
/usr/bin/install -c -m 644 ./www/examples.html /usr/local/share/doc/ImageMagick-7/www
/usr/bin/install -c -m 644 ./www/exception.html /usr/local/share/doc/ImageMagick-7/www
/usr/bin/install -c -m 644 ./www/export.html /usr/local/share/doc/ImageMagick-7/www
/usr/bin/install -c -m 644 ./www/favicon.ico /usr/local/share/doc/ImageMagick-7/www
/usr/bin/install -c -m 644 ./www/formats.html /usr/local/share/doc/ImageMagick-7/www
/usr/bin/install -c -m 644 ./www/fx.html /usr/local/share/doc/ImageMagick-7/www
/usr/bin/install -c -m 644 ./www/gradient.html /usr/local/share/doc/ImageMagick-7/www
/usr/bin/install -c -m 644 ./www/high-dynamic-range.html /usr/local/share/doc/ImageMagick-7/www
/usr/bin/install -c -m 644 ./www/history.html /usr/local/share/doc/ImageMagick-7/www
/usr/bin/install -c -m 644 ./www/identify.html /usr/local/share/doc/ImageMagick-7/www
/usr/bin/install -c -m 644 ./www/ImageMagickObject.html /usr/local/share/doc/ImageMagick-7/www
/usr/bin/install -c -m 644 ./www/import.html /usr/local/share/doc/ImageMagick-7/www
/usr/bin/install -c -m 644 ./www/index.html /usr/local/share/doc/ImageMagick-7/www
/usr/bin/install -c -m 644 ./www/install-source.html /usr/local/share/doc/ImageMagick-7/www
/usr/bin/install -c -m 644 ./www/jp2.html /usr/local/share/doc/ImageMagick-7/www
/usr/bin/install -c -m 644 ./www/license.html /usr/local/share/doc/ImageMagick-7/www
/usr/bin/install -c -m 644 ./www/links.html /usr/local/share/doc/ImageMagick-7/www
/usr/bin/install -c -m 644 ./www/magick-core.html /usr/local/share/doc/ImageMagick-7/www
/usr/bin/install -c -m 644 ./www/magick++.html /usr/local/share/doc/ImageMagick-7/www
/usr/bin/install -c -m 644 ./www/magick.html /usr/local/share/doc/ImageMagick-7/www
/usr/bin/install -c -m 644 ./www/magick-script.html /usr/local/share/doc/ImageMagick-7/www
/usr/bin/install -c -m 644 ./www/magick-vector-graphics.html /usr/local/share/doc/ImageMagick-7/www
/usr/bin/install -c -m 644 ./www/magick-wand.html /usr/local/share/doc/ImageMagick-7/www
/usr/bin/install -c -m 644 ./www/miff.html /usr/local/share/doc/ImageMagick-7/www
/usr/bin/install -c -m 644 ./www/mirror.html /usr/local/share/doc/ImageMagick-7/www
/usr/bin/install -c -m 644 ./www/mogrify.html /usr/local/share/doc/ImageMagick-7/www
/usr/bin/install -c -m 644 ./www/montage.html /usr/local/share/doc/ImageMagick-7/www
/usr/bin/install -c -m 644 ./www/motion-picture.html /usr/local/share/doc/ImageMagick-7/www
/usr/bin/install -c -m 644 ./www/news.html /usr/local/share/doc/ImageMagick-7/www
/usr/bin/install -c -m 644 ./www/opencl.html /usr/local/share/doc/ImageMagick-7/www
/usr/bin/install -c -m 644 ./www/openmp.html /usr/local/share/doc/ImageMagick-7/www
/usr/bin/install -c -m 644 ./www/perl-magick.html /usr/local/share/doc/ImageMagick-7/www
/usr/bin/install -c -m 644 ./www/porting.html /usr/local/share/doc/ImageMagick-7/www
/usr/bin/install -c -m 644 ./www/quantize.html /usr/local/share/doc/ImageMagick-7/www
/usr/bin/install -c -m 644 ./www/resources.html /usr/local/share/doc/ImageMagick-7/www
/usr/bin/install -c -m 644 ./www/search.html /usr/local/share/doc/ImageMagick-7/www
/usr/bin/install -c -m 644 ./www/security-policy.html /usr/local/share/doc/ImageMagick-7/www
/usr/bin/install -c -m 644 ./www/sitemap.html /usr/local/share/doc/ImageMagick-7/www
/usr/bin/install -c -m 644 ./www/stream.html /usr/local/share/doc/ImageMagick-7/www
/usr/bin/install -c -m 644 ./www/support.html /usr/local/share/doc/ImageMagick-7/www
/usr/bin/install -c -m 644 ./www/wand.png /usr/local/share/doc/ImageMagick-7/www
/usr/bin/install -c -m 644 ./www/webp.html /usr/local/share/doc/ImageMagick-7/www
mkdir -p -- /usr/local/share/doc/ImageMagick-7/www/assets
/usr/bin/install -c -m 644 ./www/assets/magick.css /usr/local/share/doc/ImageMagick-7/www/assets
/usr/bin/install -c -m 644 ./www/assets/magick.js /usr/local/share/doc/ImageMagick-7/www/assets
mkdir -p -- /usr/local/share/doc/ImageMagick-7/www/api
/usr/bin/install -c -m 644 ./www/api/animate.html /usr/local/share/doc/ImageMagick-7/www/api
/usr/bin/install -c -m 644 ./www/api/annotate.html /usr/local/share/doc/ImageMagick-7/www/api
/usr/bin/install -c -m 644 ./www/api/attribute.html /usr/local/share/doc/ImageMagick-7/www/api
/usr/bin/install -c -m 644 ./www/api/blob.html /usr/local/share/doc/ImageMagick-7/www/api
/usr/bin/install -c -m 644 ./www/api/cache.html /usr/local/share/doc/ImageMagick-7/www/api
/usr/bin/install -c -m 644 ./www/api/cache-view.html /usr/local/share/doc/ImageMagick-7/www/api
/usr/bin/install -c -m 644 ./www/api/channel.html /usr/local/share/doc/ImageMagick-7/www/api
/usr/bin/install -c -m 644 ./www/api/cipher.html /usr/local/share/doc/ImageMagick-7/www/api
/usr/bin/install -c -m 644 ./www/api/color.html /usr/local/share/doc/ImageMagick-7/www/api
/usr/bin/install -c -m 644 ./www/api/colormap.html /usr/local/share/doc/ImageMagick-7/www/api
/usr/bin/install -c -m 644 ./www/api/colorspace.html /usr/local/share/doc/ImageMagick-7/www/api
/usr/bin/install -c -m 644 ./www/api/compare.html /usr/local/share/doc/ImageMagick-7/www/api
/usr/bin/install -c -m 644 ./www/api/composite.html /usr/local/share/doc/ImageMagick-7/www/api
/usr/bin/install -c -m 644 ./www/api/constitute.html /usr/local/share/doc/ImageMagick-7/www/api
/usr/bin/install -c -m 644 ./www/api/decorate.html /usr/local/share/doc/ImageMagick-7/www/api
/usr/bin/install -c -m 644 ./www/api/deprecate.html /usr/local/share/doc/ImageMagick-7/www/api
/usr/bin/install -c -m 644 ./www/api/display.html /usr/local/share/doc/ImageMagick-7/www/api
/usr/bin/install -c -m 644 ./www/api/distort.html /usr/local/share/doc/ImageMagick-7/www/api
/usr/bin/install -c -m 644 ./www/api/draw.html /usr/local/share/doc/ImageMagick-7/www/api
/usr/bin/install -c -m 644 ./www/api/drawing-wand.html /usr/local/share/doc/ImageMagick-7/www/api
/usr/bin/install -c -m 644 ./www/api/effect.html /usr/local/share/doc/ImageMagick-7/www/api
/usr/bin/install -c -m 644 ./www/api/enhance.html /usr/local/share/doc/ImageMagick-7/www/api
/usr/bin/install -c -m 644 ./www/api/exception.html /usr/local/share/doc/ImageMagick-7/www/api
/usr/bin/install -c -m 644 ./www/api/feature.html /usr/local/share/doc/ImageMagick-7/www/api
/usr/bin/install -c -m 644 ./www/api/fourier.html /usr/local/share/doc/ImageMagick-7/www/api
/usr/bin/install -c -m 644 ./www/api/fx.html /usr/local/share/doc/ImageMagick-7/www/api
/usr/bin/install -c -m 644 ./www/api/histogram.html /usr/local/share/doc/ImageMagick-7/www/api
/usr/bin/install -c -m 644 ./www/api/image.html /usr/local/share/doc/ImageMagick-7/www/api
/usr/bin/install -c -m 644 ./www/api/Image++.html /usr/local/share/doc/ImageMagick-7/www/api
/usr/bin/install -c -m 644 ./www/api/image-view.html /usr/local/share/doc/ImageMagick-7/www/api
/usr/bin/install -c -m 644 ./www/api/layer.html /usr/local/share/doc/ImageMagick-7/www/api
/usr/bin/install -c -m 644 ./www/api/list.html /usr/local/share/doc/ImageMagick-7/www/api
/usr/bin/install -c -m 644 ./www/api/magick++-classes.html /usr/local/share/doc/ImageMagick-7/www/api
/usr/bin/install -c -m 644 ./www/api/magick-deprecate.html /usr/local/share/doc/ImageMagick-7/www/api
/usr/bin/install -c -m 644 ./www/api/magick.html /usr/local/share/doc/ImageMagick-7/www/api
/usr/bin/install -c -m 644 ./www/api/magick-image.html /usr/local/share/doc/ImageMagick-7/www/api
/usr/bin/install -c -m 644 ./www/api/magick-property.html /usr/local/share/doc/ImageMagick-7/www/api
/usr/bin/install -c -m 644 ./www/api/magick-wand.html /usr/local/share/doc/ImageMagick-7/www/api
/usr/bin/install -c -m 644 ./www/api/memory.html /usr/local/share/doc/ImageMagick-7/www/api
/usr/bin/install -c -m 644 ./www/api/mime.html /usr/local/share/doc/ImageMagick-7/www/api
/usr/bin/install -c -m 644 ./www/api/module.html /usr/local/share/doc/ImageMagick-7/www/api
/usr/bin/install -c -m 644 ./www/api/mogrify.html /usr/local/share/doc/ImageMagick-7/www/api
/usr/bin/install -c -m 644 ./www/api/monitor.html /usr/local/share/doc/ImageMagick-7/www/api
/usr/bin/install -c -m 644 ./www/api/montage.html /usr/local/share/doc/ImageMagick-7/www/api
/usr/bin/install -c -m 644 ./www/api/morphology.html /usr/local/share/doc/ImageMagick-7/www/api
/usr/bin/install -c -m 644 ./www/api/paint.html /usr/local/share/doc/ImageMagick-7/www/api
/usr/bin/install -c -m 644 ./www/api/pixel-iterator.html /usr/local/share/doc/ImageMagick-7/www/api
/usr/bin/install -c -m 644 ./www/api/pixel-wand.html /usr/local/share/doc/ImageMagick-7/www/api
/usr/bin/install -c -m 644 ./www/api/profile.html /usr/local/share/doc/ImageMagick-7/www/api
/usr/bin/install -c -m 644 ./www/api/property.html /usr/local/share/doc/ImageMagick-7/www/api
/usr/bin/install -c -m 644 ./www/api/quantize.html /usr/local/share/doc/ImageMagick-7/www/api
/usr/bin/install -c -m 644 ./www/api/registry.html /usr/local/share/doc/ImageMagick-7/www/api
/usr/bin/install -c -m 644 ./www/api/resize.html /usr/local/share/doc/ImageMagick-7/www/api
/usr/bin/install -c -m 644 ./www/api/resource.html /usr/local/share/doc/ImageMagick-7/www/api
/usr/bin/install -c -m 644 ./www/api/segment.html /usr/local/share/doc/ImageMagick-7/www/api
/usr/bin/install -c -m 644 ./www/api/shear.html /usr/local/share/doc/ImageMagick-7/www/api
/usr/bin/install -c -m 644 ./www/api/signature.html /usr/local/share/doc/ImageMagick-7/www/api
/usr/bin/install -c -m 644 ./www/api/statistic.html /usr/local/share/doc/ImageMagick-7/www/api
/usr/bin/install -c -m 644 ./www/api/stream.html /usr/local/share/doc/ImageMagick-7/www/api
/usr/bin/install -c -m 644 ./www/api/transform.html /usr/local/share/doc/ImageMagick-7/www/api
/usr/bin/install -c -m 644 ./www/api/version.html /usr/local/share/doc/ImageMagick-7/www/api
/usr/bin/install -c -m 644 ./www/api/wand-view.html /usr/local/share/doc/ImageMagick-7/www/api
mkdir -p -- /usr/local/share/doc/ImageMagick-7/www/source
/usr/bin/install -c -m 644 ./www/source/analyze.c /usr/local/share/doc/ImageMagick-7/www/source
/usr/bin/install -c -m 644 ./www/source/coder.xml /usr/local/share/doc/ImageMagick-7/www/source
/usr/bin/install -c -m 644 ./www/source/colors.xml /usr/local/share/doc/ImageMagick-7/www/source
/usr/bin/install -c -m 644 ./www/source/configure.xml /usr/local/share/doc/ImageMagick-7/www/source
/usr/bin/install -c -m 644 ./www/source/contrast.c /usr/local/share/doc/ImageMagick-7/www/source
/usr/bin/install -c -m 644 ./www/source/core.c /usr/local/share/doc/ImageMagick-7/www/source
/usr/bin/install -c -m 644 ./www/source/delegates.xml /usr/local/share/doc/ImageMagick-7/www/source
/usr/bin/install -c -m 644 ./www/source/english.xml /usr/local/share/doc/ImageMagick-7/www/source
/usr/bin/install -c -m 644 ./www/source/examples.pl /usr/local/share/doc/ImageMagick-7/www/source
/usr/bin/install -c -m 644 ./www/source/francais.xml /usr/local/share/doc/ImageMagick-7/www/source
/usr/bin/install -c -m 644 ./www/source/incantation.msl /usr/local/share/doc/ImageMagick-7/www/source
/usr/bin/install -c -m 644 ./www/source/locale.xml /usr/local/share/doc/ImageMagick-7/www/source
/usr/bin/install -c -m 644 ./www/source/log.xml /usr/local/share/doc/ImageMagick-7/www/source
/usr/bin/install -c -m 644 ./www/source/magic.xml /usr/local/share/doc/ImageMagick-7/www/source
/usr/bin/install -c -m 644 ./www/source/mgk.c /usr/local/share/doc/ImageMagick-7/www/source
/usr/bin/install -c -m 644 ./www/source/mime.xml /usr/local/share/doc/ImageMagick-7/www/source
/usr/bin/install -c -m 644 ./www/source/piechart.mvg /usr/local/share/doc/ImageMagick-7/www/source
/usr/bin/install -c -m 644 ./www/source/piechart.svg /usr/local/share/doc/ImageMagick-7/www/source
/usr/bin/install -c -m 644 ./www/source/policy.xml /usr/local/share/doc/ImageMagick-7/www/source
/usr/bin/install -c -m 644 ./www/source/quantization-table.xml /usr/local/share/doc/ImageMagick-7/www/source
/usr/bin/install -c -m 644 ./www/source/thresholds.xml /usr/local/share/doc/ImageMagick-7/www/source
/usr/bin/install -c -m 644 ./www/source/type-apple.xml /usr/local/share/doc/ImageMagick-7/www/source
/usr/bin/install -c -m 644 ./www/source/type-dejavu.xml /usr/local/share/doc/ImageMagick-7/www/source
/usr/bin/install -c -m 644 ./www/source/type-ghostscript.xml /usr/local/share/doc/ImageMagick-7/www/source
/usr/bin/install -c -m 644 ./www/source/type-urw-base35.xml /usr/local/share/doc/ImageMagick-7/www/source
/usr/bin/install -c -m 644 ./www/source/type-windows.xml /usr/local/share/doc/ImageMagick-7/www/source
/usr/bin/install -c -m 644 ./www/source/type.xml /usr/local/share/doc/ImageMagick-7/www/source
/usr/bin/install -c -m 644 ./www/source/wand.c /usr/local/share/doc/ImageMagick-7/www/source
mkdir -p -- /usr/local/share/doc/ImageMagick-7/www/Magick++
/usr/bin/install -c -m 644 ./www/Magick++/Blob.html /usr/local/share/doc/ImageMagick-7/www/Magick++
/usr/bin/install -c -m 644 ./www/Magick++/Cache.fig /usr/local/share/doc/ImageMagick-7/www/Magick++
/usr/bin/install -c -m 644 ./www/Magick++/Cache.png /usr/local/share/doc/ImageMagick-7/www/Magick++
/usr/bin/install -c -m 644 ./www/Magick++/Cache.svg /usr/local/share/doc/ImageMagick-7/www/Magick++
/usr/bin/install -c -m 644 ./www/Magick++/ChangeLog.html /usr/local/share/doc/ImageMagick-7/www/Magick++
/usr/bin/install -c -m 644 ./www/Magick++/CoderInfo.html /usr/local/share/doc/ImageMagick-7/www/Magick++
/usr/bin/install -c -m 644 ./www/Magick++/Color.html /usr/local/share/doc/ImageMagick-7/www/Magick++
/usr/bin/install -c -m 644 ./www/Magick++/Documentation.html /usr/local/share/doc/ImageMagick-7/www/Magick++
/usr/bin/install -c -m 644 ./www/Magick++/Drawable_example_1.png /usr/local/share/doc/ImageMagick-7/www/Magick++
/usr/bin/install -c -m 644 ./www/Magick++/Drawable.html /usr/local/share/doc/ImageMagick-7/www/Magick++
/usr/bin/install -c -m 644 ./www/Magick++/Enumerations.html /usr/local/share/doc/ImageMagick-7/www/Magick++
/usr/bin/install -c -m 644 ./www/Magick++/Exception.html /usr/local/share/doc/ImageMagick-7/www/Magick++
/usr/bin/install -c -m 644 ./www/Magick++/FormatCharacters.html /usr/local/share/doc/ImageMagick-7/www/Magick++
/usr/bin/install -c -m 644 ./www/Magick++/Future.html /usr/local/share/doc/ImageMagick-7/www/Magick++
/usr/bin/install -c -m 644 ./www/Magick++/Geometry.html /usr/local/share/doc/ImageMagick-7/www/Magick++
/usr/bin/install -c -m 644 ./www/Magick++/ImageDesign.html /usr/local/share/doc/ImageMagick-7/www/Magick++
/usr/bin/install -c -m 644 ./www/Magick++/Image.fig /usr/local/share/doc/ImageMagick-7/www/Magick++
/usr/bin/install -c -m 644 ./www/Magick++/Image++.html /usr/local/share/doc/ImageMagick-7/www/Magick++
/usr/bin/install -c -m 644 ./www/Magick++/Image.html /usr/local/share/doc/ImageMagick-7/www/Magick++
/usr/bin/install -c -m 644 ./www/Magick++/ImageMagick.png /usr/local/share/doc/ImageMagick-7/www/Magick++
/usr/bin/install -c -m 644 ./www/Magick++/Image.png /usr/local/share/doc/ImageMagick-7/www/Magick++
/usr/bin/install -c -m 644 ./www/Magick++/index.html /usr/local/share/doc/ImageMagick-7/www/Magick++
/usr/bin/install -c -m 644 ./www/Magick++/Install.html /usr/local/share/doc/ImageMagick-7/www/Magick++
/usr/bin/install -c -m 644 ./www/Magick++/magick.css /usr/local/share/doc/ImageMagick-7/www/Magick++
/usr/bin/install -c -m 644 ./www/Magick++/Magick++.png /usr/local/share/doc/ImageMagick-7/www/Magick++
/usr/bin/install -c -m 644 ./www/Magick++/Montage.html /usr/local/share/doc/ImageMagick-7/www/Magick++
/usr/bin/install -c -m 644 ./www/Magick++/montage-sample-framed.jpg /usr/local/share/doc/ImageMagick-7/www/Magick++
/usr/bin/install -c -m 644 ./www/Magick++/NEWS.html /usr/local/share/doc/ImageMagick-7/www/Magick++
/usr/bin/install -c -m 644 ./www/Magick++/PixelPacket.html /usr/local/share/doc/ImageMagick-7/www/Magick++
/usr/bin/install -c -m 644 ./www/Magick++/Pixels.html /usr/local/share/doc/ImageMagick-7/www/Magick++
/usr/bin/install -c -m 644 ./www/Magick++/Quantum.html /usr/local/share/doc/ImageMagick-7/www/Magick++
/usr/bin/install -c -m 644 ./www/Magick++/README.txt /usr/local/share/doc/ImageMagick-7/www/Magick++
/usr/bin/install -c -m 644 ./www/Magick++/right_triangle.png /usr/local/share/doc/ImageMagick-7/www/Magick++
/usr/bin/install -c -m 644 ./www/Magick++/STL.html /usr/local/share/doc/ImageMagick-7/www/Magick++
/usr/bin/install -c -m 644 ./www/Magick++/thumbnail-anatomy-framed.fig /usr/local/share/doc/ImageMagick-7/www/Magick++
/usr/bin/install -c -m 644 ./www/Magick++/thumbnail-anatomy-framed.jpg /usr/local/share/doc/ImageMagick-7/www/Magick++
/usr/bin/install -c -m 644 ./www/Magick++/thumbnail-anatomy-plain.fig /usr/local/share/doc/ImageMagick-7/www/Magick++
/usr/bin/install -c -m 644 ./www/Magick++/thumbnail-anatomy-plain.jpg /usr/local/share/doc/ImageMagick-7/www/Magick++
/usr/bin/install -c -m 644 ./www/Magick++/thumbnail-sample-framed.jpg /usr/local/share/doc/ImageMagick-7/www/Magick++
/usr/bin/install -c -m 644 ./www/Magick++/thumbnail-sample-plain.jpg /usr/local/share/doc/ImageMagick-7/www/Magick++
/usr/bin/install -c -m 644 ./www/Magick++/TypeMetric.html /usr/local/share/doc/ImageMagick-7/www/Magick++
 /usr/bin/mkdir -p '/usr/local/share/doc/ImageMagick-7'
 /usr/bin/install -c -m 644 LICENSE ChangeLog NEWS.txt '/usr/local/share/doc/ImageMagick-7'
 /usr/bin/mkdir -p '/usr/local/include/ImageMagick-7/Magick++'
 /usr/bin/install -c -m 644 Magick++/lib/Magick++/Blob.h Magick++/lib/Magick++/CoderInfo.h Magick++/lib/Magick++/Color.h Magick++/lib/Magick++/Drawable.h Magick++/lib/Magick++/Exception.h Magick++/lib/Magick++/Functions.h Magick++/lib/Magick++/Geometry.h Magick++/lib/Magick++/Image.h Magick++/lib/Magick++/Include.h Magick++/lib/Magick++/Montage.h Magick++/lib/Magick++/Pixels.h Magick++/lib/Magick++/ResourceLimits.h Magick++/lib/Magick++/SecurityPolicy.h Magick++/lib/Magick++/Statistic.h Magick++/lib/Magick++/STL.h Magick++/lib/Magick++/TypeMetric.h '/usr/local/include/ImageMagick-7/Magick++'
 /usr/bin/mkdir -p '/usr/local/include/ImageMagick-7'
 /usr/bin/install -c -m 644 Magick++/lib/Magick++.h '/usr/local/include/ImageMagick-7'
 /usr/bin/mkdir -p '/usr/local/share/man/man1'
 /usr/bin/install -c -m 644 MagickCore/MagickCore-config.1 MagickWand/MagickWand-config.1 Magick++/bin/Magick++-config.1 utilities/ImageMagick.1 utilities/animate.1 utilities/compare.1 utilities/composite.1 utilities/conjure.1 utilities/convert.1 utilities/display.1 utilities/identify.1 utilities/import.1 utilities/magick.1 utilities/magick-script.1 utilities/mogrify.1 utilities/montage.1 utilities/stream.1 '/usr/local/share/man/man1'
 /usr/bin/mkdir -p '/usr/local/lib/pkgconfig'
 /usr/bin/install -c -m 644 MagickCore/ImageMagick.pc MagickCore/MagickCore.pc MagickCore/ImageMagick-7.Q16HDRI.pc MagickCore/MagickCore-7.Q16HDRI.pc MagickWand/MagickWand.pc MagickWand/MagickWand-7.Q16HDRI.pc Magick++/lib/Magick++.pc Magick++/lib/Magick++-7.Q16HDRI.pc '/usr/local/lib/pkgconfig'
make[2]: Leaving directory '/home/ye/tool/ImageMagick-7.0.10-60'
make[1]: Leaving directory '/home/ye/tool/ImageMagick-7.0.10-60'
```

## make

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/ImageMagick-7.0.10-60$ make
make  all-am
make[1]: Entering directory '/home/ye/tool/ImageMagick-7.0.10-60'
  CC       utilities/magick.o
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-accelerate.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-animate.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-annotate.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-artifact.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-attribute.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-blob.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-cache.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-cache-view.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-channel.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-cipher.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-client.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-coder.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-color.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-colormap.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-colorspace.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-compare.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-composite.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-compress.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-configure.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-constitute.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-decorate.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-delegate.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-deprecate.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-display.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-distort.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-distribute-cache.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-draw.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-effect.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-enhance.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-exception.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-feature.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-fourier.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-fx.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-gem.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-geometry.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-histogram.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-identify.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-image.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-image-view.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-layer.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-linked-list.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-list.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-locale.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-log.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-magic.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-magick.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-matrix.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-memory.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-mime.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-module.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-monitor.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-montage.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-morphology.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-opencl.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-option.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-paint.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-pixel.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-policy.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-prepress.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-property.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-profile.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-quantize.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-quantum.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-quantum-export.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-quantum-import.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-random.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-registry.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-resample.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-resize.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-resource.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-segment.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-semaphore.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-shear.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-signature.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-splay-tree.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-static.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-statistic.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-stream.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-string.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-thread.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-timer.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-token.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-transform.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-threshold.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-type.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-utility.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-version.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-visual-effects.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-vision.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-widget.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-xml-tree.lo
  CC       MagickCore/libMagickCore_7_Q16HDRI_la-xwindow.lo
MagickCore/xwindow.c: In function ‘XMakeImage’:
MagickCore/xwindow.c:5420:5: warning: variable ‘length’ set but not used [-Wunused-but-set-variable]
 5420 |     length;
      |     ^~~~~~
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-aai.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-art.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-ashlar.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-avs.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-bgr.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-bmp.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-braille.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-cals.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-caption.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-cin.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-cip.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-clip.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-cmyk.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-cube.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-cut.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-dcm.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-dds.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-debug.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-dib.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-dng.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-dot.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-dpx.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-farbfeld.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-fax.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-fits.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-fl32.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-gif.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-gradient.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-gray.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-hald.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-hdr.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-histogram.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-hrz.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-html.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-icon.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-info.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-inline.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-ipl.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-jnx.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-json.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-kernel.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-label.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-mac.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-magick.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-map.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-mask.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-mat.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-matte.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-meta.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-miff.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-mono.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-mpc.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-mpr.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-msl.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-mtv.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-mvg.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-null.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-ora.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-otb.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-palm.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-pango.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-pattern.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-pcd.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-pcl.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-pcx.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-pdb.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-pdf.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-pes.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-pgx.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-pict.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-pix.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-plasma.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-pnm.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-ps2.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-ps3.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-ps.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-psd.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-pwp.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-raw.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-rgb.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-rgf.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-rla.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-rle.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-scr.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-screenshot.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-sct.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-sfw.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-sgi.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-sixel.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-stegano.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-sun.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-svg.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-tga.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-thumbnail.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-tile.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-tim2.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-tim.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-ttf.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-txt.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-uil.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-url.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-uyvy.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-vicar.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-vid.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-video.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-viff.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-vips.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-wbmp.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-wpg.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-xbm.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-xc.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-xcf.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-xpm.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-xps.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-xtrn.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-yaml.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-ycbcr.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-yuv.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-x.lo
  CC       coders/MagickCore_libMagickCore_7_Q16HDRI_la-xwd.lo
  CC       filters/MagickCore_libMagickCore_7_Q16HDRI_la-analyze.lo
  CCLD     MagickCore/libMagickCore-7.Q16HDRI.la
  CC       MagickWand/libMagickWand_7_Q16HDRI_la-animate.lo
  CC       MagickWand/libMagickWand_7_Q16HDRI_la-compare.lo
  CC       MagickWand/libMagickWand_7_Q16HDRI_la-composite.lo
  CC       MagickWand/libMagickWand_7_Q16HDRI_la-conjure.lo
  CC       MagickWand/libMagickWand_7_Q16HDRI_la-convert.lo
  CC       MagickWand/libMagickWand_7_Q16HDRI_la-deprecate.lo
  CC       MagickWand/libMagickWand_7_Q16HDRI_la-display.lo
  CC       MagickWand/libMagickWand_7_Q16HDRI_la-drawing-wand.lo
  CC       MagickWand/libMagickWand_7_Q16HDRI_la-identify.lo
  CC       MagickWand/libMagickWand_7_Q16HDRI_la-import.lo
  CC       MagickWand/libMagickWand_7_Q16HDRI_la-magick-cli.lo
  CC       MagickWand/libMagickWand_7_Q16HDRI_la-magick-image.lo
  CC       MagickWand/libMagickWand_7_Q16HDRI_la-magick-property.lo
  CC       MagickWand/libMagickWand_7_Q16HDRI_la-magick-wand.lo
  CC       MagickWand/libMagickWand_7_Q16HDRI_la-mogrify.lo
  CC       MagickWand/libMagickWand_7_Q16HDRI_la-montage.lo
  CC       MagickWand/libMagickWand_7_Q16HDRI_la-operation.lo
  CC       MagickWand/libMagickWand_7_Q16HDRI_la-pixel-iterator.lo
  CC       MagickWand/libMagickWand_7_Q16HDRI_la-pixel-wand.lo
  CC       MagickWand/libMagickWand_7_Q16HDRI_la-script-token.lo
  CC       MagickWand/libMagickWand_7_Q16HDRI_la-stream.lo
  CC       MagickWand/libMagickWand_7_Q16HDRI_la-wand.lo
  CC       MagickWand/libMagickWand_7_Q16HDRI_la-wandcli.lo
  CC       MagickWand/libMagickWand_7_Q16HDRI_la-wand-view.lo
  CCLD     MagickWand/libMagickWand-7.Q16HDRI.la
  CCLD     utilities/magick
  CXX      Magick++/lib/libMagick___7_Q16HDRI_la-Blob.lo
  CXX      Magick++/lib/libMagick___7_Q16HDRI_la-BlobRef.lo
  CXX      Magick++/lib/libMagick___7_Q16HDRI_la-CoderInfo.lo
  CXX      Magick++/lib/libMagick___7_Q16HDRI_la-Color.lo
  CXX      Magick++/lib/libMagick___7_Q16HDRI_la-Drawable.lo
  CXX      Magick++/lib/libMagick___7_Q16HDRI_la-Exception.lo
  CXX      Magick++/lib/libMagick___7_Q16HDRI_la-Functions.lo
  CXX      Magick++/lib/libMagick___7_Q16HDRI_la-Geometry.lo
  CXX      Magick++/lib/libMagick___7_Q16HDRI_la-Image.lo
  CXX      Magick++/lib/libMagick___7_Q16HDRI_la-ImageRef.lo
  CXX      Magick++/lib/libMagick___7_Q16HDRI_la-Montage.lo
  CXX      Magick++/lib/libMagick___7_Q16HDRI_la-Options.lo
  CXX      Magick++/lib/libMagick___7_Q16HDRI_la-Pixels.lo
  CXX      Magick++/lib/libMagick___7_Q16HDRI_la-ResourceLimits.lo
  CXX      Magick++/lib/libMagick___7_Q16HDRI_la-SecurityPolicy.lo
  CXX      Magick++/lib/libMagick___7_Q16HDRI_la-Statistic.lo
  CXX      Magick++/lib/libMagick___7_Q16HDRI_la-STL.lo
  CXX      Magick++/lib/libMagick___7_Q16HDRI_la-Thread.lo
  CXX      Magick++/lib/libMagick___7_Q16HDRI_la-TypeMetric.lo
  CXXLD    Magick++/lib/libMagick++-7.Q16HDRI.la
cp -f MagickCore/ImageMagick.pc MagickCore/ImageMagick-7.Q16HDRI.pc
cp -f MagickCore/MagickCore.pc MagickCore/MagickCore-7.Q16HDRI.pc
cp -f MagickWand/MagickWand.pc MagickWand/MagickWand-7.Q16HDRI.pc
cp -f Magick++/lib/Magick++.pc Magick++/lib/Magick++-7.Q16HDRI.pc
make[1]: Leaving directory '/home/ye/tool/ImageMagick-7.0.10-60'
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/ImageMagick-7.0.10-60$
```

## ldconfig

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/ImageMagick-7.0.10-60$ convert --help
convert: error while loading shared libraries: libMagickCore-7.Q16HDRI.so.8: cannot open shared object file: No such file or directory
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/ImageMagick-7.0.10-60$ convert -help
convert: error while loading shared libraries: libMagickCore-7.Q16HDRI.so.8: cannot open shared object file: No such file or directory
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/ImageMagick-7.0.10-60$ sudo ldconfig /usr/local/lib
```

## convert -help

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/ImageMagick-7.0.10-60$ convert -help
Version: ImageMagick 7.0.10-60 Q16 x86_64 2021-01-25 https://imagemagick.org
Copyright: (C) 1999-2021 ImageMagick Studio LLC
License: https://imagemagick.org/script/license.php
Features: Cipher DPC HDRI OpenMP(4.5) 
Delegates (built-in): x zlib
Usage: convert [options ...] file [ [options ...] file ...] [options ...] file

Image Settings:
  -adjoin              join images into a single multi-image file
  -affine matrix       affine transform matrix
  -alpha option        activate, deactivate, reset, or set the alpha channel
  -antialias           remove pixel-aliasing
  -authenticate password
                       decipher image with this password
  -attenuate value     lessen (or intensify) when adding noise to an image
  -background color    background color
  -bias value          add bias when convolving an image
  -black-point-compensation
                       use black point compensation
  -blue-primary point  chromaticity blue primary point
  -bordercolor color   border color
  -caption string      assign a caption to an image
  -clip                clip along the first path from the 8BIM profile
  -clip-mask filename  associate a clip mask with the image
  -clip-path id        clip along a named path from the 8BIM profile
  -colorspace type     alternate image colorspace
  -comment string      annotate image with comment
  -compose operator    set image composite operator
  -compress type       type of pixel compression when writing the image
  -define format:option
                       define one or more image format options
  -delay value         display the next image after pausing
  -density geometry    horizontal and vertical density of the image
  -depth value         image depth
  -direction type      render text right-to-left or left-to-right
  -display server      get image or font from this X server
  -dispose method      layer disposal method
  -dither method       apply error diffusion to image
  -encoding type       text encoding type
  -endian type         endianness (MSB or LSB) of the image
  -family name         render text with this font family
  -features distance   analyze image features (e.g. contrast, correlation)
  -fill color          color to use when filling a graphic primitive
  -filter type         use this filter when resizing an image
  -font name           render text with this font
  -format "string"     output formatted image characteristics
  -fuzz distance       colors within this distance are considered equal
  -gravity type        horizontal and vertical text placement
  -green-primary point chromaticity green primary point
  -intensity method    method to generate an intensity value from a pixel
  -intent type         type of rendering intent when managing the image color
  -interlace type      type of image interlacing scheme
  -interline-spacing value
                       set the space between two text lines
  -interpolate method  pixel color interpolation method
  -interword-spacing value
                       set the space between two words
  -kerning value       set the space between two letters
  -label string        assign a label to an image
  -limit type value    pixel cache resource limit
  -loop iterations     add Netscape loop extension to your GIF animation
  -matte               store matte channel if the image has one
  -mattecolor color    frame color
  -moments             report image moments
  -monitor             monitor progress
  -orient type         image orientation
  -page geometry       size and location of an image canvas (setting)
  -ping                efficiently determine image attributes
  -pointsize value     font point size
  -precision value     maximum number of significant digits to print
  -preview type        image preview type
  -quality value       JPEG/MIFF/PNG compression level
  -quiet               suppress all warning messages
  -read-mask filename  associate a read mask with the image
  -red-primary point   chromaticity red primary point
  -regard-warnings     pay attention to warning messages
  -remap filename      transform image colors to match this set of colors
  -repage geometry     size and location of an image canvas
  -respect-parentheses settings remain in effect until parenthesis boundary
  -sampling-factor geometry
                       horizontal and vertical sampling factor
  -scene value         image scene number
  -seed value          seed a new sequence of pseudo-random numbers
  -size geometry       width and height of image
  -stretch type        render text with this font stretch
  -stroke color        graphic primitive stroke color
  -strokewidth value   graphic primitive stroke width
  -style type          render text with this font style
  -support factor      resize support: > 1.0 is blurry, < 1.0 is sharp
  -synchronize         synchronize image to storage device
  -taint               declare the image as modified
  -texture filename    name of texture to tile onto the image background
  -tile-offset geometry
                       tile offset
  -treedepth value     color tree depth
  -transparent-color color
                       transparent color
  -undercolor color    annotation bounding box color
  -units type          the units of image resolution
  -verbose             print detailed information about the image
  -view                FlashPix viewing transforms
  -virtual-pixel method
                       virtual pixel access method
  -weight type         render text with this font weight
  -white-point point   chromaticity white point
  -write-mask filename associate a write mask with the image

Image Operators:
  -adaptive-blur geometry
                       adaptively blur pixels; decrease effect near edges
  -adaptive-resize geometry
                       adaptively resize image using 'mesh' interpolation
  -adaptive-sharpen geometry
                       adaptively sharpen pixels; increase effect near edges
  -alpha option        on, activate, off, deactivate, set, opaque, copy
                       transparent, extract, background, or shape
  -annotate geometry text
                       annotate the image with text
  -auto-gamma          automagically adjust gamma level of image
  -auto-level          automagically adjust color levels of image
  -auto-orient         automagically orient (rotate) image
  -auto-threshold method
                       automatically perform image thresholding
  -bench iterations    measure performance
  -bilateral-blur geometry
                       non-linear, edge-preserving, and noise-reducing smoothing filter
  -black-threshold value
                       force all pixels below the threshold into black
  -blue-shift factor   simulate a scene at nighttime in the moonlight
  -blur geometry       reduce image noise and reduce detail levels
  -border geometry     surround image with a border of color
  -bordercolor color   border color
  -brightness-contrast geometry
                       improve brightness / contrast of the image
  -canny geometry      detect edges in the image
  -cdl filename        color correct with a color decision list
  -channel mask        set the image channel mask
  -charcoal radius     simulate a charcoal drawing
  -chop geometry       remove pixels from the image interior
  -clahe geometry      contrast limited adaptive histogram equalization
  -clamp               keep pixel values in range (0-QuantumRange)
  -colorize value      colorize the image with the fill color
  -color-matrix matrix apply color correction to the image
  -colors value        preferred number of colors in the image
  -connected-components connectivity
                       connected-components uniquely labeled
  -contrast            enhance or reduce the image contrast
  -contrast-stretch geometry
                       improve contrast by 'stretching' the intensity range
  -convolve coefficients
                       apply a convolution kernel to the image
  -cycle amount        cycle the image colormap
  -decipher filename   convert cipher pixels to plain pixels
  -deskew threshold    straighten an image
  -despeckle           reduce the speckles within an image
  -distort method args
                       distort images according to given method ad args
  -draw string         annotate the image with a graphic primitive
  -edge radius         apply a filter to detect edges in the image
  -encipher filename   convert plain pixels to cipher pixels
  -emboss radius       emboss an image
  -enhance             apply a digital filter to enhance a noisy image
  -equalize            perform histogram equalization to an image
  -evaluate operator value
                       evaluate an arithmetic, relational, or logical expression
  -extent geometry     set the image size
  -extract geometry    extract area from image
  -fft                 implements the discrete Fourier transform (DFT)
  -flip                flip image vertically
  -floodfill geometry color
                       floodfill the image with color
  -flop                flop image horizontally
  -frame geometry      surround image with an ornamental border
  -function name parameters
                       apply function over image values
  -gamma value         level of gamma correction
  -gaussian-blur geometry
                       reduce image noise and reduce detail levels
  -geometry geometry   preferred size or location of the image
  -grayscale method    convert image to grayscale
  -hough-lines geometry
                       identify lines in the image
  -identify            identify the format and characteristics of the image
  -ift                 implements the inverse discrete Fourier transform (DFT)
  -implode amount      implode image pixels about the center
  -kmeans geometry     K means color reduction
  -kuwahara geometry   edge preserving noise reduction filter
  -lat geometry        local adaptive thresholding
  -level value         adjust the level of image contrast
  -level-colors color,color
                       level image with the given colors
  -linear-stretch geometry
                       improve contrast by 'stretching with saturation'
  -liquid-rescale geometry
                       rescale image with seam-carving
  -local-contrast geometry
                       enhance local contrast
  -mean-shift geometry delineate arbitrarily shaped clusters in the image
  -median geometry     apply a median filter to the image
  -mode geometry       make each pixel the 'predominant color' of the
                       neighborhood
  -modulate value      vary the brightness, saturation, and hue
  -monochrome          transform image to black and white
  -morphology method kernel
                       apply a morphology method to the image
  -motion-blur geometry
                       simulate motion blur
  -negate              replace every pixel with its complementary color 
  -noise geometry      add or reduce noise in an image
  -normalize           transform image to span the full range of colors
  -opaque color        change this color to the fill color
  -ordered-dither NxN
                       add a noise pattern to the image with specific
                       amplitudes
  -paint radius        simulate an oil painting
  -perceptible epsilon
                       pixel value less than |epsilon| become epsilon or
                       -epsilon
  -polaroid angle      simulate a Polaroid picture
  -posterize levels    reduce the image to a limited number of color levels
  -profile filename    add, delete, or apply an image profile
  -quantize colorspace reduce colors in this colorspace
  -raise value         lighten/darken image edges to create a 3-D effect
  -random-threshold low,high
                       random threshold the image
  -range-threshold values
                       perform either hard or soft thresholding within some range of values in an image
  -region geometry     apply options to a portion of the image
  -render              render vector graphics
  -resample geometry   change the resolution of an image
  -resize geometry     resize the image
  -roll geometry       roll an image vertically or horizontally
  -rotate degrees      apply Paeth rotation to the image
  -rotational-blur angle
                       rotational blur the image
  -sample geometry     scale image with pixel sampling
  -scale geometry      scale the image
  -segment values      segment an image
  -selective-blur geometry
                       selectively blur pixels within a contrast threshold
  -sepia-tone threshold
                       simulate a sepia-toned photo
  -set property value  set an image property
  -shade degrees       shade the image using a distant light source
  -shadow geometry     simulate an image shadow
  -sharpen geometry    sharpen the image
  -shave geometry      shave pixels from the image edges
  -shear geometry      slide one edge of the image along the X or Y axis
  -sigmoidal-contrast geometry
                       increase the contrast without saturating highlights or
                       shadows
  -sketch geometry     simulate a pencil sketch
  -solarize threshold  negate all pixels above the threshold level
  -sort-pixels         sort each scanline in ascending order of intensity
  -sparse-color method args
                       fill in a image based on a few color points
  -splice geometry     splice the background color into the image
  -spread radius       displace image pixels by a random amount
  -statistic type geometry
                       replace each pixel with corresponding statistic from the
                       neighborhood
  -strip               strip image of all profiles and comments
  -swirl degrees       swirl image pixels about the center
  -threshold value     threshold the image
  -thumbnail geometry  create a thumbnail of the image
  -tile filename       tile image when filling a graphic primitive
  -tint value          tint the image with the fill color
  -transform           affine transform image
  -transparent color   make this color transparent within the image
  -transpose           flip image vertically and rotate 90 degrees
  -transverse          flop image horizontally and rotate 270 degrees
  -trim                trim image edges
  -type type           image type
  -unique-colors       discard all but one of any pixel color
  -unsharp geometry    sharpen the image
  -vignette geometry   soften the edges of the image in vignette style
  -wave geometry       alter an image along a sine wave
  -wavelet-denoise threshold
                       removes noise from the image using a wavelet transform
  -white-balance       automagically adjust white balance of image
  -white-threshold value
                       force all pixels above the threshold into white

Image Channel Operators:
  -channel-fx expression
                       exchange, extract, or transfer one or more image channels
  -separate            separate an image channel into a grayscale image

Image Sequence Operators:
  -append              append an image sequence
  -clut                apply a color lookup table to the image
  -coalesce            merge a sequence of images
  -combine             combine a sequence of images
  -compare             mathematically and visually annotate the difference between an image and its reconstruction
  -complex operator    perform complex mathematics on an image sequence
  -composite           composite image
  -copy geometry offset
                       copy pixels from one area of an image to another
  -crop geometry       cut out a rectangular region of the image
  -deconstruct         break down an image sequence into constituent parts
  -evaluate-sequence operator
                       evaluate an arithmetic, relational, or logical expression
  -flatten             flatten a sequence of images
  -fx expression       apply mathematical expression to an image channel(s)
  -hald-clut           apply a Hald color lookup table to the image
  -layers method       optimize, merge, or compare image layers
  -morph value         morph an image sequence
  -mosaic              create a mosaic from an image sequence
  -poly terms          build a polynomial from the image sequence and the corresponding
                       terms (coefficients and degree pairs).
  -print string        interpret string and print to console
  -process arguments   process the image with a custom image filter
  -smush geometry      smush an image sequence together
  -write filename      write images to this file

Image Stack Operators:
  -clone indexes       clone an image
  -delete indexes      delete the image from the image sequence
  -duplicate count,indexes
                       duplicate an image one or more times
  -insert index        insert last image into the image sequence
  -reverse             reverse image sequence
  -swap indexes        swap two images in the image sequence

Miscellaneous Options:
  -debug events        display copious debugging information
  -distribute-cache port
                       distributed pixel cache spanning one or more servers
  -help                print program options
  -list type           print a list of supported option arguments
  -log format          format of debugging information
  -version             print version information

By default, the image format of 'file' is determined by its magic
number.  To specify a particular image format, precede the filename
with an image format name and a colon (i.e. ps:image) or specify the
image type as the filename suffix (i.e. image.ps).  Specify 'file' as
'-' for standard input or output.
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/ImageMagick-7.0.10-60$
```
