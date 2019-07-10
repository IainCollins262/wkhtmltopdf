wkhtmltopdf and wkhtmltoimage
-----------------------------

wkhtmltopdf and wkhtmltoimage are command line tools to render HTML into PDF
and various image formats using the QT Webkit rendering engine. These run
entirely "headless" and do not require a display or display service.

See http://wkhtmltopdf.org for updated documentation.


Build Instructions (For future me)
----------------------------------

sed -i -e 's/    SYNCQT_OPTS=/    SYNCQT_OPTS=-quiet/g' qt/configure
test -n "$CC"  && unset CC
test -n "$CXX" && unset CXX
git clone https://github.com/IainCollins262/packaging.git ../packaging

sudo -H pip install -q conan pyyaml --ignore-installed six
sudo gem install fpm --no-ri --no-rdoc
sudo xcode-select --switch /Library/Developer/CommandLineTools
MACOSX_DEPLOYMENT_TARGET=10.10 ../packaging/build vagrant macos-cocoa --clean --version - - $PWD;

AFTERWARDS - run this to put everything back
--------------------------------------------
export CC=/Applications/Xcode.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/bin/clang
export CXX=/Applications/Xcode.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/bin/clang++
sudo xcode-select --reset
