<template>
    <header class="header-container">
        <img src="../assets/bmuse_logo.png" alt="BMUSE Logo"/>
        <div class="right-side">
            <div class="search-container">
                <img class="search-icon" src="../assets/search.png" alt="Search Icon">
            </div>
        </div>
    </header>
</template>
<style lang="scss" scoped>
    .header-container {
        display: flex;

        .right-side {
            margin-left: auto;

            .search-container {
                height: 50px;
                width: 50px;
                border-radius: 50px;
                background-color: black;
                display: flex;
                align-items: center;
                justify-content: center;

                .search-icon {
                    height: 20px;
                    width: 20px;
                }
            }
        }
    }
</style>
