<template>
  <v-navigation-drawer
    v-model="drawer"
    location="left"
    color="green"
    :rail="rail"
    @click="rail = false"
  >
    <v-list>
      <v-list-item
        class="py-4"
        prepend-avatar="/avatar.svg"
        title="User"
        subtitle="user@user.com"
      >
        <template v-slot:append>
          <v-btn
            icon="mdi-chevron-left"
            variant="text"
            @click.stop="rail = !rail"
          ></v-btn>
        </template>
      </v-list-item>
    </v-list>
    <v-divider></v-divider>

    <v-list>
      <v-list-item
        v-for="(item, i) in drawerItems"
        :key="i"
        :value="item"
        :to="item.route"
        rounded="xl"
      >
        <template v-slot:prepend>
          <v-icon :icon="item.icon"></v-icon>
        </template>

        <v-list-item-title v-text="item.title"></v-list-item-title>
      </v-list-item>
      <v-divider> </v-divider>
      <v-list-item prepend-icon="mdi-logout"
        ><v-list-item-title>Signout</v-list-item-title></v-list-item
      >
    </v-list>
  </v-navigation-drawer>

  <v-navigation-drawer
    v-model="rightDrawer"
    location="right"
    color="green"
    :rail="rightRail"
    @click="rightRail = false"
    temporary
  >
    <v-list>
      <v-list-item
        class="py-4"
        append-avatar="/avatar.svg"
        title="User"
        subtitle="user@user.com"
      >
        <template v-slot:prepend>
          <v-btn
            :icon="rightRail ? 'mdi-chevron-left' : 'mdi-chevron-right'"
            variant="text"
            @click.stop="rightRail = !rightRail"
          ></v-btn>
        </template>
      </v-list-item>
    </v-list>
    <v-divider></v-divider>

    <v-list>
      <v-list-item
        v-for="(item, i) in drawerItems"
        :key="i"
        :value="item"
        :to="item.route"
        rounded="xl"
      >
        <template v-slot:prepend>
          <v-icon :icon="item.icon"></v-icon>
        </template>

        <v-list-item-title v-text="item.title"></v-list-item-title>
      </v-list-item>
      <v-divider> </v-divider>
      <v-list-item prepend-icon="mdi-logout"
        ><v-list-item-title>Signout</v-list-item-title></v-list-item
      >
    </v-list>
  </v-navigation-drawer>

  <v-app-bar class="d-flex justify-center" color="white">
    <template v-slot:prepend>
      <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>
    </template>
    <v-app-bar-title>
      <v-img width="50" src="logo.svg" size="80" rounded="0"></v-img>
    </v-app-bar-title>

    <v-menu>
      <template v-slot:activator="{ props }">
        <v-btn icon v-bind="props"> <v-icon>mdi-magnify</v-icon></v-btn>
      </template>
    </v-menu>

    <v-menu>
      <template v-slot:activator="{ props }">
        <v-btn icon v-bind="props">
          <v-icon>mdi-bell-outline</v-icon>
        </v-btn>
      </template>
      <v-list><v-list-item>No Notifications</v-list-item></v-list>
    </v-menu>

    <v-menu>
      <template v-slot:activator="{ props }">
        <v-btn icon v-bind="props">
          <v-icon>mdi-account-circle-outline</v-icon>
        </v-btn>
      </template>
      <v-card min-width="300">
        <v-card-text>
          <div class="mx-auto text-center">
            <v-avatar image="/avatar.svg" size="80"></v-avatar>

            <h3 class="mt-3">Hi, User!</h3>
            <p class="text-caption mt-1">user@user.com</p>

            <v-divider class="my-3"></v-divider>
            <v-row
              ><v-col cols="6">
                <v-btn
                  variant="text"
                  rounded
                  class="text-capitalize"
                  prepend-icon="mdi-account-outline"
                  to="/profile"
                >
                  My Profile
                </v-btn></v-col
              ><v-col cols="6"
                ><v-btn
                  class="text-capitalize"
                  color="primary"
                  prepend-icon="mdi-logout"
                  variant="text"
                  rounded
                >
                  Signout
                </v-btn></v-col
              ></v-row
            >
          </div>
        </v-card-text>
      </v-card>
    </v-menu>

    <v-menu>
      <template v-slot:activator="{ props }">
        <v-btn icon v-bind="props" @click="rightDrawer = !rightDrawer">
          <v-icon>mdi-menu-open</v-icon></v-btn
        >
      </template>
    </v-menu>
  </v-app-bar>
</template>
<script setup>
import { ref, onMounted } from "vue";

const drawer = ref(null);
const rail = ref(false);

const rightDrawer = ref(null);
const rightRail = ref(false);

const drawerItems = ref([
  {
    title: "Dashboard",
    route: "/",
    icon: "mdi-view-dashboard-outline",
  },
  {
    title: "Profile",
    route: "/profile",
    icon: "mdi-account-settings-outline",
  },
  {
    title: "Settings",
    route: "/settings",
    icon: "mdi-cog-outline",
  },
]);
</script>
