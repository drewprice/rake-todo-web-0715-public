task :hello_rake do
  puts 'Hello, from rake'
end

task :default do
  puts 'Hello, from default task!'
end

task :environment do
  require_relative 'config/environment'
end

task upcoming_todos: [:environment] do
  User.with_upcoming_todos.each { |u| puts "Emailing #{u}" }
end

task overdue_todos: [:environment] do
  User.with_overdue_todos.each { |u| puts "Emailing #{u}" }
end

namespace :todos do
  task mark_overdue: [:environment] do
    Todo.mark_overdue
  end

  task mark_upcoming: [:environment] do
    Todo.mark_upcoming
  end
end

desc "Loads an interactive console."
task console: [:environment] do
  load 'bin/config'
  exit
end

namespace :user do
  desc 'Send a summary to a User'
  task :send_summary, [:email] => [:environment] do |_, args|
    puts "Sending summary to user with #{args[:email]}"
  end

  desc 'Does some reminding stuff'
  task todo_reminder: [:environment] do
    my_ruby_home = ENV['MY_RUBY_HOME']

    puts "ENV includes #{my_ruby_home}"
    puts "Sending todo reminder to #{ENV['EMAIL']}"
  end
end
