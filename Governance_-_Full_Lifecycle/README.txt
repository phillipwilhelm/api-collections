# Who this collection is for
Organizations who are ready to think about applying governance to the complete API lifecycle, rather than just the design stage. This collection covers everything from that design stage to how those APIs are supported post release.

# What does this collection do?
Provides a framework for assessing every asset designed, developed and consumed within the API lifecycle, so that it can be tested against an organizations defined standard for what a good API should look like.

# More

This is the API governance Postman collection for Union Fashion, providing a documented and executable process that can be applied to all APIs being developed to support business operations. Demonstrating how Postman collections and tests can be used to define and enforce governance across API operations, and self-service, and eventually automated way.

This governance framework is still being defined, and will keep evolving based upon the overall objectives of Union Fashion operations. Each top level area of this governance has it's own GitHub issue to help guide the adding, removing, and evolution of each of the governance requests that exist within each folder.

Each API being evoluated should have it's own governance environment, providing all the meta adata about the API being evaluated, and the store of met ricsof the governance process can scan, providing a snapshot of how well each API meets the governance criteria. Adding another environmental state to each API, helping bring each API into alignment with each other.

This governance collection works hand in hand with the API life cycle collection. You can't measure what you can't quantify. Without a a clear machine readable blueprint of what the API life cycle is it will be difficult to every properly govern and ultimately guide what is happening across APIs. This governance framework is not meant to be prescriptive. It is meant to show what is possible when it comes to using Postman to test not just the surface area of each API, but also the entire lifecycle for each API.

There is [a separate API governance collection dedicated to just governing the design process](https://documenter.getpostman.com/view/10394726/T1DwbZC8?version=latest), which is what most enterprise organizations are ready for. This one might be a little overwhelming for groups who aren't further along in their API journey. The goal is here is to try and define end to end governance for the entire lifecycle of an API.

Here are some things to keep top of mind as you are working with this collection:

- **This is a proof of concept -- use at your own risk!**
- **You will need your Postman API key in the environment**
- **Run the "Pull API Into Environment" before running anything else**
- **It uses Postman echo for each API request, and only pulling OpenAPI from environment**
- [**Here is the home page for this project**](https://github.com/union-fashion/home)
