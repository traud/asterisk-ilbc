# Asterisk patch for iLBC 20

Asterisk already supports iLBC 30. This patch adds [iLBC 20](http://tools.ietf.org/html/rfc3952). Now, Asterisk defaults to iLBC 20 but falls back to iLBC 30, when the remote party requests this.

## Installing the patch

The patch was built on top of Asterisk 13.7.2. If you use a newer version and the patch fails, please, [report](http://help.github.com/articles/creating-an-issue/)!

    cd /usr/src/
    wget downloads.asterisk.org/pub/telephony/asterisk/asterisk-13-current.tar.gz
    tar zxf ./asterisk*
    cd ./asterisk*
    sudo apt-get --assume-yes install build-essential libssl-dev libncurses-dev libnewt-dev libxml2-dev libsqlite3-dev uuid-dev libjansson-dev libblocksruntime-dev

Apply all patches:

    wget github.com/traud/asterisk-ilbc/archive/master.zip
    unzip -qq master.zip
    rm master.zip
    cp --verbose --recursive ./asterisk-ilbc*/* ./
    patch -p0 <./codec_ilbc.patch

Compile and install:

    make --jobs
    sudo make install

## Testing
You can test iLBC 20 with

* Symbian/S60, since 3rd Edition Feature Pack 2, like [Nokia N79](http://www.gsmarena.com/compare.php3?idPhone1=2497&idPhone2=2792&idPhone3=4021)
* Nokia Series 40, since Platform Release 9 with 3G (UMTS, HSPA), like [Nokia C3-01](http://www.gsmarena.com/compare.php3?&idPhone1=3479&idPhone2=4546&idPhone3=5663)
* Asha Software Platform, like [Nokia Asha 501](http://www.gsmarena.com/compare.php3?&idPhone2=5795&idPhone3=5794&idPhone1=5792)
* (iOS) [Acrobits Groundwire](http://itunes.apple.com/app/groundwire-business-caliber/id378503081?mt=8)
* (Windows Phone) [Zoiper](http://www.windowsphone.com/s?appid=9cc16f11-b78b-437d-87ec-578fa1660737)

However instead, please, consider [Opus](http://github.com/traud/asterisk-opus), [AMR-WB](http://github.com/traud/asterisk-amr), or [AMR](http://github.com/traud/asterisk-amr).

## Thanks goes to
* Asterisk team: Thanks to their efforts and architecture the changes were done in one working day.
* [Rob Gagnon](http://issues.asterisk.org/jira/browse/ASTERISK-18094) provided the starting point with his patch.