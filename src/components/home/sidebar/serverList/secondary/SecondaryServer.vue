<template>
    <div v-for="(serverList, country) in list.secondary">
        <DropdownTitle class="cursor-pointer" :country="country" @click="open(country)" :is-open="country === selectedCountry"/>
        <Transition name="expand">
            <div v-if="selectedCountry === country" class="flex flex-col gap-y-[2px]">
                <Server v-for="server in serverList.sort((a, b) => a.city.localeCompare(b.city))" protocol="openvpn" :server="server"/>
            </div>
        </Transition>
    </div>
</template>
<script>
import Server from "@/components/home/sidebar/serverList/Server.vue";
import DropdownTitle from "@/components/home/sidebar/serverList/secondary/dropdown/DropdownTitle.vue";

export default {
    name: 'Dropdown',
    components: {DropdownTitle, Server},
    props: {
        list: {
            type: Object,
            required: true
        },
    },
    data() {
        return {
            selectedCountry: null,
        }
    },
    methods: {
        open(country) {
            if (country === this.selectedCountry) {
                this.selectedCountry = null
            } else this.selectedCountry = country
        },
    }
}
</script>
<style>

.expand-enter-active,
.expand-leave-active {
    transition: all 0.2s;
    height: 100%;
}

.expand-enter-from,
.expand-leave-to {
    opacity: 0;
    height: 0;
}

</style>
