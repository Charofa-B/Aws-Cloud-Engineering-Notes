# EventBridge
* `Serverless service` that `facilitates` the creation of `event-driven applications`.
* Building `loosely-coupled` systems that interact by emitting and responding to events.
* Allows you to `connect` diverse `sources`, including `custom applications`, `AWS services`, and `third-party software`.

## Event Buses
* Acts as a `central hub` for `routing events` from various sources to `multiple destinations`.
* `Receives` incoming `events` and based on `predefined rules`, `distributes` them to appropriate `targets`.
* `Rules linked` to an event bus examine incoming events. Each rule assesses whether an event aligns with its `specific pattern`.If a `match is found`, EventBridge `forwards` the event to designated targets.
* Rule is `tied` to a particular event bus,
* We can have `multiple` event `buses`, and `events` can be `routed across them`depending on your architecture.

## how Event Buses work
1. **Event Source** Event is `generated` from a `source`.
2. **Event Bus** Event is `sent` to an `event bus`.
3. **Rule Matching** `EventBridge` evaluates the incoming `event` against the `rules associated with the event bus`.
4. **Target Invocation** If the event `matches a rule`, EventBridge `invokes` the `target(s) specified in the rule`.

## Event Bus Types:

**Default Bus** `Automatically available` in each `AWS account`, `receives` events from `AWS services`.

**Custom Bus** `Created` by `you` to `organize` or `isolate events`.

**Partner Bus** For `SaaS` partner `integrations`.

<br><br>

## Rules
* **Event-Based Rules** 
    1. An `event` is sent to your `event bus`.
    2. The `rule checks` if the event matches a `pattern you defined`.
    3. If the event `matches`, it’s `forwarded` to the `rule’s target(s)`.

* **Schedule-Based Rules**
    1. A `schedule` triggers the rule at a `predefined time` or `interval`.
    2. The r`ule activates` `automatically` according to the `schedule`.
    3. The rule `sends` a `generated event` to the rule’s `target(s)`.

You can define `patterns` that match `dynamically based` on `event` content.

<br><br>

## Targets
* targets are `endpoints` that `receive events`.
* When an `event` `matches` a `rule's pattern`, `EventBridge` processes the `event` data and `sends` relevant `information` to the designated `targets`.
* Important to note that `EventBridge` `requires` `permission` to access the `target` `resource`, Check the official webs page for permissions types.
* A single `rule` can have up to `five targets`, and each `target` is `triggered` in `parallel`.
* there might be a `brief delay` before `newly` `added` or `updated` `targets` become `active`