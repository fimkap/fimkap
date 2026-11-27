Senior engineer and hands-on architect, at home in both 0 → 1 builds and systems at scale.
Most recently I was the founding engineer on a real-time platform that controls hardware in the field, and I owned it end to end through to production: event-driven ingestion, live telemetry and the operator console. Before that I worked on a multi-tenant, event-driven attribution pipeline on AWS: 64 shards, 500k+ rps.

## Projects

**[tundra](https://github.com/fimkap/tundra)** · C++23  
A user-space TCP/IP stack, from Ethernet to TCP with NewReno loss recovery, running on a Linux TAP device
against the real Linux stack. Transfers in both directions match their SHA-256 byte for byte. Every byte a
network stack parses comes from outside, so a read past the end of a buffer can become a security hole. Such
bugs rarely crash on their own, so the tests and fuzzers run with two compiler options that add checks to the
program and stop it the moment a bug happens. ASan (AddressSanitizer) catches any read or write outside valid
memory. UBSan (UndefinedBehaviorSanitizer) catches undefined behaviour, such as a signed overflow, which can
pass in testing and break once the compiler optimises the code. Fuzzers generated 38.6 million inputs for the
parsers and 598 thousand runs of packets, timer events and API calls against a live stack, and both checks
stayed silent; an earlier run caught one real bug, since fixed. The NEON checksum runs at 50–66 GB/s, up from 7,
once GCC no longer fuses its two loads into one `LDP`.

**[sluice](https://github.com/fimkap/sluice)** · Go  
A Kafka-style broker built to measure the trade-offs log-based systems make. Group commit kept every write on disk
before its ack at 56k records/s with 64 producers, against 2.3–3k with an fsync per write. With one slow follower,
Kafka's ISR rule fell to 149 records/s while a majority quorum held 5.9k.

**[slotstream](https://github.com/fimkap/slotstream)** · Go, PostgreSQL  
Change data capture from PostgreSQL done four ways, with its own pgoutput decoder, exactly-once delivery into
PostgreSQL and S3, and failover slots. Polling lost every delete, triggers cost 3.4× the WAL, and the streaming
protocol delivered with a p99 lag of 12 ms.

**[dynamic](https://github.com/fimkap/dynamic)** · Swift  
Streams a million-row CSV into ScyllaDB with backpressure. Swift has no official driver, and the one that worked was
broken in five ways, so the loader has its own connection layer: 37.3 s and 818 MB became 19.5 s and 7 MB.

**[termpix](https://github.com/hopey-dishwasher/termpix/pull/15)** · Rust  
Fixed alpha blending in this terminal image viewer (300+ stars); merged upstream.


[LinkedIn](https://www.linkedin.com/in/efimpolevoi)
