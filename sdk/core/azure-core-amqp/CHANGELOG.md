# Release History

## 1.0.0-beta.4 (Unreleased)

### Features Added

- AMQP moved from a polling model to an asynchronous model. 

### Breaking Changes

- Removed the `QueueSend` API from `MessageSender` because it was not compatible with the new asynchronous model.
- The new asynchronous model requires the user to call `Close()` on the `MessageSender` and `MessageReceiver` 
to ensure operations have stabilized before destroying the object.
- For connection listeners (primarily test scenarios), if you call `Open()` or `Listen()` on a connection, you MUST call `Close()` 
before the connection is destroyed.
- The `Connection::Close()` method no longer requires that the caller provide connection disconnect information.
- The `Session::End()` method no longer requires that the caller provide session disconnect information.
- Several asserts have been added which will force termination of the running application if invariants have not been met.

### Bugs Fixed

- Several fixes related to the new asynchronous model. Ensures that message senders and receivers are always closed, 
and that resources are released.

### Other Changes

## 1.0.0-beta.3 (2023-09-07)

### Bugs Fixed

- When a message sender is destroyed, close the underlying AMQP link if it hasn't been closed already.

## 1.0.0-beta.2 (2023-08-04)

### Features Added

- Added `Azure::Core::Amqp::Models::AmqpBinaryData::operator=(std::vector<std::uint8_t> const&)`.
- Added `Azure::Core::Amqp::Models::AmqpMessage::MessageFormat`.
- Collection types (`AmqpArray`, `AmqpMap`, `AmqpList`, `AmqpBinaryData`, `AmqpSymbol` and `AmqpComposite`):
  - Added explicit cast operator to underlying collection type.
  - Added `find()`.
- Rationalized the return code for AMQP MessageSender and MessageReceiver and Management APIs to use AmqpError for error codes.
- Added additional AMQP Error values.

### Breaking Changes

- Renamed `Azure::Core::Amqp::Models::AmqpMessageFormatValue` to `AmqpDefaultMessageFormatValue`.
- Changed the return values for the MessageSender, MessageReceiver and Management APIs.

## 1.0.0-beta.1 (2023-07-06)

### Features Added

- Initial release
