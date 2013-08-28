require 'rake/testtask'

task :default => :test

Rake::TestTask.new do |t|
  t.libs << "test"
  t.test_files = FileList['test/*_test.rb']
  t.verbose = true
end

desc "Remove temporary files"
task :clean do
  %x{rm -rf *.gem doc pkg coverage}
  %x{rm -f `find . -name '*.rbc'`}
end

desc "Build the gem"
task :gem do
  %x{gem build friendly_id-globalize.gemspec}
end