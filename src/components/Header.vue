<template>
    <nav>
        <div id="container">
            <div id="flex">
                <h1>Reaction Timer</h1>
                <p>Vue Project</p>
            </div>
        </div>
    </nav>
</template>

<style scoped>
    nav {
        background: #30E3CA;
        color: #40514E;
    }

    #container {
        margin: 0 10rem;
    }

    #flex {
        display: flex;
        justify-content: space-between;
        align-items: center;
        padding: 0.9rem 0;
    }

    p {
        margin: 0;
    }

    @media (max-width: 481px) {
        #container {
            margin: 0 1rem;
        }
    }
</style>