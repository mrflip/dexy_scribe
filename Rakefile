require 'logger'
require 'configliere' ; Settings.use :commandline
require 'gorillib/model'
Log = Logger.new($stderr).tap{|log| log.level = Logger::DEBUG } unless defined?(Log)
ENV['BOOK_CONTENTS'] = File.expand_path('big_data_for_chimps')

load 'tasks/git_scribe.rake'
Settings.resolve!

#
# Top-level rake tasks
#

# run if no task specified
task :default => :book

# dummy task to force generation
task :force

desc "Generate all documents"
task :gen

desc "Remove generated artifacts for all file types"
task :clean

namespace :book do
  desc "Merge book files with code and its output"
  task :dexy do
    sh 'dexy', '--loglevel', 'DEBUG', '--directory', 'big_data_for_chimps'
  end
end
task :book => ['book:dexy', 'gen:html']

namespace :init do
  desc "Install and initialize dexy"
  task :dexy do
    cd('vendor/dexy'){ sh('pip install -e .') }
    sh('dexy setup')
  end
end
desc "Installs prerequisites for book"
task :init => ['init:dexy']

# --------------------------------------------------------------------------
#
# Rake Task definitions for book
#

HtmlTask.new.tasks
PdfTask.new.tasks
DocbookTask.new.tasks
EpubTask.new.tasks
# MobiTask.new.tasks
