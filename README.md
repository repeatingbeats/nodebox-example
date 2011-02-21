# nodebox-example

nodebox-example is "Hello World" for Node.js, but it's sandboxed in a VirtualBox VM. Experiment with Node, blow it up, start over. Configure a development VM with code reloading and Node listening right on port 80, or configure a production-ish VM with nginx proxying to a daemonized Node process.

## Dependencies

NodeBox uses [Vagrant](http://www.vagrantup.com") to create [VirtualBox](http://www.virtualbox.org) virtual machines that are then provisioned with [Chef](http://www.opscode.com/chef) (solo). Your host machine needs to be set up for Ruby and RubyGems, and you need to [download VirtualBox 4.0.x](http://www.virtualbox.org/wiki/Downloads). The [Vagrant getting started guide](http://vagrantup.com/docs/getting-started/index.html) has more information on Vagrant's dependencies.

Install vagrant:
    $ gem install vagrant

Download an 32-bit Ubuntu Lucid base box:
    $ vagrant box add ubuntu-lucid-32 http://files.vagrantup.com/lucid32.box

If you have a different Vagrant base box you want to use (i.e. _not_ ubuntu-lucid-32), you'll need to edit vgr_config.vm.box in the Vagrantfile accordingly.

## nodebox.json

NodeBox is configured using the required nodebox.json file in the application's root directory. Current options (no promises that they will remain stable any time in the near future):

    app_name: your application's name. this affects various directory names on
              the VM (e.g. the app directory is /var/www/app_name/)

    environment: "development" or "production". see below for details.

    app_port: Node listens on this port on the VM. Should be 80 for "development"

    host_port: Vagrant forwards this port on the host to port 80 on the VM.
               Point your host browser at localhost:host_port to see the app.

    modules: An array of modules that will be installed on the VM by npm.

    node_version: Self explanatory. No guarantee that all node versions will work.

    npm_version: Self explanatory. No guarantee that all node versions will work.

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

NodeBox uses Chef cookbooks by [opscode](https://github.com/opscode/cookbooks) and [mdxp](https://github.com/mdxp/cookbooks). Using Monit and Upstart was [not my idea](http://howtonode.org/deploying-node-upstart-monit).

