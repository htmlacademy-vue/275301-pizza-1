<template>
  <div>
    <header class="header">
      <div class="header__logo">
        <a href="index.html" class="logo">
          <img
            src="~@/assets/img/logo.svg"
            alt="V!U!E! Pizza logo"
            width="90"
            height="40"
          />
        </a>
      </div>
      <div class="header__cart">
        <a href="cart.html">0 ₽</a>
      </div>
      <div class="header__user">
        <a href="#" class="header__login"><span>Войти</span></a>
      </div>
    </header>
    <main class="content">
      <form action="#" method="post">
        <div class="content__wrapper">
          <h1 class="title title--big">Конструктор пиццы</h1>
          <div class="content__dough">
            <div class="sheet">
              <h2 class="title title--small sheet__title">Выберите тесто</h2>
              <div class="sheet__content dough">
                <label
                  v-for="dough_type in getDoughType"
                  :key="dough_type.name"
                  :class="`dough__input dough__input--${dough_type.type}`"
                >
                  <input
                    type="radio"
                    name="dought"
                    :value="getDoughType.type"
                    class="visually-hidden"
                    checked
                  />
                  <b>{{ dough_type.name }}</b>
                  <span>{{ dough_type.description }}</span>
                </label>
              </div>
            </div>
          </div>
          <div class="content__diameter">
            <div class="sheet">
              <h2 class="title title--small sheet__title">Выберите размер</h2>
              <div class="sheet__content diameter">
                <label
                  v-for="size in getSizes"
                  :key="size.name"
                  :class="`diameter__input diameter__input--${size.type}`"
                >
                  <input
                    type="radio"
                    name="diameter"
                    :value="getSizes.type"
                    class="visually-hidden"
                  />
                  <span>{{ size.name }}</span>
                </label>
              </div>
            </div>
          </div>
          <div class="content__ingridients">
            <div class="sheet">
              <h2 class="title title--small sheet__title">
                Выберите ингридиенты
              </h2>
              <div class="sheet__content ingridients">
                <div class="ingridients__sauce">
                  <p>Основной соус:</p>
                  <label
                    v-for="sauce in getSauces"
                    :key="sauce.name"
                    class="radio ingridients__input"
                  >
                    <input
                      type="radio"
                      name="sauce"
                      :value="getSauces.type"
                      checked
                    />
                    <span>{{ sauce.name }}</span>
                  </label>
                </div>

                <div class="ingridients__filling">
                  <p>Начинка:</p>
                  <ul class="ingridients__list">
                    <li
                      v-for="ingredient in getIngredients"
                      :key="ingredient.name"
                      class="ingridients__item"
                    >
                      <span :class="`filling filling--${ingredient.type}`">
                        {{ ingredient.name }}
                      </span>
                      <div class="counter counter--orange ingridients__counter">
                        <button
                          type="button"
                          class="
                            counter__button
                            counter__button--disabled
                            counter__button--minus
                          "
                        >
                          <span class="visually-hidden">Меньше</span>
                        </button>
                        <input
                          type="text"
                          name="counter"
                          class="counter__input"
                          value="0"
                        />
                        <button
                          type="button"
                          class="counter__button counter__button--plus"
                        >
                          <span class="visually-hidden">Больше</span>
                        </button>
                      </div>
                    </li>
                  </ul>
                </div>
              </div>
            </div>
          </div>
          <div class="content__pizza">
            <label class="input">
              <span class="visually-hidden">Название пиццы</span>
              <input
                type="text"
                name="pizza_name"
                placeholder="Введите название пиццы"
              />
            </label>
            <div class="content__constructor">
              <div class="pizza pizza--foundation--big-tomato">
                <div class="pizza__wrapper">
                  <div class="pizza__filling pizza__filling--ananas"></div>
                  <div class="pizza__filling pizza__filling--bacon"></div>
                  <div class="pizza__filling pizza__filling--cheddar"></div>
                </div>
              </div>
            </div>
            <div class="content__result">
              <p>Итого: 0 ₽</p>
              <button type="button" class="button button--disabled" disabled>
                Готовьте!
              </button>
            </div>
          </div>
        </div>
      </form>
    </main>
  </div>
</template>
<script>
import pizza from "../static/pizza.json";
import misc from "../static/misc.json";
import user from "../static/user.json";
import {
  normalizeDoughType,
  normalizeIngredientsType,
  normalizeSauceType,
  normalizeSizeType,
} from "../common/helpers.js";

export default {
  name: "Index",
  data() {
    return {
      misc,
      user,
    };
  },
  computed: {
    getDoughType() {
      return pizza.dough.map((dough_type) => normalizeDoughType(dough_type));
    },
    getSizes() {
      return pizza.sizes.map((size) => normalizeSizeType(size));
    },
    getSauces() {
      return pizza.sauces.map((sauce) => normalizeSauceType(sauce));
    },
    getIngredients() {
      return pizza.ingredients.map((ingredient) =>
        normalizeIngredientsType(ingredient)
      );
    },
  },
};
</script>
<style lang="scss"></style>
