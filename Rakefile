require 'fileutils'

namespace :book do
  # 文件名
  file = "slf4j-docs"

  # 删除存着的文件
  def delete_file(file)
    if File.exist? file
      puts "Delete: #{file}"
      if File.file? file
        File.delete file
      else # TODO 如何删除不空文件夹？
        FileUtils.rm_r file
      end
    end
  end

  desc 'Clear build result'
  task :clear do
    delete_file "images"
    delete_file "#{file}.html"
    delete_file "#{file}.pdf"
    delete_file "#{file}.epub"
    delete_file "#{file}.mobi"

    puts "Clear ok"
  end

  desc 'prepare build'
  task :prebuild => :clear do
    print "Start to copy images...\n"
    Dir.mkdir 'images' unless Dir.exists? 'images'
    Dir.glob("docs/images/*").each do |image|
      FileUtils.copy(image, "images/" + File.basename(image))
    end
    print "Finish copying images.\n\n"
  end

  desc 'build basic book formats'
  task :build => :prebuild do
    puts "Converting to HTML..."
    `asciidoctor #{file}.adoc`
    puts " -- HTML output at #{file}.html"

    #puts "Converting to HTML..."
    #`bundle exec asciidoctor -r ./config.rb #{file}.adoc`
    #puts " -- HTML output at #{file}.html"

    #puts "Converting to EPub..."
    #`bundle exec asciidoctor-epub3 -r ./config.rb #{file}.adoc`
    #puts " -- Epub output at #{file}.epub"

    #puts "Converting to Mobi (kf8)..."
    #`bundle exec asciidoctor-epub3 -r ./config.rb -a ebook-format=kf8 #{file}.adoc`
    #puts " -- Mobi output at #{file}.mobi"

    #puts "Converting to PDF... (this one takes a while)"
    #`bundle exec asciidoctor-pdf -r ./config.rb -a pdf-style=KaiGenGothicCN #{file}.adoc`
    #puts " -- PDF  output at #{file}.pdf"
  end
end

task :default => "book:build"
