# -*- ruby -*-

require 'pry'

ignore  %r{(?:\.git|data|images)/}
ignore %r{^(?:output|output-long|output-scribe|artifacts|logs|vendor)}

notification :off
interactor :off

require 'guard/notifiers/emacs'
::Guard::Notifier::DEFAULTS.merge!(
  :success => '#e7fde4',
  :failed  => '#faeedc',
  :default => '#eee8d6',
  )

book_dir = "big_data_for_chimps"

# Add files and commands to this file, like the example:
#   watch(%r{file/path}) { `command(s)` }
#
guard 'shell' do
  # ENV['BOOK_CONTENTS'] = File.expand_path(book_dir)
  # watch(/#{book_dir}\/([^\/]+)\.asciidoc/) do |match|
  #   system 'rake', 'book:code:airline_flights'
  #   system 'rake', 'book:dexy', '--', "--dexy_file=match[0]" and
  #     system 'rake', '--trace', 'gen:html', '--', "--book_file=output/#{match[0]}"
  # end

  watch(/#{book_dir}\/code\/.+\.rake/){|match|
    # binding.pry
    system 'rake', '-f', match[0], '--trace' }

  watch(%r{#{book_dir}/code/.+\.rb\z}) do |match|
    rakefile = File.join(File.dirname(match[0]), 'tasks.rake')
    system 'rake', '-f', rakefile, '--trace' if File.exist?(rakefile)
  end
end

guard 'livereload' do
  watch(/(.*).asciidoc/){|match| [ "#{match[1]}.html", "working.html"] }
end
