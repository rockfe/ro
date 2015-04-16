var onlineConfig = require('./onlineConfig.js');

var C = onlineConfig;


module.exports = function(grunt) {
    // var transport = require('grunt-cmd-transport');
    // var style = transport.style.init(grunt);
    // var text = transport.text.init(grunt);
    // var script = transport.script.init(grunt);
    var getdir = function(filepath) {
        var sp = filepath.split('/');
        var filename = sp[sp.length - 1];
        return filepath.replace(filename,'');
    }

    
    
    
    grunt.initConfig({
        pkg: grunt.file.readJSON("package.json"),
        less: { // Set up to detect files dynamically versus statically
            css1: {
                options: {
                    cleancss: true
                },
                expand: true, // set to true to enable options following options:
                cwd: C.base, // all sources relative to this path
                src: C.less, // source folder patterns to match, relative to cwd
                dest: "dest/", // destination folder path prefix
                ext: ".css", // replace any existing extension with this value in dest folder
                flatten: false // flatten folder structure to single level
            }
        },
        uglify: {
            js1: {
                files: [{
                    expand: true,
                    cwd: C.base,
                    src: C.js,
                    dest: 'dest'
                }]
            }
        },
        copy: {
            css1: {
                files: [{
                    expand: true,
                    cwd: C.base,
                    src: C.copycss,
                    dest: 'dest'
                }]
            }
        },
        imagemin: { // Task
            img1: { // Another target
                files: [{
                    expand: true, // Enable dynamic expansion
                    cwd: C.base, // Src matches are relative to this path
                    src: C.img, // Actual patterns to match
                    dest: 'dest', // Destination path prefix
                    filter: function(filepath) {
                        if('src/tem/' == getdir(filepath)){
                            return false
                        }else{
                            return true
                        }
                        // console.log()
                        // return (grunt.file.isDir(filepath) && require('fs').readdirSync(filepath).length === 0);
                    },
                }]
            }
        }
    }); 

    grunt.loadNpmTasks('grunt-contrib-less');
    grunt.loadNpmTasks('grunt-contrib-copy');
    grunt.loadNpmTasks('grunt-contrib-imagemin');
    grunt.loadNpmTasks('grunt-contrib-uglify');


    // process: ["less", "copy", "imagemin", "uglify"]
    var process = [];
    if(C.less){
        process.push('less');
    }
    if(C.copycss){
        process.push('copy');
    }
    if(C.img){
        process.push('imagemin')
    }
    if(C.js){
        process.push('uglify');
    }
    // grunt.registerTask('default', ['clean', "uglify:seamodules"]);
    
    grunt.registerTask('default', process);
    
};
