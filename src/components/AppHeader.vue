<template>
	<div>
		<v-navigation-drawer absolute temporary v-model="drawer" class="hidden-md-and-up">
			<v-list>
				<v-list-tile v-for="(item, i) in menuItems" flat :key="'A' + i" :to="item.route">
					<v-list-tile-action>
						<v-icon v-html="item.icon"></v-icon>
					</v-list-tile-action>
					<v-list-tile-content>
						<v-list-tile-title v-text="item.title"></v-list-tile-title>
					</v-list-tile-content>
				</v-list-tile>
			</v-list>
		</v-navigation-drawer>
		<v-toolbar app dark class="primary">
			<v-toolbar-side-icon v-on:click.stop="drawer = !drawer" class="hidden-md-and-up"></v-toolbar-side-icon>
			<router-link :to="'/'" tag="span" style="cursor:pointer">
				<v-toolbar-title v-text="'Something About Books'"></v-toolbar-title>
			</router-link>
			<v-spacer></v-spacer>
			<v-toolbar-items class="hidden-sm-and-down">
				<v-btn v-for="(item, i) in menuItems" flat :key="'B' + i" :to="item.route">
					<v-icon left v-html="item.icon"></v-icon>
					{{item.title}}
				</v-btn>
			</v-toolbar-items>

		</v-toolbar>	
	</div>
</template>

<script>
export default {

  name: 'AppHeader',

  data () {
    return {
    	drawer: false
    }
  },

  computed:{
    isUserAuth(){
      return this.$store.getters.isUserAuth
    },
  	menuItems(){
  		return this.isUserAuth ? 
      [
  			{
  				icon: "visibility",
  				title: "Читать",
  				route: "/books",
  			},
  			{
  				icon: "extension",
  				title: "Учить слова",
  				route: "/words",
  			},
  			{
  				icon: "account_circle",
  				title: "Мой кабинет",
  				route: "/profile",
  			},
  			{
  				icon: "exit_to_app",
  				title: "Выйти",
  				route: "/logout",
  			}
  		] : 

      [
        {
          icon: "visibility",
          title: "Читать",
          route: "/books",
        },
        {
          icon: "extension",
          title: "Учить слова",
          route: "/words",
        },
        {
          icon: "input",
          title: "Войти",
          route: "/signin",
        },
        {
          icon: "lock_open",
          title: "Зарегистрироваться",
          route: "/signup",
        }
      ]
  	}
  }
}
</script>

<style lang="css" scoped>
</style>