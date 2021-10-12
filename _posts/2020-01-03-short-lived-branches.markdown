---
layout: post
title:  "Short lived branches"
date:   2020-01-03 19:03:04 +1200
---


## Reviewing
Short lived branches enable fast reviews. There is little code to review and the reviewer has enough time to think the proposed changes through. If reviewer ask for changes then they can be easily introduced because there is not much code to change. It requires less mental capacity to write the code and to review it. There is more attention to naming and details. The beneficiary here is the quality of code and overall readability.
 
And if the taken approach is for some reason suboptimal, it is easy to discard it and start from scratch. Ideally the approach should be discussed upfront, but that is not always the case. Developers are very often attached to their code, especially if a lot of effort was put into it. The more effort the more attachment. It is less painful to throw away 1 day of work rather than more days of work.

If the task at hand grows unexpectedly then more time is needed to spend on a single branch. It's worth considering splitting the task into smaller ones, smaller branches. Splitting tasks into smaller pieces is one of the most important skills engineers (and not only) should learn. This is probably a topic for another post.

## Testing
Testing changes introduced by short lived branches is quick as well. Mainly because there are few functional changes. It is easy to explain the context and present the change to QA. 

## Deploying
Short branches are easy to deploy, especially when frequent deployments are possible. Introduced bugs are easy to spot, simply because the deployed change is small. Correlation between deployment and new errors can be easily observed. This a clear signal to roll back the release, effectively shortening time to recovery.

## Conclusion
Based on experience, my preferred amount of time spent on a single branch is up to 2 days.
The actors in this process, author, reviewer and QA are very productive. 
Adding feature flags to the mix makes the entire system easy to understand and follow.
