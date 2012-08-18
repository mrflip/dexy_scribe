require 'logger'
Log = Logger.new($stderr).tap{|log| log.level = Logger::WARN } unless defined?(Log)

require_relative './tasks/git_scribe.rake'

Settings.resolve!
Log.level   = Logger::DEBUG if Settings.verbose
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

task :initial do
  sh('git submodule update --init')
  sh('git submodule foreach git checkout master')
  sh('git submodule foreach git pull')
  sh('bundle update')
  cd 'dexy' do
    sh('pip install -e .')
  end
  sh('dexy setup')
end
