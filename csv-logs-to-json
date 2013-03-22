#! /usr/bin/env node

(function () {
    'use strict';

    var CSV_HEADERS = [
            'remote_addr',
            'remote_user',
            'time_local',
            'request',
            'status',
            'body_bytes_sent',
            'http_referer',
            'http_user_agent'
        ];

    var fs = require('fs'),
        _ = require('underscore'),
        csvParse = require('csv');

    var logFilePath = process.argv[2],
        jsonFilePath = process.argv[3];

    if (!fs.existsSync(logFilePath)) {
        fatalError('No log file given');
    }

    if (!jsonFilePath) {
        jsonFilePath = 'logs.json';
    }

    if (fs.existsSync(jsonFilePath)) {
        fs.renameSync(jsonFilePath, jsonFilePath + '.old');
    }

    try {
        var output = fs.createWriteStream(jsonFilePath);
    } catch (error) {
        fatalError(error);
    }

    output.write('[');

    csv().from.stream(fs.createReadStream(logFilePath))
        .transform(function (row) {
            // console.log();
            return _(row).reduce(function (memo, value, index) {
                memo[CSV_HEADERS[index]] = value;
                // console.log("value:", value);
                return memo;
            }, {});
        })
        .on('record', function (row) {
            output.write(JSON.stringify(row));
        })
        .on('end', function () {
            output.write(']');
        })
        .on('error', fatalError);


    function fatalError(message) {
        console.error(message);
        process.exit(1);
    }
}())
