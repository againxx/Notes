# Logging

## change logger levels
### command line
`rosservice call /<node-name>/set_logger_level ros.<package-name> <level>`

* level: `DEBUG`, ..., `FATAL`
* cannot use it until after the node is started
