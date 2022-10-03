# Feedback Loops

2016 - When Angular* Was introduced (Angular 2 a the time)

## Inner Loop

- Everything that happens *before* we push the code.
- TypeScript provides a better "Inner Loop" experience.

```javascript
const rover = new Dog();
rover.meow();
```

- Testing in 2016 With Angular
    - "Unit" testing tool called "Karma"
    - A component and service testing tool called "TestBed" (you use this in your Karma tests)
    - And an "End-To-End" testing tool called Protractor.
        - Protractor was NOT usable in our "inner loop"
        - Replacements
            - Cypress - inner loop development because of the DX (Developer Experience)
            - Playwright - originated at Microsoft
                - Arguably better for outerloop. (Actual acceptance testing, etc.)
                    - "Smoke Testing" - 


## Outer Loop

- Everything that happens *after* we push our code to the repo.
- CI (Build, etc.) portion
- CD - deliver the code to the "next" environment.



## CI/CD "Mindset"

"Every day, deliver code to the next environment" - and we "pretend" the next environment is production.

- No long lived feature branches
- "Trunk" based development.

Software Development "Hells"

- "Merge Conflicts"
- "Finding issues WAY after I've written the code"
    - Long outer loops.
- "Vague Requirements"
    - For a lot of this stuff (UI in particular) WE HAVE NO IDEA WHAT WE ARE DOING.
    - "Hypothesis Driven Development"
        - 


"Churn" - just meaning you are changing things a LOT.
