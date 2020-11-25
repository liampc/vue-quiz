<template>
    <div>
        <b-navbar type="light" variant="info">
            <b-navbar-nav>
            <b-nav-item >Hollywoo stars and celebrities what do they know </b-nav-item>
            <b-nav-item> Counter {{correctAnswers}}/{{totalAnswers}} </b-nav-item>
            </b-navbar-nav>
        </b-navbar>
    </div>
</template>

<script>
export default {
    props: [
        "correctAnswers",
        "totalAnswers",
    ]
}
</script>