require 'logger'
require 'configliere' ; Settings.use :commandline
require 'gorillib/model'
Log = Logger.new($stderr).tap{|log| log.level = Logger::DEBUG } unless defined?(Log)
ENV['BOOK_CONTENTS'] = File.expand_path('big_data_for_chimps')

load 'tasks/git_scribe.rake'

# Settings.book_file = 'big_data_for_chimps/ba06-semi_structured_data-d-airline_flights.asciidoc'

Settings.resolve!
Log.debug{ "configuration: #{Settings.inspect}" }

#
# Top-level rake tasks
#

# dummy task to force generation
task :force

desc "Generate all documents"
task :gen

desc "Remove generated artifacts for all file types"
task :clean

task :default => 'gen:html'

namespace :book do
  desc "Merge book files with code and its output"
  task :dexy do
    sh 'dexy', '--loglevel', 'DEBUG', '--directory', 'big_data_for_chimps'  # , '--run', Settings.dexy_file
  end
end


namespace :init do
  desc "Retrieve submodules"
  task :submodules do
    sh('git submodule update --init')
    sh('git submodule foreach git checkout master')
  end
  desc "Update ruby dependencies"
  task :bundle do
    sh('bundle update')
  end
  desc "Install and initialize dexy"
  task :dexy do
    cd('vendor/dexy'){ sh('pip install -e .') }
    sh('dexy setup')
  end
end
desc "Installs prerequisites for book"
task :init => ['init:submodules', 'init:bundle', 'init:dexy']

# --------------------------------------------------------------------------
#
# Rake Task definitions for book
#

HtmlTask.new.tasks
PdfTask.new.tasks
DocbookTask.new.tasks
EpubTask.new.tasks
# MobiTask.new.tasks
