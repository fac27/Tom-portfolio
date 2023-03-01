## 1. Write code that executes asynchronously

### Example of async await fetch function

```
async function fetchWeather(postcode) {
  try {
    const validateResult = await fetchResult(
      `https://api.postcodes.io/postcodes/${postcode}/validate`
    );
    if (!validateResult) throw new Error("Invalid postcode");
    const { longitude, latitude } = await fetchResult(
      `https://api.postcodes.io/postcodes/${postcode}`
    );

    let url = new URL(
      `https://api.open-meteo.com/v1/forecast?latitude=${latitude}&longitude=${longitude}`
    );
    let params = new URLSearchParams(url.search);
    params.append("current_weather", true);
    ...

    const response = await fetch(url + params);
    const json = await response.json();
    fetches++;
    return json;
  } catch (error) {
    // TODO improve error handling to give user feedback
    alert(error);
  }
}

```

## 2. Use callbacks to access values that aren’t available synchronously

### Example of reusable fetch function that can accept a callback to handle errors.

```
async function fetchResult(
  url,
  init,
  errorHandler = (url) => {
    throw new Error("invalid request: " + url);
  }
) {
  const response = await fetch(url, init);
  const json = await response.json();
  if (!json.result) {
    errorHandler(url);
  }
  return json.result;
}
```

## 3. Use promises to access values that aren’t available synchronously

All the above fucntions handle the promise returned by the fetch and pass through await and return the fulfilled value in a variable named repsonse. Similarly .json() returns a promise.

## 4. Use the fetch method to make HTTP requests and receive responses

Above ☝️

## 5. Configure the options argument of the fetch method to make GET and POST requests

### The following example shows passing options parameters for a post request, including headers and stringified body

```
async function fetchPostcode(latitude, longitude) {
  const body = {
    geolocations: [
      {
        longitude: longitude,
        latitude: latitude,
        widesearch: true,
        limit: 1,
      },
    ],
  };
  const url = "https://api.postcodes.io/postcodes";
  const result = await fetchResult(url, {
    method: "POST",
    body: JSON.stringify(body),
    headers: { "content-type": "application/json" },
  });
  if (!result[0].result) return null;

  return result[0].result[0].postcode;
}
```

## 6 + 7. Access DOM nodes using a variety of selectors, Add and remove DOM nodes to change the content on the page

This function renders an svg image in an Iframe and then adds that Iframe to the results section. that also handles accessibility attributes and avoids inserting multiple images to same child when changing image.

```
const renderImage = (weatherCode) => {
  const sectionElement = document.querySelector("#results");
  const firstDesc = sectionElement.firstElementChild;
  const currTemp = document.querySelector("#curr_temp");
  const insertIFRAME = () => {
    const iframe = document.createElement("iframe");
    iframe.src = `./icons/weather-codes/${weatherCode}.svg`;
    iframe.title = "WeatherIcon";
    iframe.ariaHidden = "true";
    iframe.tabIndex = "-1";
    sectionElement.insertBefore(iframe, currTemp);
  };
  // lots of nesting but seemed most efficient after diffrent refatoring attempts
  if (firstDesc.tagName == "IFRAME") {
    const prevCode = firstDesc.src.split("/").pop().slice(0, -4);
    if (weatherCode != prevCode) {
      firstDesc.remove();
      insertIFRAME();
    }
  } else insertIFRAME();
};
```

## 8. Toggle the classes applied to DOM nodes to change their CSS properties

Since there were lots of hidden elements it was necesary to make a reusable function for toggling given selectors with a shorthand to declutter code

```
const toggle = (selector, classname = "hidden") => {
  document.querySelector(selector).classList.toggle(classname);
};
```

## 9 + 10. Use consistent layout and spacing, Follow a spacing guideline to give our app a consistent feel

![Screenshot 2023-03-01 at 15 44 18](https://user-images.githubusercontent.com/44851616/222189588-ed96eeab-e993-4b48-a988-09dd82a2ff4a.png)

This example shows even spacing between all flex containers, the body, within each child of a flex container. 

Below shows this

```
/* ~?|| STACK ||  */

.stack > * + * {
  margin-top: 2.5rem;
}

.stack-sm > * + * {
  margin-top: 0.4rem;
}

/* ? || FLEX || */

.flex {
  display: flex;
}

.flex__wrap {
  flex-wrap: wrap;
}

.flex--scroll-x {
  overflow-x: auto;
}

.flex__col {
  flex-direction: column;
}

.align-center {
  align-items: center;
}
```

## 11. Debug client side JS in our web browser

Using Chrome dev tools I was able to debug client side using the elemnts tab. Then if weere debugging js i use DOM breakpoints tab, or stlyes for debuggin css, or the main elements tab for debuggin HTML 

![Screenshot 2023-03-01 at 15 40 53](https://user-images.githubusercontent.com/44851616/222188777-a379e349-6fe2-4de9-868c-303659f883e4.png)


## 12. Use console.log() to help us debug our code

### console.log to show that the google charts has started rendering..

as soon as the fucntion is triggered, alert the user/dev 

```
function drawChart() {
    console.log("rendering");
    const data = new google.visualization.DataTable();
    data.addColumn("string", "Hour");
    data.addColumn("number", "Temperature");
    data.addColumn({ type: "number", role: "annotation" });
    let rows = [];
    for (let i = 0; i < 24; i++) {
      const value = Math.floor(json.hourly.temperature_2m[i]);
      rows.push([
        `${i < 10 ? "0" + i : i}:00`,
        value,
        i % 2 == 0 ? null : value,
      ]);
    }
    data.addRows(rows);
```
