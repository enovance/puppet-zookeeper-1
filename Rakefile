require 'bundler'
Bundler.require(:rake)

require 'puppetlabs_spec_helper/rake_tasks'
require 'puppet-lint/tasks/puppet-lint'
require 'rspec-system/rake_task'

PuppetLint.configuration.ignore_paths = ["spec/fixtures/modules/cron/manifests/*.pp"]
PuppetLint.configuration.log_format = '%{path}:%{linenumber}:%{KIND}: %{message}'
PuppetLint.configuration.send("disable_80chars")

# use librarian-puppet to manage fixtures instead of .fixtures.yml
# offers more possibilities like explicit version management, forge downloads,...
task :librarian_spec_prep do
  sh "librarian-puppet install --path=spec/fixtures/modules/"
  pwd = `pwd`.strip
  unless File.directory?("#{pwd}/spec/fixtures/modules/zookeeper")
    sh "ln -s #{pwd} #{pwd}/spec/fixtures/modules/zookeeper"
  end
end
task :spec_prep => :librarian_spec_prep


task :default => [:spec, :lint]
