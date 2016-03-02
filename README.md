# learn-relay

## What

A data fetching library by Facebook for use with GraphQL and React. [Thinking in Relay](https://facebook.github.io/relay/docs/thinking-in-relay.html#content)

### Why?

**Advantages**

* Query optimisation and Caching data from requests
  - A component that displays a preview of a newspaper article might request the title and an image, and another component that displays the full article requests all the data for the article including the title and image - Relay doesn't refetch the title and image properties as it is stored in a local cache.
  - helps to avoid errors when two components have implicit dependencies i.e. one component relies on data that is fetched from another component. With Relay both components can delcare their data needs and Relay optimises the query to ensure the same data is not fetched twice.
* Declarative  
  * Applies the same principles as React
  * makes continuous scrolling easy!
    - relayVariables - can be set like setState using setVariables - allows easy toggling of views etc to alter the query based on a user interaction. Relay will detect which part of the query has changed and re-fetch the data as needed.
    - a prop called 'relay' is added to any component that has a relay container. The variables can be accessesed using 'relay.variables' and methods using 'relay.variables.setVariables'. For unit testing components the whole relay object can be mocked.
* Co location of views and queries
  - data needs of the component are declared alongside the component code
  - data is passed directly as props to the React component that needs it rather than having to pass props down multiple view layers
* Not as much set up if you have a GraphQL implementation already!
  * Can also keep the graphql implementation separate and expose an API endpoint - using the introspection API the GraphQL schema can be retrieved for querying againstgithub

**Disadvantages**

* Needs GraphQL implementation although there is an npm module ([relay-local-schema](https://github.com/relay-tools/relay-local-schema) to allow Relay to be used without a GraphQL server
* Needs client and server side state
  * all client side data needs to be kept consistent with Relay’s store

### How?

* uses Higher Order (RelayContainers) that wrap regular React UI component. The HOC will execute its queries and then render the child UI component, passing the query data in as props.
* Relay Routes to define entry points into the query
* Node Interfaces for mapping


#### Set up

* GraphQL server or api endpoint
* babel-relay-plugin
* Optional: react-router-relay

## Resources

* [Relay Tutorial](https://medium.com/@clayallsopp/relay-101-building-a-hacker-news-client-bb8b2bdc76e6#.1lpesgmth)
* [Relay Advantages](http://red-badger.com/blog/2015/08/28/give-it-5-days-facebook-relay-and-graphql/)
* [Relay and Routing using react-router](https://medium.com/@cpojer/relay-and-routing-36b5439bad9#.br822rom9)
* [relay-tools](https://github.com/relay-tools)
