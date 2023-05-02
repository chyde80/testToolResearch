# Perf Testing Notes/Considerations

Great, comprehensive listing of almost the entire perf/load marketplace:

[GitHub - mgasiorowski/performance_testing: Tools, articles, etc. related to performance/load/etc. testing.](https://github.com/mgasiorowski/performance_testing) 





 



* Language - Python, or language-agnostic/CLI tool
* Performance/load/spike(+/-) testing
* Support for event-driven messaging services
    * gRPC, etc
* Paid vs. open-source
    * Prefer OSS as it’s free, and more control over the tool
* Flexibility - licensing model (if paid)
* CI
    * Jenkins pipelines (plugins)
* Eventually have a test-only DB or DBs for specific usage
    * Contract
    * functional/state
    * Perf/load/spike/etc.
    * Etc..
* Region performance
    * Need to think about different AZs
    * Our apps will start in US-West but we need to test as users in different AZs across the world
* Have a “synthetic” pinging/using different areas with very small impact to heuristically see if the app areas are performing correctly so users don’t have to find it
* Reporting
* Analysis
    * Feed perf results to log analysis like grafana
        * Does IA already have grafana and alerts set up?
            * Hook into existing
