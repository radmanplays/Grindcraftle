# Common mistakes

 1. Forgot to put a comma between every value in a list and after every property in areas, grinds, crafts, resources, etc.
 2. Put text outside of quotation marks (""). All **text** except true/false should be in quotation mark. Resource names in the `addResources` function only need to be in quotation marks if they have multiple words, though.
 3. Put numbers or booleans (true/false) inside quotation marks. Numbers and booleans should never be in quotation marks, except when you are using numbers as text (either in a name or description).
 4. Forgot a bracket (`[]` or `{}`). Always remember to put brackets both before and after the contents of a grind, craft or resource:

```
dirt: {
    image: "images/dirt.png",
},
```

 5. Forgot to add a resource to the `addResources` function. All resources that are used in grinds/crafts should be added to the `addResources` function first. If not, the game won't work.

## Specific Scenarios (W.I.P.):

### The best tool is not selected when grinding a resource:
 - Put the best tool first in the time list, or else a weaker tool will be selected first.

### Failed to execute 'btoa' on 'Window':
 - Some letters or symbols outside of the english alphabet might break the save encoding system. If you get a this error message, you'll probably have to change some of the resource, grind or area names.