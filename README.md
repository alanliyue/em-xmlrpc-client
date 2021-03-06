## em-xmlrpc-client

This gem monkey patches Ruby's built in XMLRPC::Client to be EventMachine + Fiber aware.  If you are not using EventMachine (or the reactor isn't running), then it will fallback to using XMLRPC::Client's default implemenation (using Net::HTTP).

## Example

  require "eventmachine"
  require "em-xmlrpc-client"

  EM.run do
    Fiber.new do
      client = XMLRPC::Client.new2("http://blah.com/api")
      result = client.call("someMethod", "arg1", 123) # Uses em-http-request.
    end.resume
  end


  client = XMLRPC::Client.new2("http://blah.com/api")
  result = client.call("someMethod", "arg1", 123) # Uses Net::HTTP like normal.

## Dependencies

{em-http-request}[https://github.com/igrigorik/em-http-request] is required if you want to use the EventMachine + Fiber aware implementation.

## Author

Christopher J. Bottaro

{\https://github.com/cjbottaro}[https://github.com/cjbottaro]

@cjbottaro

## Copyright and License

Copyright (c) 2017, Christopher J. Bottaro.

This project is licensed under the [MIT License](LICENSE.md).