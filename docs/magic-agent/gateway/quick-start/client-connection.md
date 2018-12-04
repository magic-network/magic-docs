# Client Connection

To test that your provider setup is complete & that a user can connect, use the following methods:

1. Verify Magic Gateway Logs
1. Use client-cli in testing mode

## Verify Magic Gateway Logs

From the gateway server device, run the following commands:

```
docker ps
docker logs -f <containerId from previous command>
```

The logs should contain no errors.

## Client-cli in testing mode

TODO: add client-cli method of testing a specific ssid. 