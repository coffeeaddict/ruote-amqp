
# ruote-amqp

ruote-amqp is a set of classes that let a ruote engine publish and/or receive messages over AMQP.

The most common use case is publishing workitems for processing by AMQP consumers and eventually receiving them back to resume the flow.

Another use case would be to listen on an AMQP queue for workflow launch requests.

Listening for arbitrary AMQP messages before resuming a flow (ambush/alert) is also possible.


## usage

### Ruote::Amqp::Participant

Publishing messages

```ruby
  $dashboard.register(
    :toto,
    Ruote::Amqp::Participant,
    :exchange => [ 'direct', '' ],
    :routing_key => 'alpha')

  pdef = Ruote.define do
    toto
  end

  $dashboard.launch(pdef)

  # ...
```

### Ruote::Amqp::Receiver

Receiving messages.

```ruby
# TODO
```

### Ruote::Amqp::AlertParticipant

Ambushing messages from a process definition.

```ruby
# TODO
```


## requirements

* ruote[http://ruote.rubyforge.org] 2.3.0 or later
* amqp[http://rubyamqp.info/] 0.9.0 or later
* rabbitmq[http://www.rabbitmq.com/] 2.2.0 or later


## install

Please be sure to have read the requirements section above

    gem install ruote-amqp

or via your Gemfile (thanks [bundler](http://gembundler.com)).


## tests / specs

To run the tests you need the following requirements met, or the testing environment will fail horribly (or simply get stuck without output).


### RabbitMQ vhost

The tests use dedicated vhost on a running AMQP broker. To configure RabbitMQ
you can run the following commands (the RabbitMQ server must be running):

    $ rabbitmqctl add_vhost ruote-test
    $ rabbitmqctl add_user ruote ruote
    $ rabbitmqctl set_permissions -p ruote-test ruote '.*' '.*' '.*'

or by running:

    $ rake prepare


If you need to change the AMQP configuration used by the tests, edit the
+spec/spec_helper.rb+ file.


## daemon-kit

Kenneth Kalmer, the original author of the ruote-amqp gem is also the author of [DaemonKit](https://github.com/kennethkalmer/daemon-kit) a library/toolbox for building daemons.

It used to be the preferred way to wrap remote participants (as daemons) but lately Kenneth hasn't had much time for support. It's still full of excellent ideas.


## license

MIT, see LICENSE.txt

