# Rostopic

## Supported Commands
* `rostopic bw`     display bandwidth used by topic
* `rostopic delay`  display delay for topic which has header
* `rostopic echo`   print messages to screen
* `rostopic find`   find topics by type
* `rostopic hz`     display publishing rate of topic
* `rostopic info`   print information about active topic
* `rostopic list`   print information about active topics
* `rostopic pub`    publish data to topic
* `rostopic type`   print topic type

## echo
* `--offset` display time in messages as offset from current time
* `--filter` display messages that match a specified python expression
    - `rostopic echo --filter "m.data == 'foo'" /topic_name`
    - `m` is the message object
* `-c` clear the screen after each message is published, cannot be used with `-p`
* `-b` display messages in a bag file
* `-p` display messages in a matlab/octave-friendly plotting format, cannot be used with `-c`
* `-n <count>` echo count number of messages and exit
* `echo <topic-name/field>` display specific fields in a message
