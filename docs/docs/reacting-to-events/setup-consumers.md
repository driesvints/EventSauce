---
permalink: /docs/reacting-to-events/setup-consumers/
title: Setup Consumers
published_at: 2018-03-11
updated_at: 2018-03-12
---

In order to process events you need to wire up your consumers
to your dispatchers. EventSauce ships with a
`SynchronousMessageDispatcher` which is used for testing, but
you can also use it as a regular dispatcher. It's recommended
to use a queueing/async dispatcher for better system resiliency,
reliability and general fault-tolerance. However, you're not
blocked from modelling simply because you're lacking that
infrastructure.

## Synchronous Message Dispatcher

```php
<?php

use EventSauce\EventSourcing\AggregateRootRepository;
use EventSauce\EventSourcing\SynchronousMessageDispatcher;

$messageDispatcher = new SynchronousMessageDispatcher(
    new ProjectorOne(),
    new ProjectorTwo(),
    new ProcessManager()
);

$aggregateRootRepository = new AggregateRootRepository(
    YourAggregateRootClass::class,
    $messageRepository,
    $messageDispatcher
);
```
