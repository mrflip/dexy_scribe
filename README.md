
Scripts for compiling an asciidoc book with dexy




* final -- artifacts as rendered into html, pdf, etc



* dexy for going from raw (`big_data_for_chimps`) to compiled (`output`)
* rake (git-scribe) for going from `dexy`d to `final`


## Setup

Please use 

* Ruby 1.9.2+ -- I recommend using [ruby-build with rbenv](https://github.com/sstephenson/ruby-build).
* Python 2.6 or 2.7 (not 3.0), with `pip`

Run these commands:

```bash
cd dexy_scribe
gem install bundler
bundle update
rake init
```    
    