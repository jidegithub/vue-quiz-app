<template>
    <div class="navbar-menu">
        <div class="navbar-end">
            <div class="navbar-item">
                <div class="field is-grouped">
                    <p class="control">
                    <a>
                        <span class="icon">
                        <i class="fas fa-twitter" aria-hidden="true"></i>
                        </span>
                        <span>Quiz App</span>
                    </a>
                    </p>
                    <p class="control">
                    <a class="button is-primary">
                        <span>question</span>  {{ Currentquestion + 1 }} of 10
                        <span class="icon">
                        <i class="fas fa-download" aria-hidden="true"></i>
                        </span>
                        <span>correct</span> 1 of 10
                    </a>
                    </p>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props:{
        Currentquestion:Number
    }
}
</script>

<style>

</style>