## GPSTEC302 - SaaS Reference Architectures: A Review of Real World Patterns and Strategies

#### Tod Golding: Partner Solutions Architect with aws saas factory (todg@)


#### One Goal, Many Flavors: Silo, Bridge, Pool
- Silo: Every Tenant has seperate resources
- Bridge: some shared resources, some seperate resources (combo of silo and pooled)
- Pooled: multi tenancy across all tiers


#### Key challenges:
- Variable Tenant Load
	- new tenant onboarding
	    - bulk operations
	- complex scaling profiles
	- Seamless Tenant identitiy
	    - binding users to tenant
	    - efficient resolution of context
	    - minimally invasive
	    - best case: make multi-tenancy invisible to developers
  - Variable data footprint
	    - limiting storage bottlenecks
	    - cross-tenant impact
	    - cost optimization
    - Operational agility
        - small, repeatable deployments
        - proactive metrics/monitoring
        - tenant-level health/policy maagement


#### Multi-tenancy can vary at every layer
- don't be afraid to make multi-tenant decisions at a service by service level
- service-optimized tenancy

#### The common thread: Agility
- frictionless onboarding
- zero downtime deployment
- unified, proactive monitoring
- usage and consumption metrics
- centralized billing


#### SaaS Architecture pattern landscape
- onboarding | application access (auth) | api access
- application services
- storage partitioning (tenant isolation)


#### The Patterns
- The SaaS monolith
- Microcervies SaaS with containers (pretty close to wellmark)
- Serverless SaaS (best option, for cost optimization due to only spinning up what's needed per function per tenant)


- multi-tenant aware application services
- minimize developer awareness of multi-tenant policies

#### Storage Partitioning Patterns
- Silo Relational
- Silo NoSQL
- Pool Relational or noSQL


#### Avoiding tenant bottlenecks
- scaling tenant partitioned data
        - shard mapping
        - serverless storage <- look into this
- role and policy-based isolation
- siloed compute isolation
    - vpc per tenant
    - namespace per tenant
    - iam role per function (lambda)
- pooled compute isolation
	 - tenant scoped credentials to control access to each resource
- tenant data isolation
    - iam role per tenant
        - use to control access to services
        - use to control rows within data (the dynamodb example)
    - using policies to isolation shared resources
    - full stack isolation (bad for cost)


#### onboarding patterns: the building blocks
- signup (form/process)
- user identity -> maped to -> tenant
- provisioning & configuration
- billing and account management

- zero touch, volume onboarding
- enterprise, low volume onboarding

- delayed tenant detection (auth up front, but have service figure out tenant) introduces bottleneck at service level
- upfront tenant detection changes auth process but provides user with tenant creds to pass to all future services for them to use to provide access to tenant resources.

"when you don't control the identity provider your auth flow in SaaS just gets harder"


#### metering and analytics patterns
- pooled analytics data


#### Takeaways:
- no single pattern fits all SaaS businesses
- SaaS architecture mush embrace variable consumption
- Metrics and analytics are foundational to SaaS architecture
- getting isolation right can be challenging
- automation and agility are essential
