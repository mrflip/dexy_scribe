require 'logger'
require 'configliere' ; Settings.use :commandline
require 'gorillib/model'
Log = Logger.new($stderr).tap{|log| log.level = Logger::DEBUG } unless defined?(Log)

load 'tasks/git_scribe.rake'

Settings.book_file = File.expand_path(
  'output/big_data_for_chimps/ba06-semi_structured_data-d-airline_flights.asciidoc',
  File.dirname(__FILE__))
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

task :init do
  sh('git submodule update --init')
  sh('git submodule foreach git checkout master')
  sh('git submodule foreach git pull')
  sh('bundle update')
  cd 'dexy' do
    sh('pip install -e .')
  end
  sh('dexy setup')
end

# --------------------------------------------------------------------------
#
# Rake Task definitions for book
#

HtmlTask.new.tasks
PdfTask.new.tasks
DocbookTask.new.tasks
EpubTask.new.tasks
# MobiTask.new.tasks
