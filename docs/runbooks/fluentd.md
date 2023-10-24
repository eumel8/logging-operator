# FluentdRetry

## Meaning

Fluentd retries connection to the target logging system.

## Impact

Logs are not shipped to the target logging system.

## Diagnosis

```bash
kubectl -n <controlnamespace> exec -it <logging>-fluentd-0 -c fluentd -- curl -v http://127.0.0.1:443
*   Trying 127.0.0.1:443...
* connect to 127.0.0.1 port 443 failed: Connection refused
```

## Mitigation

- Check if the target logging system is reachable.
- Check NetworkPolicies to reach the target logging system.
- Restart fluentd POD if TCP connection are still in SYN/TIMEOUT state
