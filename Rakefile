task :default => [:server]

coffee_path = File.dirname(__FILE__) + "/app/assets/javascripts"
scss_path = File.dirname(__FILE__) + "/app/assets/stylesheets"

coffee_files = FileList[coffee_path + '/*.coffee']
scss_files = FileList[scss_path + '/*.scss']

desc "Compile assets"
task :compile => [:compile_coffee, :compile_scss]

desc "Compile coffeescripts"
task :compile_coffee do
  coffee_files.each do |file|
    sh "coffee -c #{file}"
  end
end

desc "Compile scss"
task :compile_scss do
  scss_files.each do |file|
    sh "scss #{file} #{file.ext('css')}"
  end
end

desc "Cleanup css and js"
task :cleanup do
  coffee_files.each do |file|
    sh "rm #{file.ext('js')}" if File.exist? file.ext('js')
  end
  scss_files.each do |file|
    sh "rm #{file.ext('css')}" if File.exist? file.ext('css')
  end
end

desc "run server"
task :server do
  puts "Cleaning generated assets!"
  Rake::Task["cleanup"].invoke
  puts "DONE!\n"
  puts "\nRunning development server: to stop press CTRL-C!"
  sh "rackup config.ru"
  puts "\nGenerating assets!"
  Rake::Task["compile"].invoke
  puts "DONE!\n"
end
