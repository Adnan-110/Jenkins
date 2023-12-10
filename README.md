# Jenkins
This is a repository created to host and document all the learnings related to Jenkins starting from bacis to advanced.

We are going to write pipelines using both declarative and scripted pipelines.


### What is a pipeline ?

```
    Pipeline is nothig but flow that defines what to happen first and next. Typically this is acronmym used in Jenkins.
```

### Types of Pipeline jobs ?

```
    Pipeline jobs can be writtent by using 2 ways :

        1) Declarative Approach         ( Using Jenkins Provided Options : Non-Programmatic )
        2) Scripted Pipeline Approach   ( This is written by using Groovy) [ groovy is a wrapper to java ]


```
>>> PS : we are going to learn groovy as well from bacis to advanced like a Cloud & DevOps Engineer

### Pipeline Classification

```
    v0 : Freestyle  ( UI ) 
    
    v1 : Scripted Pipelines  ( groovy )

    v2 : DSL / Declarative Pipelines

    v3 : YAML [ Still in the development phase ]

```

### Naming Standard of a Jenkins Pipeline.

```
    Pipelines are supposed to be enclosed in a file that end's with Jenkinsfile [ J as in caps ]
```