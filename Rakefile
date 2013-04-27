require 'bump/tasks'
require_relative 'lib/restpack-serializer/version'

task :default => :test
task :test => :spec

begin
  require "rspec/core/rake_task"

  desc "Run all specs"
  RSpec::Core::RakeTask.new(:spec) do |t|
    t.rspec_opts = ['-cfs']
  end
rescue LoadError
end

task :gem do
  Rake::Task["gem:bump"].invoke
  Rake::Task["gem:tag"].invoke
  Rake::Task["gem:build"].invoke
  Rake::Task["gem:push"].invoke
end

namespace :gem do
  task :build do
    sh "gem build restpack-serializer.gemspec"
  end

  task :push do
    require 'bump'
    sh "gem push restpack-serializer-#{Bump::Bump.current}.gem"
  end

  task :tag do
    require 'bump'
    version = Bump::Bump.current
    puts "tagging v#{version}"
    `git push && git tag v#{version} && git push --tags`
  end

  task :bump do
    Rake::Task["bump:patch"].invoke
  end
end
