<template>
    <div>
      <TransitionRoot as="template" :show="sidebarOpen">
        <Dialog class="relative z-50 lg:hidden" @close="sidebarOpen = false">
          <TransitionChild as="template" enter="transition-opacity ease-linear duration-300" enter-from="opacity-0" enter-to="opacity-100" leave="transition-opacity ease-linear duration-300" leave-from="opacity-100" leave-to="opacity-0">
            <div class="fixed inset-0 bg-gray-900/80" />
          </TransitionChild>
  
          <div class="fixed inset-0 flex">
            <TransitionChild as="template" enter="transition ease-in-out duration-300 transform" enter-from="-translate-x-full" enter-to="translate-x-0" leave="transition ease-in-out duration-300 transform" leave-from="translate-x-0" leave-to="-translate-x-full">
              <DialogPanel class="relative mr-16 flex w-full max-w-xs flex-1">
                <TransitionChild as="template" enter="ease-in-out duration-300" enter-from="opacity-0" enter-to="opacity-100" leave="ease-in-out duration-300" leave-from="opacity-100" leave-to="opacity-0">
                  <div class="absolute left-full top-0 flex w-16 justify-center pt-5">
                    <button type="button" class="-m-2.5 p-2.5" @click="sidebarOpen = false">
                      <span class="sr-only">Close sidebar</span>
                      <XMarkIcon class="h-6 w-6 text-white" aria-hidden="true" />
                    </button>
                  </div>
                </TransitionChild>
                <!-- Sidebar component, swap this element with another sidebar if you like -->
                <div class="flex grow flex-col gap-y-5 overflow-y-auto bg-purple-600 px-6 pb-4">
                  <div class="flex h-16 shrink-0 items-center">
                    <Logo />
                  </div>
                  <nav class="flex flex-1 flex-col">
                    <ul role="list" class="flex flex-1 flex-col gap-y-7">
                      <li>
                        <ul role="list" class="-mx-2 space-y-1">
                          <li v-for="item in navigation" :key="item.name">
                            <NuxtLink :href="item.href" :class="[isCurrentPage(item.href) ? 'bg-purple-700 text-white' : 'text-purple-200 hover:bg-purple-700 hover:text-white', 'group flex gap-x-3 rounded-md p-2 text-sm font-semibold leading-6']">
                              <Icon size="20" :name="item.icon" />
                              {{ item.name }}
                            </NuxtLink>
                          </li>
                        </ul>
                      </li>
                      <li>
                        <div class="text-xs font-semibold leading-6 text-purple-200">Your teams</div>
                        <ul role="list" class="-mx-2 mt-2 space-y-1">
                          <li v-for="team in teams" :key="team.name">
                            <NuxtLink :href="team.href" :class="[isCurrentPage(team.href) ? 'bg-purple-700 text-white' : 'text-purple-200 hover:bg-purple-700 hover:text-white', 'group flex gap-x-3 rounded-md p-2 text-sm font-semibold leading-6']">
                              <span class="flex h-6 w-6 shrink-0 items-center justify-center rounded-lg border border-purple-400 bg-purple-500 text-[0.625rem] font-medium text-white">{{ team.initial }}</span>
                              <span class="truncate">{{ team.name }}</span>
                            </NuxtLink>
                          </li>
                        </ul>
                      </li>
                      <li class="mt-auto">
                        <NuxtLink :href="settingsHref" :class="[isCurrentPage(settingsHref) ? 'bg-purple-700 text-white' : 'text-purple-200 hover:bg-purple-700 hover:text-white', 'group -mx-2 flex gap-x-3 rounded-md p-2 text-sm font-semibold leading-6']">
                          <Cog6ToothIcon class="h-6 w-6 shrink-0 text-purple-200 group-hover:text-white" aria-hidden="true" />
                          Settings
                        </NuxtLink>
                      </li>
                    </ul>
                  </nav>
                </div>
              </DialogPanel>
            </TransitionChild>
          </div>
        </Dialog>
      </TransitionRoot>
  
      <!-- Static sidebar for desktop -->
      <div class="hidden lg:fixed lg:inset-y-0 lg:z-50 lg:flex lg:w-72 lg:flex-col">
        <!-- Sidebar component, swap this element with another sidebar if you like -->
        <div class="flex grow flex-col gap-y-5 overflow-y-auto bg-purple-600 px-6 pb-4">
          <div class="flex h-16 shrink-0 items-center">
            <Logo />
          </div>
          <nav class="flex flex-1 flex-col">
            <ul role="list" class="flex flex-1 flex-col gap-y-7">
              <li>
                <ul role="list" class="-mx-2 space-y-1">
                        <li v-for="(item,index) in navigation" :key="index">
                            <NuxtLink :href="item.href" :class="[isCurrentPage(item.href) ? 'bg-purple-700 text-white' : 'text-purple-200 hover:bg-purple-700 hover:text-white', 'group flex gap-x-3 rounded-md p-2 text-sm font-semibold leading-6']">
                                <Icon size="25" :name="item.icon" />
                                {{ item.name }}
                            </NuxtLink>
                        </li>
                </ul>
              </li>
              <li>
                <div class="text-xs font-semibold leading-6 text-purple-200">Your teams</div>
                <ul role="list" class="-mx-2 mt-2 space-y-1">
                  <li v-for="team in teams" :key="team.name">
                    <NuxtLink :href="team.href" :class="[isCurrentPage(team.href) ? 'bg-purple-700 text-white' : 'text-purple-200 hover:bg-purple-700 hover:text-white', 'group flex gap-x-3 rounded-md p-2 text-sm font-semibold leading-6']">
                      <span class="flex h-6 w-6 shrink-0 items-center justify-center rounded-lg border border-purple-400 bg-purple-500 text-[0.625rem] font-medium text-white">{{ team.initial }}</span>
                      <span class="truncate">{{ team.name }}</span>
                    </NuxtLink>
                  </li>
                </ul>
              </li>
              <li class="mt-auto">
                <NuxtLink :href="settingsHref" :class="[isCurrentPage(settingsHref) ? 'bg-purple-700 text-white' : 'text-purple-200 hover:bg-purple-700 hover:text-white' ,'group -mx-2 flex gap-x-3 rounded-md p-2 text-sm font-semibold leading-6']">
                  <Cog6ToothIcon class="h-6 w-6 shrink-0 text-purple-200 group-hover:text-white" aria-hidden="true" />
                  Settings
                </NuxtLink>
              </li>
            </ul>
          </nav>
        </div>
      </div>
  
      <div class="lg:pl-72">
        <div class="sticky top-0 z-40 flex h-16 shrink-0 items-center gap-x-4 border-b border-gray-200 bg-white px-4 shadow-sm sm:gap-x-6 sm:px-6 lg:px-8">
          <button type="button" class="-m-2.5 p-2.5 text-gray-700 lg:hidden" @click="sidebarOpen = true">
            <span class="sr-only">Open sidebar</span>
            <Bars3Icon class="h-6 w-6" aria-hidden="true" />
          </button>
  
          <!-- Separator -->
          <div class="h-6 w-px bg-gray-900/10 lg:hidden" aria-hidden="true" />
  
          <div class="flex flex-1 gap-x-4 self-stretch lg:gap-x-6">
            <form class="relative flex flex-1" action="#" method="GET">
              <label for="search-field" class="sr-only">Search</label>
              <MagnifyingGlassIcon class="pointer-events-none absolute inset-y-0 left-2 h-full w-5 text-gray-400" aria-hidden="true" />
              <input id="search-field" class="block h-full w-full border-0 py-0 pl-8 pr-3 text-gray-900 placeholder:text-gray-400 focus:ring-0 sm:text-sm" placeholder="Search..." type="search" name="search" />
            </form>
            <div class="flex items-center gap-x-4 lg:gap-x-6">
              <button type="button" class="-m-2.5 p-2.5 text-gray-400 hover:text-gray-500">
                <span class="sr-only">View notifications</span>
                <BellIcon class="h-6 w-6" aria-hidden="true" />
              </button>
  
              <!-- Separator -->
              <div class="hidden lg:block lg:h-6 lg:w-px lg:bg-gray-900/10" aria-hidden="true" />
  
              <!-- Profile dropdown -->
              <Menu as="div" class="relative">
                <MenuButton class="-m-1.5 flex items-center p-1.5">
                  <span class="sr-only">Open user menu</span>
                  <img class="h-8 w-8 rounded-full bg-gray-50" src="@/assets/profile-picture/ehsanmoradi.jpg" alt="" />
                  <span class="hidden lg:flex lg:items-center">
                    <span class="ml-4 text-sm font-semibold leading-6 text-gray-900" aria-hidden="true">Ehsan Moradi</span>
                    <ChevronDownIcon class="ml-2 h-5 w-5 text-gray-400" aria-hidden="true" />
                  </span>
                </MenuButton>
                <transition enter-active-class="transition ease-out duration-100" enter-from-class="transform opacity-0 scale-95" enter-to-class="transform opacity-100 scale-100" leave-active-class="transition ease-in duration-75" leave-from-class="transform opacity-100 scale-100" leave-to-class="transform opacity-0 scale-95">
                  <MenuItems class="absolute right-0 z-10 mt-2.5 w-32 origin-top-right rounded-md bg-white py-2 shadow-lg ring-1 ring-gray-900/5 focus:outline-none">
                    <MenuItem v-for="item in userNavigation" :key="item.name" v-slot="{ active }">
                        <NuxtLink :href="item.href" :class="[active ? 'bg-gray-50' : '', 'flex justify-between items-center px-3 py-1 text-sm leading-6 text-gray-900']">
                            {{ item.name }}
                            <Icon :name="item.icon" size="20" />
                        </NuxtLink>
                    </MenuItem>
                  </MenuItems>
                </transition>
              </Menu>
            </div>
          </div>
        </div>
  
        <main class="py-10">
          <div class="px-4 sm:px-6 lg:px-8">
            
             <slot />

          </div>
        </main>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue'
  import {
    Dialog,
    DialogPanel,
    Menu,
    MenuButton,
    MenuItem,
    MenuItems,
    TransitionChild,
    TransitionRoot,
  } from '@headlessui/vue'
  import {
    Bars3Icon,
    BellIcon,
    Cog6ToothIcon,
    XMarkIcon,
  } from '@heroicons/vue/24/outline'
  import { ChevronDownIcon, MagnifyingGlassIcon } from '@heroicons/vue/20/solid'
  import { useRoute } from 'vue-router'

  const navigation = [
    { name: 'Home', href: '/dashboard', icon: "iconamoon:home-bold"},
    { name: 'Projects', href: '/dashboard/projects', icon: "ant-design:project-outlined"},
    { name: 'Teams', href: '/dashboard/teams', icon: "ant-design:team-outlined"},
    { name: 'Tasks', href: '/dashboard/tasks', icon: "la:tasks"},
    { name: 'Board', href: '/dashboard/board', icon: "tabler:layout-kanban"},
    { name: 'Calendar', href: '/dashboard/calendar', icon: "ion:calendar-outline"},
    { name: 'Analytics', href: '/dashboard/analytics', icon: 'material-symbols:analytics-outline-rounded'},
    { name: 'Sprints', href: '/dashboard/sprints', icon: "fluent:arrow-sprint-16-filled"},
    { name: 'Account', href: '/dashboard/account', icon: "codicon:account"},    
    { name: 'Market', href: '/dashboard/market', icon: "icon-park-outline:weixin-market"},    
  ]
  const teams = [
    { id: 1, name: 'Savalan', href: '/team/savalan', initial: 'S'},
    { id: 2, name: 'Matin inc.', href: '/team/matin-inc', initial: 'M'},
    { id: 3, name: 'Savalan Academy', href: '/team/savalan-academy', initial: 'SA'},
  ]
  const userNavigation = [
    { name: 'Profile', href: '/dashboard/account',icon: "iconamoon:profile" },
    { name: 'Sign out', href: '/auth/login',icon: "gridicons:sign-out" },
  ]

  const route = useRoute();

    const isCurrentPage = (href) => {
    return route.path === href;
    };
  
  const sidebarOpen = ref(false)
  const settingsHref = ref('/dashboard/settings')
  </script>