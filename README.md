# nodebox-example

nodebox-example is "Hello World" for Node.js, but it's sandboxed in a VirtualBox VM. Experiment with Node, blow it up, start over. Configure a development VM with code reloading and Node listening right on port 80, or configure a production-ish VM with nginx proxying to a daemonized Node process.

## Dependencies

Nodebox uses <a href="http://www.vagrantup.com">Vagrant</a> to create <a href="http://www.virtualbox.org">VirtualBox</a> virtual machines that are then provisioned with <a href="http://www.opscode.com/chef/">Chef</a> (solo). Your host machine needs to be set up for Ruby and RubyGems, and you need to <a href="http://www.virtualbox.org/wiki/Downloads">download VirtualBox 4.0.x</a>. The <a href="http://vagrantup.com/docs/getting-started/index.html">Vagrant getting started guide</a> has more information on Vagrant's dependencies.

Install vagrant:
    $ gem install vagrant

Download an 32-bit Ubuntu Lucid base box:
    $ vagrant box add ubuntu-lucid-32 http://files.vagrantup.com/lucid32.box

TODO: Instructions for using other distributions

## Getting Started with Nodebox

    $ git clone git@github.com:repeatingbeats/nodebox-example.git
    $ cd nodebox-example/nodebox
    $ vagrant up
    
    ... make your coffee ...

    $ curl http://localhost:8000

## Development Nodebox

TODO

## Production-ish Nodebox

TODO

## Acknowledgements

