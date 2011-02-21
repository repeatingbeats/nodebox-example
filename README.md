# nodebox-example

nodebox-example is "Hello World" for Node.js, but it's sandboxed in a VirtualBox VM. Experiment with Node, blow it up, start over. Configure a development VM with code reloading and Node listening right on port 80, or configure a production-ish VM with nginx proxying to a daemonized Node process.

## Dependencies

NodeBox uses <a href="http://www.vagrantup.com">Vagrant</a> to create <a href="http://www.virtualbox.org">VirtualBox</a> virtual machines that are then provisioned with <a href="http://www.opscode.com/chef/">Chef</a> (solo). Your host machine needs to be set up for Ruby and RubyGems, and you need to <a href="http://www.virtualbox.org/wiki/Downloads">download VirtualBox 4.0.x</a>. The <a href="http://vagrantup.com/docs/getting-started/index.html">Vagrant getting started guide</a> has more information on Vagrant's dependencies.

Install vagrant:
    $ gem install vagrant

Download an 32-bit Ubuntu Lucid base box:
    $ vagrant box add ubuntu-lucid-32 http://files.vagrantup.com/lucid32.box

TODO: Instructions for using other distributions

## Production-ish NodeBox

    $ git clone git://github.com/repeatingbeats/nodebox-example.git --recursive
    $ cd nodebox-example/nodebox
    $ vagrant up

    ... make your coffee ...

    $ curl http://localhost:8000

## Development NodeBox

    $ git clone git://github.com/repeatingbeats/nodebox-example.git --recursive
    $ cd nodebox-example

Then, edit the environment and app_port in nodebox.json

    {
      ...
      "environment": "development",
      "app_port": 80,
      ...
    }

After configuring the VM, SSH into the VM and start the app with the supervisor module. This allows you to see errors and console output in your shell. Supervisor reloads code on changes.
    $ cd nodebox
    $ vagrant up

    ... make your coffee ...

    $ vagrant ssh

On the VM:
    $ cd /var/www/nodebox-example
    $ sudo supervisor -p app.js -w app.js

Sudo is required so Node can listen on port 80. Do this in the saftey of your own VM! There's a reason this is called the development NodeBox. (For extra caveats, note that even the production-ish box is caveated with an 'ish')

On the host machine:
    $ curl http://localhost:8000

Now, change something in app.js. Supervisor reloads the code, so you can view your changes right away with another curl on the host.

## Acknowledgements

TODO
