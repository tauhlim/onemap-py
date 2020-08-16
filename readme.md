Python Wrapper for SLA's OneMap API
========================================

Introduction
-------------
This package provides a simple way to query data using the OneMap API in Python.

OneMap arranges its API endpoints by groups, and this package is organized to reflect that grouping.

onemap-py allows you to make queries corresponding to the OneMap API, and returns the results to you in a standard
python `dict`.

## Sample Usage

```python
import onemap_py
x = onemap_py.Client("email@hostname.com", "password")

# Search for an address
# Note: For address search, no authentication required
gh = x.search("GRAND HYATT")
gh = gh['results'][0] # Take the first result

# For other queries, need to authenticate
x.authenticate() # if email and password were None, interactive prompt

# Get planning area for Grand Hyatt
planning_area = x.PlanningAreas.find_planning_area(gh['LATITUDE'], gh['LONGITUDE'])
planning_area = planning_area['pln_area_n'] # Get the name

# Get some population-related information for the planning area
avail_data = x.Population.available_data_types # find all available data types supported by the OneMap API
x.Population.get_population_data("age", year = 2018, planning_area=planning_area)

# Get route from Grand Hyatt to, say, Changi Airport Terminal 3
x.Router.supported_route_types # ['walk', 'drive', 'cycle', 'pt']
changi_airport = x.search("CHANGI AIRPORT TERMINAL 3")['results'][0]
x.Router.route_from_postal(gh['POSTAL'], changi_airport['POSTAL'], route_type='drive')
```

## References
1. OneMap API Documentation [here](https://docs.onemap.sg/)
1. OneMap API Account Registration [here](https://developers.onemap.sg/signup/)
1. `Poetry` used to package and publish on `pypi` [here](https://python-poetry.org/)


## Details

> **Client**:
>
>   Main class that encapsulates all classes defined in other modules.
        `Client` itself is a subclass of `OneMap`, but also has attributes `Router`, `PlanningAreas`, `Population`, and `Themes`.

> **base.OneMap**
> 
>    Provides basic functionality such as address search, coordinate conversion, and authentication.

> **routing.Router**
>
>    Provides functionality to query routes between 2 points.
>    Currently supports `(lat,lng)->(lat,lng)` or `postal->postal`

> **planning_areas.PlanningAreas**
>
>   Provides functionality to retrieve planning areas, including geospatial boundaries.

> **population.Population**
>
>    Handles all population-related queries, including education level, economic status, work income, marital status etc.
>    Use `Population.available_data_types` to see available data types
>   
>    For a full list of data provided by OneMap, you can refer to their documentation.

> **themes.Themes**
>
>    Thematic information from various agencies in Singapore.