I design systems and build them: real-time and distributed backends, network protocols, and the data paths
between them.

Most recently I was the founding engineer at Lingacom. I authored the architecture of the real-time monitoring
and control system behind cosmic-ray muon imaging installations, designed its binary protocol, and led it to
production. Before that I worked on attribution infrastructure handling over 500,000 requests per second on AWS
at Singular. At ControlUp I built multithreaded C++ libraries that carry monitoring data over Citrix and VMware
Horizon virtual channels.

## Projects

**[tundra](https://github.com/fimkap/tundra)** · C++23  
A user-space TCP/IP stack, from Ethernet to TCP with NewReno loss recovery, running on a Linux TAP device against
the real Linux stack. Transfers in both directions match their SHA-256 byte for byte. Its fuzzers ran 38.6 million
parser inputs and 598 thousand stack programs clean under ASan and UBSan. The NEON checksum runs at 50–66 GB/s,
up from 7, once GCC no longer fuses its two loads into one `LDP`.

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

## How I work

Spec first, then tests that try to break it, then measurements saved next to the code.

I build with AI coding agents. tundra, sluice and slotstream each start from a written spec: the scope, what's
left out, and the experiments that settle each design question. Claude Code implements it in small steps, and a
step is done when its tests pass, not when the code looks right. Each repo's `docs/ai-workflow.md` shows the
guardrails and the bugs they caught.

[LinkedIn](https://www.linkedin.com/in/efimpolevoi)
