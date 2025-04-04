<script>
</script>

<template>
    <div class="logo">
        <img src="../components/icons/2160688.png">
    </div>
    <nav class="nav-item">
        <li>
            Разминка
        </li>
        <li>
            Воробьиные
        </li>
        <li>
            Лесные птицы
        </li>
        <li>
            Певчие птицы
        </li>
        <li>
            Хищные птицы
        </li>
        <li>
            Морские птицы
        </li>
    </nav>
</template>

<style>
* {
    background-color: rgb(179, 236, 174);
}
.nav-item{
    display: flex;
    justify-content: space-around;
    list-style-type: none;
    border: 1px solid rgb(62, 179, 144);
    border-radius: 10px;
    background-color: rgb(62, 179, 144);
}

.nav-item li {
    padding: 10px;
    color: white;
    background-color: rgb(62, 179, 144);
    cursor: pointer;
}
.nav-item li:hover {
    background-color: rgb(49, 139, 112)
}
.logo img{
    max-width: 150px;
    max-height: auto;
}
</style>