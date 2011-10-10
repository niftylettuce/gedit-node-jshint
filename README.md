**Note:** Please see [gedit-icing](http://github.com/niftylettuce/gedit-icing) for more gedit plugins.

# gedit-node-jshint

 Simply use CTRL+J in gedit to to run JSHint using [node-jshint](https://github.com/jshint/node-jshint).

 **Note**: This only works if you're working inside of a git project (since we use `git rev-parse --show-toplevel`).

## Getting started

 1. Install `node-jshint`
 (**Note:** this requires [node](https://github.com/joyent/node) and
 [npm](https://github.com/isaacs/npm), here are [quick instructions](https://gist.github.com/579814) to install these requirements):

          npm install -g jshint

 2. Enable the External Tools plugin:

    ![Enable the External Tools plugin](http://i.imgur.com/HuOOy.png)

 3. Add a new entry called `gedit-node-jshint` under `Tools -> Manage External Tools`:

        #!/bin/sh
        dirpath=`git rev-parse --show-toplevel`
        reporter="$dirpath/jshint/reporter.js"
        config="$dirpath/jshint/config.json"
        if [ -d "$HOME/bin" ] ; then
            PATH="$HOME/bin:$PATH"
        fi
        export PATH=$HOME/local/node/bin:$PATH
        cat $1 >> /tmp/jshint.js
        jshint /tmp/jshint.js --reporter $reporter --config $config > /dev/stdout
        rm /tmp/jshint.js

 4. Set External Tool Options as follows:

    ![Set External Tool Options as follows](http://i.imgur.com/El101.png)

 5. Create a `jshint` directory in your project and download `config.json` and `reporter.js` from the `node-jshint` repo.

        cd /path/to/mygitproject
        mkdir jshint && cd jshint
        wget https://raw.github.com/jshint/node-jshint/master/example/config.json
        wget https://raw.github.com/jshint/node-jshint/master/example/reporter.js

 6. Open your JavaScript file in gedit, then use the hotkey `CTRL+J` to run JSHint (see Shell Output tab for its output).

 7. You can also select specific parts of a JavaScript file and use the hotkey.

 8. Configure the `config.json` and `reporter.js` files based on your project's needs.
 See [jshint](https://github.com/jshint/jshint) or [node-jshint](https://github.com/jshint/node-jshint) to learn more.
