source 'https://rubygems.org'
require 'json'
require 'open-uri'
gem 'jekyll', '~>3.1'
versions = JSON.parse(open('https://pages.github.com/versions.json').read)
gem 'github-pages', versions['github-pages']
