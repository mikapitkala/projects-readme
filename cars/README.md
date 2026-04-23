# cars

A website that showcases information about different car models, their specifications, manufacturers, and more.

## Features

- **Look at 50 car models**: Look at a collection of cars
- **Basic Recommendation Algorithm**: Scores models, brands and categories based on interactions
- **Filtering**: Filter by manufacturer, category, country
- **Comparison**: Side-by-side model comparison. Unlimited models
- **Debug Mode**: Performance metrics and request information
- **Responsive Design**: ~~Works well~~ Should function on desktop and mobile
- **Theme Support**: Light/dark mode toggle
- **Async Logging**: You can set logging level to minimal or verbose
- **Config File/Default Config**: You can set up the API address, server address and logging level. Includes a default configuration that should just start instantly


## Project Structure
```
├── api-server/            # Node.js API server
│   ├── data/              # JSON data files
│   ├── img/               # Car images
│   ├── main.js            # API entry point
├── cmd/cars/              # Go web server
│   └── main.go            # Main application entry
├── internal/              # Go internal packages
│   ├── client/            # API client
│   ├── handlers/          # HTTP (and other) handlers and helpers
│   ├── color/             # Pretty colors
│   └── config/            # Configuration handler
├── web/                   # Frontend resources
│   ├── static/            # Stylesheets
│   └── templates/         # HTML templates
├── config.json            # Configuration file
└── README.md              # This documentation
```

## Installation

### Prequisites
- Go go 1.23.5
- Node.JS 
- npm


### Installation & Running

1. Clone the repo
`git clone https://gitea.kood.tech/mikapitkala/cars.git [target folder]`
2. Enter the folder
`cd [target folder]`
3. The web server makes an attempt to install the dependencies and then run the API for you
`go run cmd/cars/main.go`
4. If that fails, you can check the README in `/api-server` and start it manually and then run step 3 again
5. There's a `config.json` file in the root, which will be used by default. If it's missing there are hardcoded defaults that match the config file
6. You can set logging to `minimal` (the default setting) or `verbose`
7. When you stop the program, it'll make an attempt to shut down both servers gracefully and wrap up logging.

## Usage


### Main models view

When you start you'll see a collection of cars in cards. You can view additional **details** about any car by clicking on the `View Details` button on it.

You can access the **filters** by clicking on the `Filters` box on top. Select any filters you want and hit `Apply Filters` to get a listing that matches your preferences. `Clear Filters` will clear all filters.

You can **compare** different models by selecting them with the `Compare` button and then hitting the `Compare Selected` button on the bottom right corner. You can as many cars as you want.

There is a **recommendation algorithm** on the main page that orders the cars based on which it thinks you like listed first and the ones you don't care about as much listed last.

You can open a **debug panel** by clicking `Enable Debug` button on the top navitation bar. It'll show you some performance metrics and information about what's going on behind the scenes along with all the **recommendation scores** for all the cars. You can also test `404`, `405` and `500` errors. You can hide it by clicking `Disable Debug`.

You can **reset the recommendations** by clicking on `Wipe Recommendations` button on the top navigation bar. This will wipe all recommendation parameters and reset the algorithm.

You can **reset all settings** by clicking on the `Wipe All Cookies` button on the top navigation bar. This will wipe all settings and recommendations effectively resetting the application.

You can **switch between dark and light mode** with the `Dark/Light Mode` button on the top navigation bar. Setting is saved in a cookie.

If your window is very narrow, the top navigation bar will get compressed into a **hamburger menu**. You can access all the above options by clicking on the menu icon.

### Detail view

Here you will find the **specifications** of a particular model. There will also be some information about the **model** and **manufacturer** fetched from Wikipedia. You can access it by expanding the `About...` cards.  You can click on the buttons on the bottom right to open the Wikipedia entry in a new tab.

You can **like** and **dislike** the particular model on the bottom of the page. This will affect the ranking in the main models view.

Hit `Back to Models` to return to front page. It'll attempt to scroll to the model you were looking at, since it may have moved if the recommendation scores changed.

### Comparison view

Here, you can combine one (although what's the point) or more (up to all of them) car models with each other in a convenient horizontal carousel. Just scroll horizontally to look at the different specifications. You can hit `View Details` button to check the details for that particular model (comparison is not saved). You can return to home page with `Back to Models`

## Extras

### Recommendation Algorithm
Each interaction with a model generates *points* based on multipliers:

```
	ViewWeight         = 1.0
	LikeWeight         = 3.0
	DislikeWeight      = -4.0
	CategoryWeight     = 0.3
	ManufacturerWeight = 0.3
```

The baseline is a *view*. Whenever you `View Details` on a *model*, it gets `1.0`, while the *category* and *manufacturer* get `0.3`. *Likes* and *dislikes* function similarly, but have a higher multiplier. All scores get stored in a cookie.