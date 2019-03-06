require 'erb'

desc "Generate all the HTML files"
task :generate do
  Dir["*/side.txt"].each do |side_file_path|
    side_content = File.read(side_file_path)
    containing_folder = File.expand_path("..", side_file_path)
    @city = File.basename(containing_folder).gsub("-", " ").split.map(&:capitalize).join(' ')
    puts "Generating #{@city}"

    url = "https://www.mapquestapi.com/staticmap/v4/getplacemap?"
    url += "key=#{ENV['MAPQUEST_CONSUMER_KEY']}"
    url += "&location=#{@city}"
    url += "&size=1200,600"
    url += "&type=map&zoom=12&imagetype=jpg&scalebar=false"

    @maps_url = url
    @side = "West"

    renderer = ERB.new(File.read("template.html.erb"))
    output_path = File.join(containing_folder, "index.html")
    File.write(output_path, renderer.result(binding))
  end
end
