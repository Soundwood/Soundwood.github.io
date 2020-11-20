---
layout: post
title:      "MORE Edge Details"
date:       2020-11-20 17:14:30 +0000
permalink:  more_edge_details
---

In creating my react/redux application for my final project I ran into some additional issues that you might experience as well. I wrote about some of them in my previous post. Here are a few more helpful items to improve your project.

## Adding GIFs to showcase your app on Github

I found this walkthrough most useful:
https://dev.to/kelli/demo-your-app-in-your-github-readme-with-an-animated-gif-2o3c

Broken down into simple steps:

1. Create a Screen Capture GIF using GIPHY CAPTURE
2. Move the GIF file into your project folder structure
3. Reference the GIF with: 
```
![Alternate Text](foldername(below_root)/foldername/filename.gif)
```

## Create a Constants File to keep things DRY

I found myself constantly referencing ‘https://localhost:3000’ whenever making calls to my backend API. Obviously this would change if I chose to host my project online somewhere. To make the process of switching all of these reference  easier I chose to set up a constants file.

I created a file called constants.js adjacent to my index.js file. Within the file I can simply create constants like so:

```
Export const BACKEND_BASE_URL = “http://localhost:3000”
```

The constant can now be referenced anywhere like so:
```
Import * as Constants from ‘../constants’

{Constants.BACKEND_BASE_URL}
```

## Formatting Money

We have been conditioned to see money in 1,000s. That is to say that a user would expect money to be formatted like money instead of an integere or decimal. I had several locations where I would need to perform this action so I chose to implement this code in my ScenariosBreakdown Container and then pass the function to its children via props. That way I really only need to write the function once. Also of note, this function was shamelessly stolen from stackoverflow. 

The function inserts commas as needed, handles negative values,  and removes extra decimals if needed. Highly useful.

```
 const formatMoney = (amount, decimalCount = 2, decimal = ".", thousands = ",") => {
        try {
            decimalCount = Math.abs(decimalCount);
            decimalCount = isNaN(decimalCount) ? 2 : decimalCount;
            const negativeSign = amount < 0 ? "-" : "";
            let i = parseInt(amount = Math.abs(Number(amount) || 0).toFixed(decimalCount)).toString();
            let j = (i.length > 3) ? i.length % 3 : 0;
            return negativeSign + (j ? i.substr(0, j) + thousands : '') + i.substr(j).replace(/(\d{3})(?=\d)/g, "$1" + thousands) + (decimalCount ? decimal + Math.abs(amount - i).toFixed(decimalCount).slice(2) : "");
        } catch (e) {
            console.log(e)
        }
    }
```

## Using Indexes as a key in child components is an antipattern

More information - https://medium.com/@robinpokorny/index-as-a-key-is-an-anti-pattern-e0349aece318

**Do this instead** - Use IDs from backend

**OR** Create unique ID with uuid

```
import uuid from "uuid"

function App() {
  return (
    <div className="App">
      <h1>{uuid.v4()}</h1>
    </div>
  );
}
```



