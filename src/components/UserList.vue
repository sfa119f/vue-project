<template>
  <fragment>
    <td class="table__col__id">{{ user.id }}</td>
    <td class="table__col__fname">{{ user.first_name }}</td>
    <td class="table__col__lname">{{ user.last_name }}</td>
    <td class="table__col__email">{{ user.email }}</td>
  </fragment>
</template>

<script>
  export default {
    name: 'UsersList',
    props: ['user']
  }
</script>