def jekyll(opts="", path="")
  sh "rm -rf _site"
  sh path + "jekyll " + opts
end
desc "Build site using Jekyll"
task :build do
  jekyll('build')
end
desc "Serve on Localhost with port 4000"
task :default do
  jekyll "serve --watch --drafts"
end
desc "Serve on Localhost with port 4000 using development version"
task :unstable do
  jekyll "serve --auto", "../jekyll/bin/"
end
desc "Deploy to Dev"
task :deploy => :"deploy:dev"
namespace :deploy do
  desc "Deploy to Dev"
  task :dev => :default do
  end

  desc "Deploy to Live"
  task :live => :build do
    rsync "poison.tips"
  end
  desc "Deploy to all sites"
  task :all => [:live]
  def rsync(domain)

    sh "rsync -e '/usr/bin/ssh'  --bwlimit=2000 --archive --delete --verbose --compress _site/ mrpoison@#{domain}:poison.tips"
  end
end
