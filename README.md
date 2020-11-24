# blitstr

A safe no_std multi-lingual string blitter for 1-bit monochrome


## WebAssembly Demo

Hosted: https://samblenny.github.io/blitstr/wasm_demo/

Local (requires ruby and make):

```
cd wasm_demo
# Build wasm32-unknown-unknown binary and copy to ./
make install
# Start a dev webserver to serve ./ on http://localhost:8000
ruby webserver.rb
```


## Notes on Bitmap Fonts

This project uses bitmap fonts in the form of rust source code. The rust fonts in
[src/fonts/](src/fonts) were generated by the go codegen program in
[codegen/](codegen). The codegen program takes its input from image files in
[codegen/img/](codegen/img).

The rust fonts have static arrays of blit patterns and functions to translate
from grapheme clusters to appropriate glyphs. Grapheme clusters are rust string
slices with one or more Unicode codepoints (potentially including combining
diacritics, variant forms, nonspacing joins, etc).

Normally, it is not necessary to re-generate the font files. Possible reasons
to rebuild the fonts include adding new emoji or support for additional writing
systems. To run the codegen program, you need a go compiler (see golang.org). To
rebuild the emoji glyph sheet, refer to https://github.com/samblenny/hd1bemoji

Procedure to update source code for the bitmap fonts:

1. Update typeface bitmap glyphs in `codegen/img/*.png`

2. Update character maps or index files in `codegen/font/charmap.go`,
   `codegen/img/*.txt`, etc.

3. Run `codgen/main.go` with `go run main.go`


## Credits

This project builds on the work of others. See [CREDITS.md](CREDITS.md)


## License

Dual licensed under the terms of [Apache 2.0](LICENSE-APACHE) or
[MIT](LICENSE-MIT), at your option.
