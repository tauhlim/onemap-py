Python Wrapper for SLA's OneMap API
========================================

Introduction
-------------
This package provides a simple way to query data using the OneMap API in Python.

OneMap arranges its API endpoints by groups, and this package is organized to reflect that grouping.

onemap-py allows you to make queries corresponding to the OneMap API, and returns the results to you in a standard
python `dict`.

Details
----------------
Client
    Main class that encapsulates all classes defined in other modules.
    `Client` itself is a subclass of `OneMap`, but also has attributes `Router`, `PlanningAreas`, `Population`, and `Themes`.

base.OneMap
    Provides basic functionality such as address search, coordinate conversion, and authentication.

routing.Router
    Provides functionality to query routes between 2 points.

    Currently supports `(lat,lng)->(lat,lng)` or `postal->postal`

planning_areas.PlanningAreas
   Provides functionality to retrieve planning areas, including geospatial boundaries.

population.Population
    Handles all population-related queries, including education level, economic status, work income, marital status etc.

    For a full list of data provided by OneMap, you can refer to their documentation.

themes.Themes
    Thematic information from various agencies in Singapore.