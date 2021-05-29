<template>
    <div class="twoot-item" @click="favouriteTwoot(twoot.id)">
        <div class="user-profile_twoot">
            <div class="twoot-item__user">
                @{{username}}
            </div>
            <div class="twoot-item__content">
                {{twoot.content}}
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'TwootItem',
    props: {
        username: {
            type: String, 
            required: true
        },
        twoot: {
            type: Object,
            required: true
        }
    },
    methods: {
        favouriteTwoot(id) {
            this.$emit('favourite', id)
        }
    }
};
</script>

<style> 
.twoot-item {
    padding: 20px;
    background-color: #fff;
    border-radius: 5px;
    border: 1px solid #DFE3E8;
    cursor: pointer;
    transition: all .25s ease;
    width: 50%;
    /* margin: 1rem 0; */
}
/* hover funktioniert nicht wie gewollt, deshalb auskommentiert */
/* 
.twoot-item :hover {
    transform: scale(1.1, 1.1);
} */

.twoot-item__user {
    font-weight: bold;
}
</style>