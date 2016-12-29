# Grunt Config for Static Code Analysis

The intend of this repository is to test using a distrubuted grunt-configuration to set up
generic code analysis for a number of project that tend to share languages and owners, but
not purpose.

I'm using this repository together with some hobby-work to create a proof-of-concept that
should need to work within a much more complex environment, both due to the amount of
developers involved as well as the project-structures.

## How to use

```
> npm i load-grunt-configs grunt-config-windgazer-sca -D
> vi Gruntfile.js
> grunt sca:all
```

Make sure you add load-grunt-configs to your Gruntfile, like so:

```javascript
// Gruntfile.js
module.exports = function (grunt) {
    grunt.loadNpmTasks('grunt-contrib-jshint');

    //loads the various task configuration files
    var configs = require('load-grunt-configs')(grunt);
    grunt.initConfig(configs);

    grunt.registerTask('default', ['sca:all']);
}
```

## Generic design thoughts

### Goals

- distributed. Should be able to `npm install` and then run `grunt sca`.
- configurable. Especcially target locations might need tweaking.
- sane defaults. Should incorporate as much 'out-of-the-box' configration as is sane.

### Ideas

I intend to rig up using [load-grunt-configs][e1], this should allow me to easily tackle
most of the requirements for 'distribution'. This particular module will allow me to
create split config-files, even having sub-tasks split across several configurations. On
top of that, it has support for incorporating config-files from `node-modules/**`.

I hope to add [load-grunt-configs][e1] as a peer-dependency and subsequently add the
various static code checkers, as well as their configuration-settings, to this repository.

Challenges I need to solve:
- Will 'devdependencies' be installed on the main project.
- Documentation on using node-modules for distributed config-files is weak.


[e1]: https://github.com/creynders/load-grunt-configs
