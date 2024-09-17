source "https://rubygems.org"
# Run Jekyll with 'bundle exec jekyll serve'
# gem "jekyll", "~> 4.3.3"

# Theme
gem "minimal-mistakes-jekyll"

# GitHub Pages, to upgrade, run `bundle update github-pages`.
gem "github-pages", "~> 232", group: :jekyll_plugins

# Plugins
group :jekyll_plugins do

end

# Windows and JRuby does not include zoneinfo files, so bundle the tzinfo-data gem
# and associated library.
platforms :mingw, :x64_mingw, :mswin, :jruby do
  gem "tzinfo", ">= 1", "< 3"
  gem "tzinfo-data"
end

# Lock `http_parser.rb` gem to `v0.6.x` on JRuby builds since newer versions of the gem
# do not have a Java counterpart.
gem "http_parser.rb", "~> 0.6.0", :platforms => [:jruby]
