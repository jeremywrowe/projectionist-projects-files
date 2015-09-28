require "csv"
require "pathname"

namespace :generate do
  desc "Generate the projections csv file"
  task :csv do
    download_dir = "downloads"
    index_file   = File.join download_dir, "index.csv"
    header       = %w( project updated location )

    mkdir_p download_dir
    files        = Dir[File.join(download_dir, "*.projections.json").to_s]

    CSV.open(index_file, "w") do |csv|
      csv << header
      files.each do |file|
        project  = Pathname.new(file).basename(".projections.json").to_s
        updated  = File.mtime(file).to_i
        location = "/#{file}"
        csv << [project, updated, location]
      end
    end
  end
end

task default: "generate:csv"
