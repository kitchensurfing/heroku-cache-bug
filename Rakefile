# Add your own tasks in files placed in lib/tasks ending in .rake,
# for example lib/tasks/capistrano.rake, and they will automatically be available to Rake.

require File.expand_path('../config/application', __FILE__)

Rails.application.load_tasks

require 'sprockets/rails/task'
# clean the old tasks

Rake::Task["assets:environment"].clear
Rake::Task["assets:precompile"].clear
Rake::Task["assets:clean"].clear
Rake::Task["assets:clobber"].clear

class SprocketsRailsTask < Sprockets::Rails::Task
  def define
    super

    Rake::Task["assets:clean"].clear

    namespace :assets do
      desc "Remove old compiled assets"
      task :clean, [:keep] => :environment do |t, args|
        with_logger do
          manifest.clean(0)
        end
      end
    end
  end
end

SprocketsRailsTask.new(Rails.application)
