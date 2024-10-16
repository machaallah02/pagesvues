<template>
    <div class="w-full mx-auto p-4  h-screen">
        <Disclosure as="nav" class="bg-white border-b border-gray-200" v-slot="{ open }">
            <div class="mx-auto max-w-7xl px-4 sm:px-6 lg:px-8">
                <div class="flex h-16 items-center justify-between">
                    <div class="flex items-center">
                        <div class="flex-shrink-0">
                            <img class="h-8 w-8" src="AFROSTD.png" alt="Your Company" />
                        </div>
                        <div class="hidden md:block">
                            <div class="ml-10 flex items-baseline space-x-4 ">
                                <a href="#"
                                    class="relative py-2 px-8 text-black text-base font-bold nded-full overflow-hidden bg-white rounded-full transition-all duration-400 ease-in-out shadow-md hover:scale-105 hover:text-white hover:shadow-lg active:scale-90 before:absolute before:top-0 before:-left-full before:w-full before:h-full before:bg-gradient-to-r before:from-blue-500 before:to-blue-300 before:transition-all before:duration-500 before:ease-in-out before:z-[-1] before:rounded-full hover:before:left-0">
                                    HOVER ME!
                                </a>
                                <a v-for="item in navigation" :key="item.name" :href="item.href"
                                    :class="[item.current ? 'bg-gray-900 text-gray-900' : 'text-gray-500 hover:bg-gray-700 hover:text-white', 'rounded-md px-3 py-2 text-sm font-medium']"
                                    :aria-current="item.current ? 'page' : undefined">{{ item.name }}</a>
                            </div>
                        </div>
                    </div>
                    <div class="hidden md:block">
                        <div class="ml-4 flex items-center md:ml-6">
                            <button type="button"
                                class="relative rounded-full bg-gray-800 p-1 text-gray-400 hover:text-white focus:outline-none focus:ring-2 focus:ring-white focus:ring-offset-2 focus:ring-offset-gray-800">
                                <span class="absolute -inset-1.5" />
                                <span class="sr-only">View notifications</span>
                                <BellIcon class="h-6 w-6" aria-hidden="true" />
                            </button>

                            <!-- Profile dropdown -->
                            <Menu as="div" class="relative ml-3">
                                <div>
                                    <MenuButton
                                        class="relative flex max-w-xs items-center rounded-full bg-gray-800 text-sm focus:outline-none focus:ring-2 focus:ring-white focus:ring-offset-2 focus:ring-offset-gray-800">
                                        <span class="absolute -inset-1.5" />
                                        <span class="sr-only">Open user menu</span>
                                        <img class="h-8 w-8 rounded-full" :src="user.imageUrl" alt="" />
                                    </MenuButton>
                                </div>
                                <transition enter-active-class="transition ease-out duration-100"
                                    enter-from-class="transform opacity-0 scale-95"
                                    enter-to-class="transform opacity-100 scale-100"
                                    leave-active-class="transition ease-in duration-75"
                                    leave-from-class="transform opacity-100 scale-100"
                                    leave-to-class="transform opacity-0 scale-95">
                                    <MenuItems
                                        class="absolute right-0 z-10 mt-2 w-48 origin-top-right rounded-md bg-white py-1 shadow-lg ring-1 ring-black ring-opacity-5 focus:outline-none">
                                        <MenuItem v-for="item in userNavigation" :key="item.name" v-slot="{ active }">
                                        <a :href="item.href"
                                            :class="[active ? 'bg-gray-100' : '', 'block px-4 py-2 text-sm text-gray-700']">{{
                                                item.name }}</a>
                                        </MenuItem>
                                    </MenuItems>
                                </transition>
                            </Menu>
                        </div>
                    </div>
                    <div class="-mr-2 flex md:hidden">
                        <!-- Mobile menu button -->
                        <DisclosureButton
                            class="relative inline-flex items-center justify-center rounded-md bg-gray-800 p-2 text-gray-400 hover:bg-gray-700 hover:text-white focus:outline-none focus:ring-2 focus:ring-white focus:ring-offset-2 focus:ring-offset-gray-800">
                            <span class="absolute -inset-0.5" />
                            <span class="sr-only">Open main menu</span>
                            <Bars3Icon v-if="!open" class="block h-6 w-6" aria-hidden="true" />
                            <XMarkIcon v-else class="block h-6 w-6" aria-hidden="true" />
                        </DisclosureButton>
                    </div>
                </div>
            </div>

            <DisclosurePanel class="md:hidden">
                <div class="space-y-1 px-2 pb-3 pt-2 sm:px-3">
                    <DisclosureButton v-for="item in navigation" :key="item.name" as="a" :href="item.href"
                        :class="[item.current ? 'bg-gray-900 text-white' : 'text-gray-300 hover:bg-gray-700 hover:text-white', 'block rounded-md px-3 py-2 text-base font-medium']"
                        :aria-current="item.current ? 'page' : undefined">{{ item.name }}</DisclosureButton>
                </div>
                <div class="border-t border-gray-700 pb-3 pt-4">
                    <div class="flex items-center px-5">
                        <div class="flex-shrink-0">
                            <img class="h-10 w-10 rounded-full" :src="user.imageUrl" alt="" />
                        </div>
                        <div class="ml-3">
                            <div class="text-base font-medium leading-none text-white">{{ user.name }}</div>
                            <div class="text-sm font-medium leading-none text-gray-400">{{ user.email }}</div>
                        </div>
                        <button type="button"
                            class="relative ml-auto flex-shrink-0 rounded-full bg-gray-800 p-1 text-gray-400 hover:text-white focus:outline-none focus:ring-2 focus:ring-white focus:ring-offset-2 focus:ring-offset-gray-800">
                            <span class="absolute -inset-1.5" />
                            <span class="sr-only">View notifications</span>
                            <BellIcon class="h-6 w-6" aria-hidden="true" />
                        </button>
                    </div>
                    <div class="mt-3 space-y-1 px-2">
                        <DisclosureButton v-for="item in userNavigation" :key="item.name" as="a" :href="item.href"
                            class="block rounded-md px-3 py-2 text-base font-medium text-gray-400 hover:bg-gray-700 hover:text-white">
                            {{ item.name }}</DisclosureButton>
                    </div>
                </div>
            </DisclosurePanel>
        </Disclosure>
        <main>
            <div class="mx-auto max-w-7xl py-6 sm:px-6 lg:px-8">
                <div class="h-1/2 flex items-center justify-between">
                    <div class="w-1/2 space-y-4 p-2">
                        <!-- Affichage du texte dynamique -->
                        <h1 id="welcome" class="text-sm sm:text-2xl md:text-md lg:text-4xl font-bold text-gray-900">
                            {{ currentMessage }}
                        </h1>
                        <p class="text-sm text-gray-700 sm:text-sm md:text-lg lg:text-lg">
                            Découvrez une large gamme de produits de qualité à des prix compétitifs. Profitez de nos
                            offres spéciales et trouvez ce dont vous avez besoin.
                        </p>
                        <a href="#"
                            class="inline-block bg-indigo-600 text-white px-6 py-2 rounded-md text-sm font-medium hover:bg-indigo-700 sm:text-sm md:text-lg">
                            Parcourir nos produits
                        </a>
                    </div>
                    <div class="w-1/2 flex justify-end">
                        <img src="AFROSTD.png" alt="AFROSTD" class="w-full border rounded-3xl">
                    </div>
                </div>
            </div>

            <div class="mx-auto py-6 sm:px-6 lg:px-8">
            <div class="flex animate-scroll whitespace-nowrap ">
                <img src="AFROSTD.png" alt="logo1">
                <img src="AFROSTD.png" alt="logo2">
                <img src="AFROSTD.png" alt="logo3">
                <img src="AFROSTD.png" alt="logo4">
                <img src="AFROSTD.png" alt="logo5">
                <img src="AFROSTD.png" alt="logo6">
                <img src="AFROSTD.png" alt="logo7">
                <img src="AFROSTD.png" alt="logo8">
                <img src="AFROSTD.png" alt="logo9">
                <img src="AFROSTD.png" alt="logo10">
                <img src="AFROSTD.png" alt="logo11">
                <img src="AFROSTD.png" alt="logo12">
                <img src="AFROSTD.png" alt="logo13">
                <img src="AFROSTD.png" alt="logo14">
                <img src="AFROSTD.png" alt="logo15">
            </div>
        </div>
            <div class="flex justify-center items-center gap-16 mt-10 mb-10">
                <div
                    class="group flex flex-col justify-start items-start gap-2 w-96 h-56 duration-500 relative rounded-lg p-4 bg-purple-500 hover:-translate-y-2 hover:shadow-xl shadow-purple-400">
                    <div class="absolute duration-700 shadow-md group-hover:-translate-y-4 group-hover:-translate-x-4 -bottom-10 -right-10 w-1/2 h-1/2 rounded-lg bg-purple-400"
                        alt="image here"></div>
                    <div class="">
                        <h2 class="text-2xl font-bold mb-2 text-white">Elegant Card</h2>
                        <p class="text-gray-200 line-clamp-3">
                            Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aenean convallis
                            magna quis lectus fermentum, quis scelerisque orci pellentesque. Duis id
                            porta justo. Sed ac enim id justo tincidunt hendrerit id ac lectus.
                            Pellentesque maximus posuere tortor vitae consequat.
                        </p>
                    </div>
                    <button class="hover:bg-purple-400 bg-purple-600 text-white mt-6 rounded p-2 px-6">
                        Explore
                    </button>
                </div>
            </div>
            <div class="flex justify-center items-center gap-16 mt-10 mb-10">
                <div
                    class="max-w-sm p-4 border border-gray-200 rounded shadow animate-pulse md:p-6 dark:border-gray-400">
                    <div class="flex items-center justify-center h-48 mb-4 bg-gray-300 rounded dark:bg-gray-400">
                        <img src="AFROSTD.png" alt="">
                    </div>
                    <div class="h-2.5 bg-gray-200 rounded-full dark:bg-gray-400 w-48 mb-4"></div>
                    <div class="h-2 bg-gray-200 rounded-full dark:bg-gray-400 mb-2.5"></div>
                    <div class="h-2 bg-gray-200 rounded-full dark:bg-gray-400 mb-2.5"></div>
                    <div class="h-2 bg-gray-200 rounded-full dark:bg-gray-400"></div>
                    <div class="flex items-center mt-4">
                        <svg viewBox="0 0 20 20" fill="currentColor" xmlns="http://www.w3.org/2000/svg"
                            aria-hidden="true" class="w-10 h-10 me-3 text-gray-200 dark:text-gray-400">
                            <path
                                d="M10 0a10 10 0 1 0 10 10A10.011 10.011 0 0 0 10 0Zm0 5a3 3 0 1 1 0 6 3 3 0 0 1 0-6Zm0 13a8.949 8.949 0 0 1-4.951-1.488A3.987 3.987 0 0 1 9 13h2a3.987 3.987 0 0 1 3.951 3.512A8.949 8.949 0 0 1 10 18Z">
                            </path>
                        </svg>
                        <div>
                            <div class="h-2.5 bg-gray-200 rounded-full dark:bg-gray-400 w-32 mb-2"></div>
                            <div class="w-48 h-2 bg-gray-200 rounded-full dark:bg-gray-400"></div>
                        </div>
                    </div>
                    <span class="sr-only">Loading...</span>
                </div>

            </div>

            <div class="mx-auto py-6 sm:px-6 lg:px-8">
                <h2 class="text-3xl font-bold text-center mb-8">Nos Services</h2>
                <div class="overflow-hidden relative">
                    <div class="flex animate-scroll whitespace-nowrap">
                        <div
                            class="bg-white w-64 lg:w-80 h-auto rounded-lg shadow-lg p-4 mx-2 flex-none transform transition-transform duration-300 hover:scale-105">
                            <div class="flex items-center">
                                <i class="fas fa-truck text-indigo-600 text-3xl mr-2"></i>
                                <h3 class="text-lg font-semibold">Livraison Rapide</h3>
                            </div>
                            <p class="text-gray-700 mt-1">Livraison express pour vos commandes.</p>
                            <a href="#"
                                class="mt-2 inline-block bg-indigo-600 text-white px-3 py-1 rounded-md hover:bg-indigo-700 transition-colors duration-200">En
                                savoir plus</a>
                        </div>
                        <!-- Carte 2 -->
                        <div
                            class="bg-white w-64 lg:w-80 h-auto rounded-lg shadow-lg p-4 mx-2 flex-none transform transition-transform duration-300 hover:scale-105">
                            <div class="flex items-center">
                                <i class="fas fa-credit-card text-indigo-600 text-3xl mr-2"></i>
                                <h3 class="text-lg font-semibold">Paiement Sécurisé</h3>
                            </div>
                            <p class="text-gray-700 mt-1">Options de paiement sécurisées.</p>
                            <a href="#"
                                class="mt-2 inline-block bg-indigo-600 text-white px-3 py-1 rounded-md hover:bg-indigo-700 transition-colors duration-200">En
                                savoir plus</a>
                        </div>
                        <!-- Carte 3 -->
                        <div
                            class="bg-white w-64 lg:w-80 h-auto rounded-lg shadow-lg p-4 mx-2 flex-none transform transition-transform duration-300 hover:scale-105">
                            <div class="flex items-center">
                                <i class="fas fa-undo text-indigo-600 text-3xl mr-2"></i>
                                <h3 class="text-lg font-semibold">Retours Faciles</h3>
                            </div>
                            <p class="text-gray-700 mt-1">Processus de retour sans tracas.</p>
                            <a href="#"
                                class="mt-2 inline-block bg-indigo-600 text-white px-3 py-1 rounded-md hover:bg-indigo-700 transition-colors duration-200">En
                                savoir plus</a>
                        </div>
                        <!-- Carte 4 -->
                        <div
                            class="bg-white w-64 lg:w-80 h-auto rounded-lg shadow-lg p-4 mx-2 flex-none transform transition-transform duration-300 hover:scale-105">
                            <div class="flex items-center">
                                <i class="fas fa-headset text-indigo-600 text-3xl mr-2"></i>
                                <h3 class="text-lg font-semibold">Support 24/7</h3>
                            </div>
                            <p class="text-gray-700 mt-1">Support disponible à toute heure.</p>
                            <a href="#"
                                class="mt-2 inline-block bg-indigo-600 text-white px-3 py-1 rounded-md hover:bg-indigo-700 transition-colors duration-200">En
                                savoir plus</a>
                        </div>
                        <!-- Carte 5 -->
                        <div
                            class="bg-white w-64 lg:w-80 h-auto rounded-lg shadow-lg p-4 mx-2 flex-none transform transition-transform duration-300 hover:scale-105">
                            <div class="flex items-center">
                                <i class="fas fa-gift text-indigo-600 text-3xl mr-2"></i>
                                <h3 class="text-lg font-semibold">Offres Spéciales</h3>
                            </div>
                            <p class="text-gray-700 mt-1">Découvrez nos promotions.</p>
                            <a href="#"
                                class="mt-2 inline-block bg-indigo-600 text-white px-3 py-1 rounded-md hover:bg-indigo-700 transition-colors duration-200">En
                                savoir plus</a>
                        </div>

                        <!-- Répétition pour l'effet de défilement infini -->
                        <div
                            class="bg-white rounded-lg shadow-lg lg:w-80 mx-2 flex-none transform transition-transform duration-300 hover:scale-105">
                            <div class="flex items-center">
                                <i class="fas fa-truck text-indigo-600 text-3xl mr-2"></i>
                                <h3 class="text-lg font-semibold">Livraison Rapide</h3>
                            </div>
                            <p class="text-gray-700 mt-1">Livraison express pour vos commandes.</p>
                            <a href="#"
                                class="mt-2 inline-block bg-indigo-600 text-white px-3 py-1 rounded-md hover:bg-indigo-700 transition-colors duration-200">En
                                savoir plus</a>
                        </div>

                        <div
                            class="bg-white rounded-lg shadow-lg lg:w-80 mx-2 flex-none transform transition-transform duration-300 hover:scale-105">
                            <div class="flex items-center">
                                <i class="fas fa-credit-card text-indigo-600 text-3xl mr-2"></i>
                                <h3 class="text-lg font-semibold">Paiement Sécurisé</h3>
                            </div>
                            <p class="text-gray-700 mt-1">Options de paiement sécurisées.</p>
                            <a href="#"
                                class="mt-2 inline-block bg-indigo-600 text-white px-3 py-1 rounded-md hover:bg-indigo-700 transition-colors duration-200">En
                                savoir plus</a>
                        </div>

                        <div
                            class="bg-white rounded-lg shadow-lg lg:w-80 mx-2 p-6 flex-none transform transition-transform duration-300 hover:scale-105">
                            <div class="flex items-center">
                                <i class="fas fa-undo text-indigo-600 text-3xl mr-2"></i>
                                <h3 class="text-lg font-semibold">Retours Faciles</h3>
                            </div>
                            <p class="text-gray-700 mt-1">Processus de retour sans tracas.</p>
                            <a href="#"
                                class="mt-2 inline-block bg-indigo-600 text-white px-3 py-1 rounded-md hover:bg-indigo-700 transition-colors duration-200">En
                                savoir plus</a>
                        </div>

                        <div
                            class="bg-white rounded-lg shadow-lg lg:w-80 mx-2 p-6 flex-none transform transition-transform duration-300 hover:scale-105">
                            <div class="flex items-center">
                                <i class="fas fa-headset text-indigo-600 text-3xl mr-2"></i>
                                <h3 class="text-lg font-semibold">Support 24/7</h3>
                            </div>
                            <p class="text-gray-700 mt-1">Support disponible à toute heure.</p>
                            <a href="#"
                                class="mt-2 inline-block bg-indigo-600 text-white px-3 py-1 rounded-md hover:bg-indigo-700 transition-colors duration-200">En
                                savoir plus</a>
                        </div>

                        <div
                            class="bg-white rounded-lg shadow-lg lg:w-80 mx-2 flex-none transform transition-transform duration-300 hover:scale-105">
                            <div class="flex items-center">
                                <i class="fas fa-gift text-indigo-600 text-3xl mr-2"></i>
                                <h3 class="text-lg font-semibold">Offres Spéciales</h3>
                            </div>
                            <p class="text-gray-700 mt-1">Découvrez nos promotions.</p>
                            <a href="#"
                                class="mt-2 inline-block bg-indigo-600 text-white px-3 py-1 rounded-md hover:bg-indigo-700 transition-colors duration-200">En
                                savoir plus</a>
                        </div>
                    </div>
                </div>
            </div>

            <div class="mx-auto py-6 sm:px-6 lg:px-8">
                <h2 class="text-3xl font-bold text-center mb-8">Nos Options</h2>
                <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-6 justify-items-center">

                    <!-- Card 1 -->
                    <div
                        class="bg-white rounded-lg shadow-lg w-64 h-64 flex flex-col justify-center items-center transform transition-transform duration-300 hover:scale-105">
                        <div class="text-red-600">
                            <i class="fas fa-shipping-fast text-6xl"></i>
                        </div>
                        <h3 class="text-lg font-semibold mt-4">Livraison Rapide</h3>
                        <p class="text-gray-700 mt-2 text-center px-4">Nous garantissons une livraison express pour vos
                            commandes.</p>
                    </div>

                    <!-- Card 2 -->
                    <div
                        class="bg-white rounded-lg shadow-lg w-64 h-64 flex flex-col justify-center items-center transform transition-transform duration-300 hover:scale-105">
                        <div class="text-blue-600">
                            <i class="fas fa-lock text-6xl"></i>
                        </div>
                        <h3 class="text-lg font-semibold mt-4">Paiement Sécurisé</h3>
                        <p class="text-gray-700 mt-2 text-center px-4">Profitez d'une sécurité optimale lors de vos
                            paiements.</p>
                    </div>

                    <!-- Card 3 -->
                    <div
                        class="bg-white rounded-lg shadow-lg w-64 h-64 flex flex-col justify-center items-center transform transition-transform duration-300 hover:scale-105">
                        <div class="text-green-600">
                            <i class="fas fa-undo text-6xl"></i>
                        </div>
                        <h3 class="text-lg font-semibold mt-4">Retours Faciles</h3>
                        <p class="text-gray-700 mt-2 text-center px-4">Un processus simple et rapide pour vos retours.
                        </p>
                    </div>

                </div>
            </div>

            <div>
                <h2 class="text-4xl font-bold text-center mb-12 text-indigo-700">Nos Tarifs</h2>
                <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-8 justify-items-center">

                    <!-- Card 1 - Forfait Basic -->
                    <div @click="openModal('Forfait Basic', 19)"
                        class="bg-gradient-to-r from-green-400 to-blue-500 rounded-2xl shadow-xl w-72 h-80 flex flex-col justify-between items-center p-6 transform transition-transform duration-300 hover:scale-105 cursor-pointer">
                        <div class="flex flex-col items-center text-center text-white">
                            <h3 class="text-2xl font-bold mb-3">Forfait Basic</h3>
                            <p class="text-5xl font-extrabold">$19</p>
                            <p class="text-base mt-2">Idéal pour un usage occasionnel.</p>
                        </div>
                    </div>

                    <!-- Card 2 - Forfait Pro -->
                    <div @click="openModal('Forfait Pro', 49)"
                        class="bg-gradient-to-r from-purple-400 to-pink-500 rounded-2xl shadow-xl w-72 h-80 flex flex-col justify-between items-center p-6 transform transition-transform duration-300 hover:scale-105 cursor-pointer">
                        <div class="flex flex-col items-center text-center text-white">
                            <h3 class="text-2xl font-bold mb-3">Forfait Pro</h3>
                            <p class="text-5xl font-extrabold">$49</p>
                            <p class="text-base mt-2">Idéal pour les professionnels.</p>
                        </div>
                    </div>

                    <!-- Card 3 - Forfait Premium -->
                    <div @click="openModal('Forfait Premium', 99)"
                        class="bg-gradient-to-r from-yellow-400 to-red-500 rounded-2xl shadow-xl w-72 h-80 flex flex-col justify-between items-center p-6 transform transition-transform duration-300 hover:scale-105 cursor-pointer">
                        <div class="flex flex-col items-center text-center text-white">
                            <h3 class="text-2xl font-bold mb-3">Forfait Premium</h3>
                            <p class="text-5xl font-extrabold">$99</p>
                            <p class="text-base mt-2">Idéal pour un usage intensif.</p>
                        </div>
                    </div>

                </div>

                <!-- Modal -->
                <div v-if="isModalOpen" class="fixed inset-0 bg-black bg-opacity-50 flex justify-center items-center">
                    <div class="bg-white rounded-lg p-8 w-full max-w-lg relative">
                        <span @click="closeModal" class="absolute top-2 right-2 cursor-pointer text-gray-600">✖</span>
                        <h3 class="text-2xl font-bold mb-4">{{ planName }}</h3>
                        <p class="text-xl mb-4">{{ planPrice }}</p>
                        <form @submit.prevent="submitPayment">
                            <div class="mb-4">
                                <label for="name" class="block text-sm font-medium text-gray-700">Nom complet</label>
                                <input type="text" v-model="name" required
                                    class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm">
                            </div>
                            <div class="mb-4">
                                <label for="email" class="block text-sm font-medium text-gray-700">Email</label>
                                <input type="email" v-model="email" required
                                    class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm">
                            </div>
                            <div class="mb-4">
                                <label for="card" class="block text-sm font-medium text-gray-700">Numéro de
                                    carte</label>
                                <input type="text" v-model="card" required
                                    class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm">
                            </div>
                            <button type="submit"
                                class="w-full bg-indigo-600 text-white py-2 rounded-lg hover:bg-indigo-700">Payer
                                maintenant</button>
                        </form>
                    </div>
                </div>
            </div>
        </main>
    </div>
</template>

<script setup>
import { Disclosure, DisclosureButton, DisclosurePanel, Menu, MenuButton, MenuItem, MenuItems } from '@headlessui/vue'
import { Bars3Icon, BellIcon, XMarkIcon } from '@heroicons/vue/24/outline'
import { ref, onMounted, onBeforeUnmount } from 'vue'

const user = {
    name: 'Tom Cook',
    email: 'tom@example.com',
    imageUrl: 'https://images.unsplash.com/photo-1472099645785-5658abf4ff4e?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=2&w=256&h=256&q=80',
}
const navigation = [
    { name: 'Home', href: '#', current: false },
    { name: 'Projects', href: '#', current: false },
    { name: 'Calendar', href: '#', current: false },
    { name: 'Reports', href: '#', current: false },
]
const userNavigation = [
    { name: 'Your Profile', href: '#' },
    { name: 'Settings', href: '#' },
    { name: 'Sign out', href: '#' },
]

const messages = [
    'Bienvenue sur notre site de vente en ligne',
    'Profitez de nos promotions exclusives',
    'Découvrez nos nouveaux produits chaque semaine',
    'Satisfaction garantie avec nos services',
]

const currentMessage = ref(messages[0])
let currentIndex = 0

const changeMessage = () => {
    currentIndex = (currentIndex + 1) % messages.length
    currentMessage.value = messages[currentIndex]
}

onMounted(() => {
    changeMessage()
    const interval = setInterval(changeMessage, 3000)

    onBeforeUnmount(() => {
        clearInterval(interval)
    })
})

// Modal state
const isModalOpen = ref(false)
const planName = ref('')
const planPrice = ref(0)
const name = ref('')
const email = ref('')
const card = ref('')

// Functions to manage modal
const openModal = (selectedPlanName, selectedPlanPrice) => {
    planName.value = selectedPlanName
    planPrice.value = selectedPlanPrice
    isModalOpen.value = true // Show the modal
}

const closeModal = () => {
    isModalOpen.value = false // Hide the modal
}

const submitPayment = () => {
    console.log('Paiement soumis pour', planName.value, 'au prix de', planPrice.value)
    // Reset fields
    name.value = ''
    email.value = ''
    card.value = ''
    closeModal() // Close modal after submission
}

// Mouse enter/leave effects on cards
onMounted(() => {
    const cards = document.querySelectorAll('.transform')
    cards.forEach(card => {
        card.addEventListener('mouseenter', () => {
            card.classList.add('scale-105')
        })

        card.addEventListener('mouseleave', () => {
            card.classList.remove('scale-105')
        })
    })
})
</script>

<style scoped>
.animate-scroll {
    animation: scroll 25s linear infinite;
}

@keyframes scroll {
    0% {
        transform: translateX(0);
    }

    100% {
        transform: translateX(-50%);
    }
}
</style>