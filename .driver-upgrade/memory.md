# What we know about yugabyte/gocql

Written by earlier upgrade sessions. Every line cost a run to discover.

Treat it as a starting point, not as fact: the tree may have moved since. If
something here is wrong, correct it -- that is worth more than the upgrade
itself, because the next session inherits whatever you leave.

Add what you learn under "Learned this run". Anything above it is already
stored; only new lines are kept.

## Learned this run

- Upstream moved Type definition from marshal.go to types.go between base and target
- Upstream refactored Marshal/Unmarshal to use info.Marshal()/info.Unmarshal() delegation pattern
- TypeJsonb (YugabyteDB-specific 0x0080) needs varcharLikeTypeInfo, registered in types.go, and case in fastSimpleTypeLookup
- Several early commits have typo "Ddocumentation" that gets fixed later - keep correct spelling
- commit 7677511 "Update README" was already upstream and git dropped it automatically
- YugabyteDB workaround for issue #1312 forces params.skipMeta = false
- Commit 311742e drops `body` field from function retrieval and `return_type` from aggregate retrieval
- PartitionAwarePolicy (commits 34-35) is major YB feature adding:
  - getClusterPartitionInfo() calls in events.go (on schema/node events)
  - getClusterPartitionInfo() call in host_source.go GetHosts()
  - New getHostInfoFromIp() helper in host_source.go
  - YBPartitionAwareHostPolicy as default policy in session.go
  - New refreshPartitionMap.go file
  - Extensive policy implementation in policies.go
- Many duplicate commits in first 35: README, LICENSE, NOTICE, import paths, JSONB - most resolve automatically or as empty
- Test files for YB features should be taken with --theirs
