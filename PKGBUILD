#
# Contributor: {{ nome_do_autor(); }}
#

pkgname=neofetch
pkgver=7.1.0
pkgrel=2
pkgdesc="Uma ferramenta de informações do sistema CLI escrita em BASH que oferece suporte à exibição de imagens."
arch=('any')
url="http://localhost/neofetch"
license=('MIT')
depends=('bash')
makedepends=('git')
backup=('etc/neofetch/config.conf')
optdepends=(
    'catimg: Exibir imagens'
    'chafa: Suporte de imagem para texto'
    'feh: Exibição de papel de parede'
    'imagemagick: Remoção de imagem/Criação de miniaturas/Captura de tela'
    'jp2a: Exibir imagens'
    'libcaca: Exibir imagens'
    'nitrogen: Exibição de papel de parede'
    'w3m: Exibir imagens'
    'xdotool: Para imagens no console.'
    'xorg-xdpyinfo: Detecção de resolução (monitor único)'
    'xorg-xprop: Ambiente de trabalho e gerenciador de janelas'
    'xorg-xrandr: Detecção de resolução (Multi Monitor + Taxas de atualização)'
    'xorg-xwininfo: Para imagens no console.'
)

source=("neofetch.tar.gz")
validpgpkeys=("SKIP")
sha256sums=('SKIP')

package()
{
    cd "${pkgname}"
    make DESTDIR="$pkgdir" install
    install -Dm644 LICENSE.md "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE.md"
}
