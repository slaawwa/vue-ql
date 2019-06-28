<template lang="pug">
  .user
    h1 Get All Errors
    //- Apollo watched Graphql query
    ApolloQuery(
        :query="require('../graphql/errors.gql')"
        :variables='{}'
        fetchPolicy='network-only'
      )
      template(slot-scope='{ result: { loading, error, data } }')
        //- Loading
        .loading.apollo(v-if='loading') Loading...
        //- Error
        .error.apollo(v-else-if='error') An error occured
        //- Result
        .result.apollo(v-else-if='data', v-for='err in data.errors', :key='err')
          strong {{ err.split(' - ')[0] }}
          |           -
          em {{ err.split(' - ')[1] }}
          hr
        //- No result
        .no-result.apollo(v-else='') No result :(

</template>
