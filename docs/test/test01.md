[TOC]

# Test01

## AdrianTest1

Some text just testing if the br tag works properly. Let me place one here <br> in the middle of the sentence.

## AdrianTest2

Now test blockquote with the guide info

> Release 5.26
>
> Document number: TP_OpenL_DG_3.6_LSh
> 
> Revised: 10-13-2022
> 
> OpenL Tablets Documentation is licensed under a Creative Commons Attribution 3.0 United States License.

And here is another pgf

Now lets see if it is better as code

```
Release 5.26

Document number: TP_OpenL_DG_3.6_LSh

Revised: 10-13-2022

OpenL Tablets Documentation is licensed under a Creative Commons Attribution 3.0 United States License.
```

And here is another pgf

Now test admonitions

!!! note
    You should note that the title will be automatically capitalized.

!!! danger "Don't try this at home"
    ...
    
!!! important ""
    This is an admonition box without a title.
    
    
 NOW SOME NUMBERED HEADING TESTS
 
 Image using markdown
 
![](../img/indexpage/indexpageimage00.png)
 
 
 
 
 Full width image using html
 
<img src="../../img/indexpage/indexpageimage00.png">


Reduced width image using html

<img src="../../img/indexpage/indexpageimage00.png" width = "400">


Reduced width and centered image using html and putting it inside a tag

<center>
<img src="../../img/indexpage/indexpageimage00.png" width = "400">
</center>

and again

<img src="../../img/indexpage/indexpageimage00.png" width = "50%" display:block margin-left:auto margin-right:auto>

Now here is a list within a list

- Bullets
  - 2 spaces
    - 4 spaces
        - 8 spaces
- more

Conclusion (looking at RTD, not Github): 2 spaces does nothing. 4 spaces gives first indent. 8 spaces gives second indent

A new list but with indents:

- Bullets
    - 1 indent
        - 2 indents
            - 3 indents
                - 4 indents
- more



1. Apples
                        1. Royal Gala
                        1. Other
1. Pears
1. Bananas

Got a question? Drop us a line: <support@writage.com>.

