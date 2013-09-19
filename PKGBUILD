# Maintainer: Kevin Mäder <kmaeder[AT]kevin-maeder[dot]de>
# TU Dresden corporate design font install

# copy DIN_Bd_PS.zip and Univers_PS.zip to directory with PKGBUILD

pkgname=texlive-tud-cd-fonts
pkgver=0.1
pkgrel=1
pkgdesc="TeX Live - TU Dresden corporate design fonts"
license=('custom:tud-cd-fonts')
arch=('any')
depends=('texlive-core')
url=("latex.wcms-file3.tu-dresden.de/phpBB3/index.php")
install=texlive.install
source=("DIN_Bd_PS.zip" "Univers_PS.zip" "git://github.com/kmaeder/texlive-tud-cd-fonts.git")
md5sums=('SKIP' 'SKIP' 'SKIP')

# if you change the path here make sure to change it in texlive.install too
TEXPATH=/usr/share/texmf

build() {
	cd $srcdir
	echo ">>> rename font files"
	mv -f DINBd___.pfb dinb8a.pfb
	mv -f DINBd___.afm dinb8a.afm
	mv -f uvceb___.pfb aunb8a.pfb
	mv -f uvceb___.afm aunb8a.afm
	mv -f uvcel___.pfb aunl8a.pfb
	mv -f uvcel___.afm aunl8a.afm
	mv -f uvceo___.pfb aunro8a.pfb
	mv -f uvceo___.afm aunro8a.afm
	mv -f uvxbo___.pfb aunbo8a.pfb
	mv -f uvxbo___.afm aunbo8a.afm
	mv -f uvxlo___.pfb aunlo8a.pfb
	mv -f uvxlo___.afm aunlo8a.afm
	mv -f uvce____.pfb aunr8a.pfb
	mv -f uvce____.afm aunr8a.afm
	mv -f uvczo___.pfb aubro8a.pfb
	mv -f uvczo___.afm aubro8a.afm
	mv -f uvcz____.pfb aubr8a.pfb
	mv -f uvcz____.afm aubr8a.afm

echo ">>> create latex font and metric files"
# cat > convert.tex <<%EOF
# \\input fontinst.sty
# \\needsfontinstversion{1.933}
# \\recordtransforms{tud-cd-fonts-rec.tex}
# \\latinfamily{din}{}
# \\latinfamily{aun}{}
# \\latinfamily{aub}{}
# \\endrecordtransforms
# \\bye
# %EOF
latex texlive-tud-cd-fonts/convertfonts.tex 1> /dev/null

# now we have files of type .afm .fd, .mtx, .pfb, .pl, .vpl
echo ">>> convert font and metric files to machine readable format"
for f in *.pl ; do
    pltotf $f 1> /dev/null
done

for f in *.vpl ; do
    vptovf $f 1> /dev/null
done

echo ">>> create map files"
# rm convert.tex
# cat > convert.tex <<%EOF
# \\input finstmsc.sty
# \\resetstr{PSfontsuffix}{.pfb}
# \\adddriver{dvips}{tud-cd-fonts.map}
# \\input tud-cd-fonts-rec.tex
# \\donedrivers
# \\bye
# %EOF
latex texlive-tud-cd-fonts/createmap.tex 1> /dev/null
}

package() {
	mkdir -p $pkgdir$TEXPATH/tex/latex/tud-cd-fonts
	mkdir -p $pkgdir$TEXPATH/fonts/tfm/adobe/tud-cd-fonts
	mkdir -p $pkgdir$TEXPATH/fonts/vf/adobe/tud-cd-fonts
	mkdir -p $pkgdir$TEXPATH/fonts/type1/adobe/tud-cd-fonts
	mkdir -p $pkgdir$TEXPATH/fonts/map
	mkdir -p $pkgdir$TEXPATH/web2c
	cp *.fd  $pkgdir$TEXPATH/tex/latex/tud-cd-fonts/
	cp *.tfm $pkgdir$TEXPATH/fonts/tfm/adobe/tud-cd-fonts/
	cp *.vf  $pkgdir$TEXPATH/fonts/vf/adobe/tud-cd-fonts/
	cp *.pfb $pkgdir$TEXPATH/fonts/type1/adobe/tud-cd-fonts/
	cp tud-cd-fonts.map $pkgdir$TEXPATH/fonts/map

	install -D -m 644 texlive-tud-cd-fonts/LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE:tud-cd-fonts"
}
