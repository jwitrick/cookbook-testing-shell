# Encoding: UTF-8

require 'rubygems'
require 'English'
require 'bundler/setup'
require 'rubocop/rake_task'
require 'cane/rake_task'
require 'rspec/core/rake_task'
require 'foodcritic'
require 'stove/rake_task'

Cane::RakeTask.new

RuboCop::RakeTask.new

desc 'Display LOC stats'
task :loc do
  puts "\n## LOC Stats"
  Kernel.system 'countloc -r .'
end

desc 'Run knife cookbook syntax test'
task :cookbook_test do
  path = File.expand_path('../..', __FILE__)
  cb = File.basename(File.expand_path('..', __FILE__))
  Kernel.system "knife cookbook test -c test/knife.rb -o #{path} #{cb}"
  $CHILD_STATUS == 0 || fail('Cookbook syntax check failed!')
end

FoodCritic::Rake::LintTask.new do |f|
  f.options = { fail_tags: %w(any) }
end

RSpec::Core::RakeTask.new(:spec)


Stove::RakeTask.new

task default: %w(cane rubocop loc cookbook_test foodcritic spec)
