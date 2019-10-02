<template>
        <a-timeline-item>
            <p>{{ created_at }}</p>
            <a-tooltip>
                <template slot="title">
                    Number of forks : {{ forks_count }}
                    Open issues : {{ open_issues_count }}
                </template>
                 <a :href="html_url" class="title">{{ name }}</a>
            </a-tooltip>
            <p>{{ description }}</p>
            <p>Language: {{ language }}</p>
        </a-timeline-item>
</template>

<script>
export default {
    props: ['name', 'description', 'created_at', 'html_url', 'forks_count', 'language', 'open_issues_count']
}
</script>

<style scoped>
a{
    text-decoration: none;
    color: #040404;
    text-transform: uppercase;
}
</style>