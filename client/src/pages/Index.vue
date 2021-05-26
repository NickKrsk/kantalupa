<template>
  <div class="q-pa-md q-gutter-md">
    <div class="row justify-between">

      <q-parallax
        src="https://cdn24.img.ria.ru/images/149555/56/1495555668_19:0:10019:5625_600x0_80_0_0_f3109c9d45d4b1518f2e528c4838daff.jpg"
      >
        <h1 class="text-white transparent">Место встречи инноваций и бизнеса</h1>
      </q-parallax>

    </div>
    <div class="row">
      <div class="col q-pa-md">
        <q-btn color="primary" class="full-width" label="Найти инвестиции" to="corps"/>
      </div>
      <div class="col q-pa-md">
        <q-btn color="secondary" class="full-width" label="Выбрать стартап" to="startups"/>
      </div>
    </div>

    <div>
      <h4>
        Сообщество инноваций
      </h4>
      <p>
        Помощь коллег, разработчиков, внедренцев и интеграторов для реализации комплексных проектов.
        Проверенные решения для повседневных задач и обсуждение эксклюзивных идей. Присоединяйся!
      </p>
    </div>

     <div class="row">
      <div class="col q-pa-md">
        <h4>Для стартапов</h4>
        <ul>
          <li>Найти инвестиции</li>
          <li>Обсудить идеи</li>
          <li>Найти единомышленников, сотрудников</li>
        </ul>
        <q-btn color="primary" class="full-width" label="Зарегистрироваться" to="register"/>
      </div>
      <div class="col q-pa-md">
        <h4>Для крупного бизнеса</h4>
        <ul>
          <li>Найти решения</li>
          <li>Найти подрядчиков</li>
          <li>Найти инновации</li>
        </ul>
        <q-btn color="secondary" class="full-width" label="Предложить проблему" to="register" />
      </div>
      <div class="col q-pa-md">
        <h4>Экосистема</h4>
        <ul>
          <li>Предложить инвестиции</li>
          <li>Предложить ресурсы</li>
          <li>Участвовать в развитии</li>
        </ul>
        <q-btn color="secondary" class="full-width" label="Присоединиться" to="register" />
      </div>
    </div>
    <br><br><br><br>
    <h3>Ближайшие события</h3>
    <div class="row items-start q-gutter-md">

      <q-card class="my-card">
        <img src="https://cdn.quasar.dev/img/mountains.jpg">

        <q-card-section>
          <div class="text-h6">Хакатон КРИТБИ</div>
          <div class="text-subtitle2">25-26 мая 2021</div>
        </q-card-section>

        <q-card-section class="q-pt-none">
          <q-btn color="secondary" class="full-width" label="Зарегистрироваться" to="register" />
        </q-card-section>
      </q-card>

      <q-card class="my-card">
        <img src="https://cdn.quasar.dev/img/parallax1.jpg">

        <q-card-section>
          <div class="text-h6">Инновации в строительстве / вебинар</div>
          <div class="text-subtitle2">12 июня 2021</div>
        </q-card-section>

        <q-card-section class="q-pt-none">
          <q-btn color="secondary" class="full-width" label="Зарегистрироваться" to="register" />
        </q-card-section>
      </q-card>

      <q-card class="my-card">
        <img src="https://cdn.quasar.dev/img/parallax2.jpg">

        <q-card-section>
          <div class="text-h6">Инновации в маркетинге</div>
          <div class="text-subtitle2">23 июня 2021</div>
        </q-card-section>

        <q-card-section class="q-pt-none">
          <q-btn color="secondary" class="full-width" label="Зарегистрироваться" to="register" />
        </q-card-section>
      </q-card>

      <q-card class="my-card">
        <img src="https://cdn.quasar.dev/img/chicken-salad.jpg">

        <q-card-section>
          <div class="text-h6">Бизнес-завтрак</div>
          <div class="text-subtitle2">2 июля 2021</div>
        </q-card-section>

        <q-card-section class="q-pt-none">
          <q-btn color="secondary" class="full-width" label="Зарегистрироваться" to="register" />
        </q-card-section>
      </q-card>
    </div>
  </div>

</template>

<style lang="sass" scoped>
.my-card
  width: 100%
  max-width: 300px

.transparent
   opacity: 0.6
   margin: 30px
   border: 1px solid black
   background-color: #000000 !important
   filter: alpha(opacity=60)
</style>
