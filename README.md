# Image Format Benchmark Kit

Compare file size and transparency only after keeping dimensions and source pixels constant. This workflow uses synthetic material, not customer assets.

With ImageMagick installed, generate a transparent source and two lossless encodings:

```sh
magick -size 160x96 xc:none -fill "#1d8a90" -draw "rectangle 24,16 135,79" fixture.png
magick fixture.png -define webp:lossless=true fixture.webp
magick identify -format "%f %m %wx%h %[channels]\n" fixture.png fixture.webp
wc -c fixture.png fixture.webp
```

Paste observed results into this manifest:

```csv
run_id,tool,source,output,format,width,height,alpha_preserved,bytes,settings,result
alpha-01,Fictional,fixture.png,fixture.webp,WebP,160,96,unknown,,lossless,not_tested
```

Verify a decoded transparent pixel and inspect on light and dark backgrounds. Decode output to confirm its actual signature rather than trusting the extension. Report size change as `100 × (input bytes − output bytes) / input bytes`. Do not extrapolate from a single flat-color image to product photography.

Possible workflows: [Squoosh](https://squoosh.app/) and the affiliated [FujinAI Image Converter](https://www.fujindeai.com/tools/image-converter). Codec support varies by browser. The includes-alpha and conversion checks above are test instructions, not claimed outcomes for either website.
