require 'json'
require 'logger'

namespace :rename do
  desc "Renames all preset files according to preset name"
  task :preset_name do
    logger = Logger.new STDOUT

    Dir.entries('presets').each do |file|
      file_path = 'presets/'+file
      unless File.directory?(file_path) || file_path =~ /json/
        preset_data = JSON.parse File.read(file_path), symbolize_names: true

        new_file_name = preset_data[:name]+'.json'
        if File.exists? 'presets/'+new_file_name
          logger.warn(file){'"%s" already exists. Leaving unchanged'%new_file_name}
        else
          File.rename file_path, 'presets/'+new_file_name
          logger.info(file){'Renamed to '+new_file_name}
        end
      end
    end
  end
end
