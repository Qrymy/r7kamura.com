require_relative 'lib/r7k/application'
require 'pathname'
require 'rack/capture'

desc 'Build static files.'
task :build do
  article_paths = R7k::Models::Article.all.map(&:canonical_path)
  static_file_paths = Pathname.glob('static/**/*').select(&:file?).map do |pathname|
    "/#{pathname.relative_path_from('static')}"
  end
  other_paths = %w[
    /
    /articles
    /feed.xml
    /sitemap.txt
  ]
  paths = other_paths + article_paths + static_file_paths

  paths.sort.each do |path|
    Rack::Capture.call(
      app: R7k::Application,
      url: "https://r7kamura.com#{path}",
    )
  end
end
