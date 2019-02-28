# Effective Behaviors

Some behavior may not be automated (at least pre Artificial General Intelligence, and post AGI the meaning of automation must change). 

For behavior that can be automated, sometimes the cost to automate is too high with existing skill set and tooling, or refinement may be required to prevent automating the wrong thing.

This document is intended to consolidate what I have learned that has not yet been automated.

## Debug

Not seeing what you are expecting? Ask yourself:
- Do you have a baseline?
  - When was it set?
  - How did you document it?
- Are you using the most recent changes?
- Are you using the most recent dependencies?
- Are you comparing to the most recent implementation examples?
- If there have been changes, have you looked at the code that changed?


## Speed

Quality cannot be sped up, but large tasks can be broken into smaller ones. Always aim to have usable code as soon as possible, even if what you are shipping is tiny. 

Find the smallest possible thing you can deliver and then _take your time on it_. 

> Slow is smooth. And _smooth is fast_.
>
> Navy SEAL saying

## Code Reviews

### Requesting

Before your commit:
- run any and all linters you can

After the commit and prior to opening or updating a merge request, take a walk. The longer the better. _Do not skip this step no matter how pressed for time you are._ 

> If you don't have time to do it right, you will have to find time to do it over.

When you get back from your walk, read the code as if reviewing it for another technologist. 

### Providing

Check for:
- dead code
- commented out code
- names that do not make sense
- repeated code
- `TODO` comments should not be merged
- `FIXME` comments should clearly indicate what work would have been included, time permitted
