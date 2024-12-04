<template>
    <Layout>
        <div class="home">
            <h1>Contact Nick!</h1>
            <p>I love connecting with people, answering questions, and receiving feedback. Feel free to reach out using
                any of the methods below!</p>
        </div>

        <div class="contact-box">
            <h2>
                <a href="mailto:Nicholasp.stull@gmail.com">
                    <i class="fas fa-envelope"></i> Email
                </a>
            </h2>
            <p>
                If you have a question, comment, or just want to chat, send me an email
                and I'll get back to you as soon as possible.
            </p>
        </div>

        <div class="contact-box">
            <h2>
                <a href="https://github.com/tinkernerd" target="_blank">
                    <i class="fab fa-github"></i> GitHub
                </a>
            </h2>
            <p>
                Check out my projects, see what I'm working on, or contribute to any
                ongoing work on my GitHub profile.
            </p>
        </div>

        <div class="contact-box">
            <h2>
                <a href="https://github.com/tinkernerd/ISYS115/issues" target="_blank">
                    <i class="fas fa-comment-dots"></i> Feedback
                </a>
            </h2>
            <p>
                If you have any questions or would like to contribute to the notes,
                please feel free to
                <a href="https://github.com/tinkernerd/ISYS115/issues" target="_blank">
                    open an issue
                </a>
                or
                <a href="https://github.com/tinkernerd/ISYS115/pulls" target="_blank">
                    submit a pull request
                </a>
                on the project's GitHub repository.
            </p>
        </div>

        <div class="contact-box">
            <h2>
                <a href="https://instagram.com/therealnicholasstull" target="_blank">
                    <i class="fab fa-instagram"></i> Instagram
                </a>
            </h2>
            <p>
                Stay updated with my latest thoughts and announcements by following me
                on Instagram.
            </p>
        </div>
    </Layout>
</template>

<script>
export default {
    name: "ContactPage",
};
</script>

<style scoped lang="scss">
h1 {
    margin-top: -15px;
    margin-bottom: 10px;
    font-family: Gilroy, var(--vp-font-family-base);
    font-size: 32px;
    line-height: 1.2;
    font-weight: 800;
    position: relative;
    display: inline-block;

    &::after {
        content: '';
        display: block;
        width: 100%;
        height: 4px;
        background-color: #387c3b;
        margin: 8px 0 0;
    }

    @media (min-width: 960px) {
        white-space: nowrap;
        margin-top: -25px;
        font-size: 48px;
        line-height: 1;
    }
}

.contact-box {
    margin: 20px 0;
    padding: 20px;
    border: 1px solid #ddd;
    border-radius: 5px;

    h2 {
        margin: 0 0 10px;
        font-size: 24px;
        color: #387c3b;
    }

}
</style>
