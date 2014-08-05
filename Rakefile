require "foodcritic"
require "rspec/core/rake_task"
require "rubocop/rake_task"

desc "Run RuboCop style and lint checks"
RuboCop::RakeTask.new(:rubocop) do |t|
  t.options = ["-D"]
end

desc "Run Foodcritic lint checks"
FoodCritic::Rake::LintTask.new(:lint) do |t|
  t.options = { :fail_tags => ["correctness"] }
end

desc "Run ChefSpec examples"
RSpec::Core::RakeTask.new(:spec) do |t|
  t.rspec_opts = %w(-f JUnit -o results.xml)
end

desc "Run all tests"
task :test => [:lint, :spec]
task :default => :test

begin
  require "kitchen/rake_tasks"
  Kitchen::RakeTasks.new

  desc "Alias for kitchen:all"
  task :integration => "kitchen:all"

  task :test => :integration
rescue LoadError
  puts ">>>>> Kitchen gem not loaded, omitting tasks" unless ENV['CI']
end
