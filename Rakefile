# Change your GitHub reponame
GITHUB_REPONAME = "jdanielnd/foresee-docs"

require "jekyll"
require 'rubygems'
require 'rake'
require 'rdoc'
require 'date'
require 'yaml'


desc "Generate blog files"
task :generate do
  Jekyll::Site.new(Jekyll.configuration({
    "source"      => ".",
    "destination" => "_site"
  })).process
end


desc "Generate and publish blog to gh-pages"
task :publish => [:generate] do
  tmpdir = '/tmp/' + rand(36**8).to_s(36)
  Dir.mkdir(tmpdir) do |tmp|
    cp_r "_site/.", tmp
    Dir.chdir tmp
    system "git init"
    system "git add ."
    message = "Site updated at #{Time.now.utc}"
    system "git commit -m #{message.shellescape}"
    system "git remote add origin git@github.com:#{GITHUB_REPONAME}.git"
    system "git push origin master --force"
  end
end