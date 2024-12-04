<template>
    <transition name="slide">
        <aside v-if="isOpen" class="navbar">
            <div class="navbar-header">
                <button @click="closeNavbar" class="close-button">
                    <XIcon clas="X" />
                </button>
            </div>
            <ul class="navbar-menu">
                <li><a href="/hardware">Hardware</a></li>
                <li><a href="/programming">Programming & Tools</a></li>
                <li><a href="/documentation">Documentation</a></li>
                <li><a href="/software">Software & Operating Systems</a></li>
                <li><a href="/networking">Networking & Security</a></li>
            </ul>
        </aside>
    </transition>
</template>

<script>
import { XIcon } from "vue-feather-icons";

export default {
    props: {
        isOpen: {
            type: Boolean,
            required: true,
        },
    },
    emits: ["close"],
    components: {
        XIcon,
    },
    methods: {
        closeNavbar() {
            this.$emit("close");
        },
    },
};
</script>

<style scoped>
.navbar {
    position: fixed;
    top: 0;
    right: 0;
    width: 300px;
    height: 100%;
    background: #fff;
    box-shadow: -2px 0 5px rgba(0, 0, 0, 0.1);
    display: flex;
    flex-direction: column;
    z-index: 20;
    padding: 20px;
}

.navbar-header {
    display: flex;
    justify-content: flex-end;
}

.close-button {
    background: none;
    border: none;
    cursor: pointer;
}

.navbar-menu {
    list-style: none;
    padding: 0;
    margin: 20px 0;
}

.navbar-menu li {
    margin: 15px 0;
}

.navbar-menu a {
    text-decoration: none;
    color: #333;
    font-size: 18px;
}

.slide-enter-active,
.slide-leave-active {
    transition: transform 0.3s ease-in-out;
}

.slide-enter {
    transform: translateX(100%);
}

.slide-leave-to {
    transform: translateX(100%);
}

</style>
