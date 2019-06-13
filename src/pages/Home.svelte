<script>
    import { onMount } from 'svelte';
    import PostForm from '../components/PostForm.svelte';
    import env from '../../env.js';

    let posts = [];

    let editingPost = {
        id: null,
        title: '',
        body: ''
    };

    let postLimit = 6;

    onMount(async () => {
        const res = await fetch(`${env.API_BASE_URL}/posts/${postLimit}`);
        posts = await res.json();
    });

    // Rename the event.detail as post inside the function
    function addPost({detail: post}) {
        if(posts.find(p => p.id === post.id)) {
            const index = posts.findIndex(p => p.id === post.id);
            let postsUpdated = posts;

            postsUpdated.splice(index, 1, post);
            posts = postsUpdated;
        } else {
            posts = [post, ...posts];
        }

        editingPost = {
            id: null,
            title: '',
            body: ''
        };
    }

    function editPost(post) {
        editingPost = post;
    }

    function deletePost(postId) {
        if(confirm('Are you sure?')) {
            fetch(`${env.API_BASE_URL}/post/${postId}`, {
                method: 'DELETE'
            }).then(res => {
                return res.json();
            }).then(() => {
                posts = posts.filter(post => post.id !== postId);
            });
        }
    }

    function setLimit() {
        fetch(`${env.API_BASE_URL}/posts/${postLimit}`)
            .then(res => {
                return res.json();
            })
            .then(postsData => {
                posts = postsData;
            });
    }
</script>

<style>
    .delete-btn {
        color: red !important;
    }

    .card.card-content.card-title {
        margin-bottom: 0;
    }

    .card.card-content p.timestamp {
        color: #999;
        margin-bottom: 10px;
    }

    .postsLimit {
        margin: 50px;
    }

</style>

<div class="row">
    <div class="col s6">
        <PostForm on:postCreated={addPost} {editingPost}/>
    </div>

    <div class="col s3 postsLimit">
        <p>Limit number of posts</p>
        <input type="number" bind:value={postLimit} />
        <button on:click={setLimit} class="waves-effect waves-light btn">
            Set
        </button>
    </div>
</div>

<div class="row">
    {#if posts.length === 0}
        <h3>Loading...</h3>
    {:else}
        {#each posts as post}
            <div class="col s6">
                <div class="card">
                    <div class="card-content">
                        <p class="card-title">{post.title}</p>
                        <p class="timestamp">{post.createdAt}</p>
                        <p>{post.body}</p>
                    </div>
                    <div class="card-action">
                        <a href="#" on:click={() => editPost(post)}>Edit</a>
                        <a href="#" class="delete-btn" on:click={() => deletePost(post.id)}>Delete</a>
                    </div>
                </div>
            </div>
        {/each}
    {/if}
</div>