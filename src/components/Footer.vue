<template>
    <footer class="site-footer">
        <p>
            &copy; 2024 The Tinkering Nerd. All rights reserved. | Excuse of the day is:
            <span class="excuse-text">{{ excuseOfTheDay }}</span>
        </p>
    </footer>
</template>

<script>
export default {
    name: "SiteFooter",
    data() {
        return {
            excuseOfTheDay: "Loading...",
        };
    },
    methods: {
        async fetchExcuse() {
            try {
                const response = await fetch(
                    "https://meyerweb.com/feeds/excuse/rss20.xml"
                );
                const text = await response.text();
                const parser = new DOMParser();
                const xmlDoc = parser.parseFromString(text, "text/xml");
                const excuse =
                    xmlDoc.querySelector("item > description")?.textContent ||
                    "Unable to fetch excuse.";
                this.excuseOfTheDay = excuse;
            } catch (error) {
                console.error("Failed to fetch Excuse of the Day:", error);
                this.excuseOfTheDay = "Unable to fetch excuse.";
            }
        },
    },
    mounted() {
        this.fetchExcuse();
    },
};
</script>

<style scoped>
.site-footer {
    position: fixed;
    bottom: 0;
    left: 0;
    right: 0;
    padding: 1rem;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    align-items: center;
    background: #2a2a2a;
    color: rgba(255, 255, 255, 0.9);
    box-shadow: 0 -2px 8px rgba(0, 0, 0, 0.2);
    z-index: 1000;
    height: auto;
    /* Ensures it adjusts based on content */
}

.site-footer span {
    margin-bottom: 0.75rem;
    text-align: center;
    font-size: 1rem;
}

.site-footer .actions {
    display: flex;
    gap: 1rem;
}

.excuse-text {
    font-weight: bold;
    color: #ffa726;
    font-style: italic;
}
</style>
