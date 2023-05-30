require "rubygems"
require "tmpdir"
require "bundler/setup"
require "jekyll"

# Indicate name of your repo
GITHUB_REPONAME = "multiobjective-ml/multiobjective-ml.github.io"
TMP = "../multiobjective-ml.github.io/"

namespace :site do
  desc "Generating site files"
  task :generate do
    Jekyll::Site.new(Jekyll.configuration({
      "source"      => ".",
      "destination" => "_site"
    })).process
  end

  desc "Generation and publication of files on GitHub"
  task :publish => [:generate] do
      cp_r "_site/.", TMP
      pwd = Dir.pwd
      Dir.chdir TMP
      File.open(".nojekyll", "wb") { |f| f.puts("Locally generated site.") }

      system "git pull"
      system "git add ."
      message = "Site updated on #{Time.now.utc}"
      system "git commit -m #{message.inspect}"
      # system "git push -u origin master"
      system "git push"
      Dir.chdir pwd
  end
end