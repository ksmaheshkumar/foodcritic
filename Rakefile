require 'rubygems'
require 'bundler'
require 'rake/testtask'
require 'cucumber'
require 'cucumber/rake/task'

task :default => [:install, :test, :features]

Bundler.setup
Bundler::GemHelper.install_tasks

Rake::TestTask.new do |t|
  t.pattern = 'spec/foodcritic/*_spec.rb'
end

Rake::TestTask.new do |t|
  t.name = 'regressions'
  t.pattern = 'spec/regression/*_spec.rb'
end

Cucumber::Rake::Task.new(:features) do |t|
  t.cucumber_opts = ['-f', 'progress', '--strict']
  unless ENV.has_key?('FC_FORK_PROCESS') and ENV['FC_FORK_PROCESS'] == true.to_s
    t.cucumber_opts += ['-t', '~@build']
    t.cucumber_opts += ['-t', '~@context']
  end
  t.cucumber_opts += ['features']
end
