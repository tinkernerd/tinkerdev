<template>
    <div>
        <!-- Cookie Notice -->
        <div id="cookie-notice" v-if="!cookieAccepted">
            <span>
                We use cookies to improve your experience and our services. By continuing to use this site, you consent
                to our use of cookies.
            </span>
            <div class="actions">
                <button @click="acceptCookies" class="btn-accept">Approve</button>
                <a href="/privacy" class="btn-info">More info</a>
            </div>
        </div>

        <!-- Fun Popup -->
        <div id="fun-popup" v-if="showFunPopup">
            <h2 class="popup-title">Welcome Back!</h2>
            <p>{{ popupMessage }}</p>
            <div class="popup-actions">
                <button class="btn-close" @click="closePopup">Close</button>
                <button class="btn-stop" @click="stopPopup">Don’t Show Again</button>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            cookieAccepted: false,
            showFunPopup: false,
            popupMessage: "",
            messages: [
                "Learning is fun!",
                "Yay! You came back for more JavaScript!",
                "Debugging: because every programmer needs a challenge!",
                "Computers are fast; programmers keep them slow.",
                "Code like there's no tomorrow!",
                "Let's make the web great... again?"
            ]
        };
    },
    methods: {
        createCookie(name, value, days) {
            let expires = "";
            if (days) {
                const date = new Date();
                date.setTime(date.getTime() + days * 24 * 60 * 60 * 1000);
                expires = "; expires=" + date.toUTCString();
            }
            document.cookie = `${name}=${value}${expires}; path=/`;
        },
        readCookie(name) {
            const nameEQ = `${name}=`;
            const ca = document.cookie.split(";");
            for (let c of ca) {
                while (c.charAt(0) === " ") c = c.substring(1, c.length);
                if (c.indexOf(nameEQ) === 0) return c.substring(nameEQ.length, c.length);
            }
            return null;
        },
        acceptCookies() {
            this.createCookie("cookie-notice-dismissed", "true", 31);
            this.cookieAccepted = true;
        },
        closePopup() {
            this.showFunPopup = false;
        },
        stopPopup() {
            this.createCookie("fun-popup-dismissed", "true", 365);
            this.showFunPopup = false;
        },
        initializePopup() {
            const dismissed = this.readCookie("cookie-notice-dismissed") === "true";
            const popupDismissed = this.readCookie("fun-popup-dismissed") === "true";

            this.cookieAccepted = dismissed;
            if (dismissed && !popupDismissed) {
                const randomIndex = Math.floor(Math.random() * this.messages.length);
                this.popupMessage = this.messages[randomIndex];
                this.showFunPopup = true;
            }
        }
    },
    mounted() {
        this.initializePopup();
    }
};
</script>

<style scoped>
/* Cookie Notice */
#cookie-notice {
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
}

#cookie-notice span {
    margin-bottom: 0.75rem;
    text-align: center;
    font-size: 1rem;
}

#cookie-notice .actions {
    display: flex;
    gap: 1rem;
}

.btn-accept {
    background: #387c3b;
    color: white;
    padding: 0.5rem 1.5rem;
    border: none;
    border-radius: 4px;
    cursor: pointer;
}

.btn-accept:hover {
    background: #2d6330;
}

.btn-info {
    color: #387c3b;
    text-decoration: underline;
    font-size: 1rem;
    cursor: pointer;
}

/* Fun Popup */
#fun-popup {
    padding: 1.5rem;
    position: fixed;
    top: 20%;
    left: 50%;
    transform: translate(-50%, -50%);
    max-width: 500px;
    background: #2a2a2a;
    color: rgba(255, 255, 255, 0.9);
    border-radius: 12px;
    text-align: center;
    box-shadow: 0 4px 16px rgba(0, 0, 0, 0.4);
    z-index: 1001;
}

.popup-title {
    font-size: 1.5rem;
    margin-bottom: 0.75rem;
}

.popup-actions {
    display: flex;
    justify-content: center;
    gap: 1rem;
    margin-top: 1rem;
}

.btn-close,
.btn-stop {
    padding: 0.5rem 1rem;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    font-size: 1rem;
}

.btn-close {
    background: #666;
    color: white;
}

.btn-close:hover {
    background: #555;
}

.btn-stop {
    background: #d9534f;
    color: white;
}

.btn-stop:hover {
    background: #c9302c;
}
</style>
