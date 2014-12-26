#!/usr/bin/env node

/**
 Fixes file system permissions for all files in a directory (recursively). All folders get 0755 mask and files 0664 mask
*/

var fs = require('fs')

var dir = process.argv[2]

fs.stat(dir, function (err, stats) {
	if (err) {
		console.error(err)
	} else {
		if (!stats.isDirectory()) {
			console.error(dir + ' is not a directory')
		} else {
			traverseDirectory(dir)
		}
	}
})

function traverseDirectory (dir) {
	fs.readdir(dir, function (err, files) {
		if (err) {
			console.error(err)
		} else {
			files.forEach(function (element, index, array) {
				fs.stat(dir + '/' + element, function (err, stats) {
					if (err) {
						console.error(err)
					} else {
						if (stats.isDirectory()) {
							fs.chmod(dir + '/' + element, 0755, function (err) {
								if (err) {
									console.error('Failed to fix permissions for directory: ' + dir + '/' + element + ', error: ' + err)
								}
							})
							traverseDirectory(dir + '/' + element) // recurse here
						} else {
							fs.chmod(dir + '/' + element, 0644, function (err) {
								if (err) {
									console.error('Failed to fix permissions for file: ' + dir + '/' + element + ', error: ' + err)
								}
							})
						}
					}
				})
			})
		}
	})
}