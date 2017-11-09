
# [HTML 5.0, Algorithm](https://www.w3.org/TR/html5/sections.html#outlines)

* `currentElement` is the element being entered
* `outlineOwner` is the element that owns the current outline
* `currentSection` is the currently active section -
   depending on the current node, an inner or an outer section

## A. entering a sectioning content element (SCE)

```
1. //- if currentElement is an inner SCE
   if(outlineOwner != null)

1.1. //- finalize the current outer section
     if(currentSection.hasNoHeading() == true)
       currentSection.setImpliedHeading()

1.2. //- save the outer context
     stack.push(outlineOwner)

3. //- switch to the inner context
   outlineOwner = currentElement

4. //- create the element's first inner section
   currentSection = new Section(currentElement)

5. //- associate the current element with that first inner section
   currentElement.parentSection = currentSection

6. //- initialize the element's inner outline with that first inner section
   currentElement.outline = new Outline(currentElement, currentSection)
```

## B. exiting a sectioning content element

```
1. //- finalize the element's last active inner section
   if(currentSection.hasNoHeading() == true)
     currentSection.setImpliedHeading()

2. //- restore the element's outer context
   outlineOwner = stack.pop()

3. //- switch currentSection to the last section of the outer outline
   currentSection = outlineOwner.outline.lastSection

4. //- add the element's inner top-level sections to that section
   //- let the current element contribute to the outer outline
   foreach(section in currentElement.outline)
     currentSection.addSubsection(section)
```

## C. entering a sectioning root element (SRE)

```
1. //- if currentElement is an inner SRE
   if(outlineOwner != null)

1.1. //- no "currentSection.setImpliedHeading()"
     //- do not finalize the current outer section
     //- do not let the current element contribute to the outer outline
    
1.2. //- save the outer context (1)
     stack.push(outlineOwner)

2. //- switch to the inner context
   outlineOwner = currentElement

3. //- save the outer context (2)
   //- save the last active outer section
   //- associate the current element with the current outer section
   currentElement.parentSection = currentSection

4. //- create the element's first inner section
   currentSection = new Section(currentElement)

5. //- initialize the element's inner outline with that first inner section
   currentElement.outline = new Outline(currentElement, currentSection)
```

## D. exiting a sectioning root element

```
1. //- finalize the element's last active inner section
   if(currentSection.hasNoHeading() == true)
     currentSection.setImpliedHeading()

2. //- restore the element's outer context (2)
   //- restore the last active outer section
   //- do not add the element's inner top-level sections to any outer section
   //- do not let the current element contribute to the outer outline
   currentSection = currentElement.parentSection

3. //- restore the element's outer context (1)
   outlineOwner = stack.pop()
```

## E. exiting an SCE or an SRE, if the stack is empty

```
1. //- finalize the element's last active inner section
   if(currentSection.hasNoHeading() == true)
     currentSection.setImpliedHeading()

2. //- Return from traversing the tree
```

## F. entering a heading content element (HCE)

```
1. //- if the element is the first heading, then
   if(currentSection.hasNoHeading() == true)

1.1. //- let that heading element be the heading of the currentSection
     currentSection.heading = currentElement

2. else if(outlineOwner.outline.lastSection.heading.isImpliedHeading
   || (currentElement.rank >= outlineOwner.outline.lastSection.heading.rank))

2.1. currentSection = new Section(currentElement)
2.2. outlineOwner.outline.add(currentSection)
2.3. currentSection.heading = currentElement

3. else

3.1. candidateSection = currentSection
3.2. begin loop

3.3. if(currentElement.rank < candidateSection.heading.rank)
3.3.1. newSection = new Section(currentElement)
3.3.2. candidateSection.addSubsection(newSection)
3.3.3. currentSection = newSection
3.3.4. currentSection.heading = currentElement
3.3.5. exit loop

3.4. else
3.4.1. newCandidateSection = candidateSection.parentSection
3.4.2. candidateSection = newCandidateSection
3.4.3. continue loop

3.5. end loop

4. //- just an optimizational step
   stack.push(currentElement)
```

## G. final steps (tree traversal is not yet done)

```
1. //- when exiting an unassociated node
   node.parentSection = currentSection
```

## H. final steps (tree traversal is done)

```
1. //- an optional step
   node.heading = node.parentSection.heading
```
