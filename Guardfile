# -*- ruby -*-

ignore /^(?:output|output-long|output-scribe|artifacts|logs)/

notification :off
# interactor :off

require 'guard/notifiers/emacs'
::Guard::Notifier::DEFAULTS.merge!(
  :success => '#e7fde4',
  :failed  => '#faeedc',
  :default => '#eee8d6',
)

# Add files and commands to this file, like the example:
#   watch(%r{file/path}) { `command(s)` }
#
guard 'shell' do
  book_dir = "big_data_for_chimps"
  ENV['BOOK_CONTENTS'] = File.expand_path(book_dir)
  watch(/#{book_dir}\/([^\/]+).asciidoc/) do |match|
    p [match]
    system 'dexy', '--loglevel', 'DEBUG', '--directory', book_dir, '--run', match[0]and
      system 'rake', '--trace', 'gen:html', '--rules', '--', "--book_file=output/#{match[0]}"
  end
end

guard 'livereload' do
  watch(/(.*).asciidoc/){|match| [ "#{match[1]}.html", "working.html"] }
end
