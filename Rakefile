require 'tempfile'

task :build do
  sh "bundle exec jekyll build"
end

task :release => :build do
  sh "git checkout gh-pages"
  Dir.mktmpdir do |dir|
    sh "cp -r _site #{dir}"
    sh "rm -rf ./*"
    sh "cp -r #{dir}/* ./"
  end
  sh "git add . --all && if ! git diff --staged --exit-code ; then git commit -am 'Update doc' && git push origin gh-pages ; fi"
  sh "git checkout master"
end

task default: :build
