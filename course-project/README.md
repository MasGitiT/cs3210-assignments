# Course Project

## Introduction

The goal of the course project is to solidify the foundational C++ knowledge obtained in this course by desinging and implementing a functional, larger-scope software system. The project topic has been chosen to necessitate the use of a wide array of language concepts and features we studied/will study, including separate compilation, user-defined types, inheritance, run-time polymorphism, resource management, smart pointers, containers and algorithms, file input/output, and other standard library facilities. We haven't covered some of these topics in details yet, but, generally speaking, you should be able to start working of the project right away. 

Note that the project definition includes a couple of "stretch goals". Those are optional enhancements on top of the core project that you might choose to explore to obtain extra credits (or perhaps simply because they seem fun).


## Grading / progress tracking

**The project due date is midnight, Wednesday, May 1st.** Late project submissions will be subject to a penalty of a 25% reduction in points for every 24-hour period they are late.

As per the syllabus, **the project constitues 30% of your total grade**. The project's grade itself will be a function of the following criteria:

| Project Evaluation Criteria | Grade percentage | Explanation | 
| ----------------------------- | --------------------- | -------------- |
| Functional requirements | 50% | Does the delivered software satisfy the project's stated functional requirements? |
| Quality of the final executable | 15% | Absence of errors during the normal execution, as well as graceful handling of error conditions. | 
| Quality of the design and implementation | 15% | Is the project implemented using idiomatic, well-structured C++? |
| Test coverage | 10% | Usage of unit/functional testing to assist project development. |
| Weekly project updates | 10% | See below. |

### Weekly project updates

To help facilitate a healthy development pace, you are required to submit (on Slack) **weekly project updates which answer the following questions**:

 - What have you done on the project so far?
 - What are you currently working on?
 - Are there any unsolved issues/errors you’re currently trying to debug?

**The weekly updates are due at midnight every Wednesday, starting from Wednesday, April 3rd, up to and including Wednesday, April 24th**.

If you have any questions or concerns, please reach out as soon as you develop them. Regular demos/office hours visits to discuss your progress are essential for avoiding surprises with your final project grade.

### Progress tracking through Github

Due to the long-running nature of this project, **we'll be using Github to host the project's code and track your development progress**. If you don't have a Github account, please create one using your @uiowa.edu email address. If you have an existing Github account you'd like to use, please make sure your @uiowa.edu email is listed as your [public email](https://github.com/settings/profile). 

Once you are logged in to Github, follow [these instructions](https://help.github.com/en/articles/create-a-repo) to **create a private repository for your project**, then invite **@agurtovoy** and **@srinvsn** as [collaborators](https://help.github.com/en/articles/inviting-collaborators-to-a-personal-repository). 

When reporting progress in your weekly updates, please **make sure to push the corresponding code to your Github repo**. Failure to do so consistently will affect the "Weekly project updates" portion of your project grade.

Use of Github issues and wiki functionality to track & document your project state is welcome and encoraged. 


## Project definition

The project objective is to **build an interactive command line program that (crudely) simulates a small terrestrial ecosystem** according to the rules below. 

The core notion of the simulator is that of an iteration: a single "step" of the simulation during which the ecosystem transforms itself to its next state according to its [rules](#ecosystem-rules) (think [Conway's Game of Life](https://en.wikipedia.org/wiki/Conway%27s_Game_of_Life)).

An ecosystem is defined by two inputs:
  - a rectangular [map of the area](Area-Map.md) that describes the (initial) location of the geographic features and the living organisms (plants + animals) that populate the area;
  - a [list of species](Species.md) populating the ecosystem, together with their essential characteristics and inter-relationships. 

The ecosystem map and the list of species are loaded from the corresponding files provided to the program as command line arguments. 

Runing the simulator starts a new simulation session. Within a single simulation session, the user can select to run a single iteration, or a "batch" of several iterations at once (e.g. 10 or 100 iterations). After each run, the simulator prints the session's current ecosystem state to the console. The user can then chose to continue the simulation session (by doing another run), save the current ecosystem state to a file, or exit.

### Ecosystem rules

1. During each iteration every organism in the ecosystem gets a chance to perform its living functions (move, grow, consume). Plants get their turn first, then the herbivores, then the omnivores, then the cycle repeats at the next iteration.
2. Animals move freely around the ecosystem to find food, but they cannot move over the geographic obstacles, plants or other animals (unless they are consuming them). All animals move with the same speed (one block per iteration).
3. Plants remain static and don't spread into new areas.
4. Each living organism has an associated number of "energy points" it gives to the organism that consumes it.
5. Plants don't eat other organisms; herbivores eat only plants; omnivores eat plants and other animals.
6. Plants that have been eaten regrow in the same location according to their "regrowth coefficient"; for example, a plant with a regrowth coefficient of 2 regrows in two iterations. A plant cannot regrow if its location is currently occupied by an animal.
7. Animals that have been eaten are removed from the similation.
8. Each animal has a current energy level as well as a "max" energy level that limits the number of energy points they can absorb. All animals start the simulation with a current energy level equal to their "max" level. Each move subtracts one point from their current energy level. An animal with zero energy points dies and is removed from the simulation. 
9. An animal can consume another organism only if it can add a greater-than-zero number of the consumed organism's energy points to its energy level without going over its "max" limit. To consume another organism, the consumer has to move to the organism's position.
10. Two adjacent animals of the same species with the current energy level that is more than a half of their "max" can produce an offspring (given that there is space next to either of them to place the offspring).


## Stretch goals (optional)

### Map generator

Add an option to programmatically generate a map of a certain size based on the list of species and possibly other parameters (e.g. area percentage for the geographical features).

### Population statistics

Collect the population statistics (number of live organisms for each species) on each iteration, allow user to save the accumulated session stats as a [CSV file](https://en.wikipedia.org/wiki/Comma-separated_values) that can be graphed by 3rd party software (e.g. Excel).
