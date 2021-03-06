# frozen_string_literal: true

# This file contains tasks with no namespace.
# All namespaced tasks are defined in the '../rakelib' directory.
# Each namespace is defined in a separate file.
# For example, 'preview:all' is defined in the '../rakelib/preview.rake' file.
# To see the list of tasks to use, run 'rake -T'.

require 'html-proofer'
require 'kramdown'
require 'launchy'
require 'colorator'

# Load ruby files with helper methods from the 'rakelib/' directory
require_relative 'rakelib/link-checker.rb'
require_relative 'rakelib/converter.rb'
require_relative 'rakelib/double-slash-check.rb'

desc "Same as 'rake', 'rake preview'"
task default: %w[preview]

desc "Same as 'test:report'"
task test: %w[test:report]

desc 'Preview the devdocs locally'
task preview: %w[install clean] do
  puts 'Generating devdocs locally ... '.magenta
  if File.exist?('_config.local.yml')
    print 'enabled the additional configuration parameters from _config.local.yml: $ '.magenta
    sh 'bundle exec jekyll serve --incremental --open-url --livereload --trace --config _config.yml,_config.local.yml'
  else
    Rake::Task['preview:all'].invoke
  end
end

task :clean do
  print 'Cleaning after the last site generation: $ '.magenta
  sh 'bundle exec jekyll clean'
  puts 'Clean!'.green
end

task :install do
  print 'Install gems listed in the Gemfile: $ '.magenta
  sh 'bundle install'
  puts 'Installed!'.green
end

desc 'Build the entire website'
task build: %w[clean] do
  print 'Building the site with Jekyll: $ '.magenta
  sh 'bundle exec jekyll build --verbose --trace'
  puts 'Built!'.green
end
