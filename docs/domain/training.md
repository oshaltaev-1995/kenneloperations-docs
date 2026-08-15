# Training

Training is the manual planning workspace. It is architecturally separate from the Operations-only Winter automatic solver.

## Saved Groups and Daily Plans

A Saved Group is organizational membership. Profiles include Carousel, Autumn training, Winter training, and Winter safari. Group size and class guidance are profile-specific, and membership can retain useful context that would not be safe to run today.

Creating a Daily Plan copies selected group members into an independent snapshot. Later edits to the group do not mutate the plan, and plan roster replacements do not mutate the group.

`Ready` is the operational gate. It reevaluates each member on the plan date, checks duplicate/overlapping Ready work, validates profile constraints, and uses optimistic revision control. Injury, illness, pregnancy, treatment/rest/restriction contexts that make a dog unavailable block Ready. Archived and Deceased dogs cannot form an operational plan. Current source treats Retired and Front Yard context as advisory for local Training Ready, not as automatic group deletion. Workload warnings may require acknowledgement.

## Autumn

Autumn is manually arranged; it never invokes the Winter solver. An explicit layout contains exactly one Lead row, zero or more Team rows, and exactly one Wheel row in that order. Each row has one or two dogs. Singleton dogs are centered in print.

The harness is stored on the Saved Group and copied into an independent Daily Plan snapshot. Route loops and planned kilometres belong to the Daily Plan.

### Housing-proximity suggestion

The Autumn-only suggestion is advisory, pen-first, area-scoped, and based on physical map proximity. It does not assign a harness role or fabricate a pair. Applying a suggestion changes only the frontend working roster; dogs must still be manually placed in harness rows before Save. At a 2-of-3 occupancy boundary the operator decides which dogs belong—no arbitrary pair is claimed.

## Carousel

Carousel is a manual Training workflow using planned minutes rather than sled geometry. Its print contains comma-separated names only: no housing, status labels, or fake pairing.

## Winter Training

Winter Training supports Jenga 400 m or the standard 3 km route in a manual Daily Plan. It is not the customer Operations solver.
