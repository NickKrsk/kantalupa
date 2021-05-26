<template>
  <q-page class="flex flex-center">    
    <div class="q-pa-md row items-start q-gutter-md">    
    <q-form
      @submit="onSubmit"
      @reset="onReset"
      class="q-gutter-md"
    >
      <q-input filled label="Название *" hint="Отрасль" />
      <q-input filled label="Рынок присутствия" hint="Рынок присутствия" />
      <q-input filled label="Количество сделок" hint="" />
      
      <div class="q-gutter-sm">        
        Уровень заинтересованности в инвестициях
        <q-radio v-model="shape" val="line" label="Низкий" />
        <q-radio v-model="shape" val="rectangle" label="Средний" />
        <q-radio v-model="shape" val="ellipse" label="Высокий" />
      </div>

      <div class="q-gutter-sm">
        <q-checkbox v-model="right" label="Готовность предоставить свое предприятие под пилотное решение" />
      </div>

       <div class="q-pa-md">
        <q-input
          v-model="text"
          filled
          type="textarea"
        />
      </div>

      <div>
        <q-btn label="Отправить" type="submit" color="primary"/>
        <q-btn label="Отмена" type="reset" color="primary" flat class="q-ml-sm" />
      </div>
    </q-form>
    </div>
  </q-page>
</template>

<script>
export default {
 
};
</script>
