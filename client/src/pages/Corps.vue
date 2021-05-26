<template>
  <div class="row q-pa-md" style="max-width: 350px">
    <div class="col-5 q-pa-sm">
      Корпорации
      <q-list bordered separator style="max-width: 600px">
        <q-item 
          v-for="item in allCorps"
          :key="item.id"
          :label="item.name"
          clickable 
          v-ripple     
          @click="selectCorp(item)"        
        >
        <q-item-section>
          <q-item-label>{{item.name}}</q-item-label>          
        </q-item-section>
        </q-item>
      </q-list>
    </div>

    <div class="col-6 q-pa-sm">
      Запросы
      <q-list bordered separator v-if="filtredReq.length > 0">
        <q-item 
          v-for="item in filtredReq"
          :key="item.id"
          :label="item.desc"
          clickable 
          v-ripple     
          @click="selectReq(item)"        
        >
        <q-item-section>
          <q-item-label>{{item.desc}}</q-item-label>
        </q-item-section>
        </q-item>
      </q-list>     
      <q-btn color="secondary" label="Создать запрос" @click="addCorp" />
    </div>
    <div class="col-5 q-pa-sm">
      Сферы
      <q-list bordered separator>
        <q-item 
          v-for="item in spheres"
          :key="item.sphereId"
          :label="item.name"
          clickable 
          v-ripple     
          @click="selectSphere(item)"        
        >
        <q-item-section>
          <q-item-label>{{item.name}}</q-item-label>          
        </q-item-section>
        </q-item>
      </q-list>
    </div>

  </div>
</template>

<script>
// import LeadAddCard from './LeadAddCard';
// import { getBaseUrl } from '../utils';

export default {
  name: 'Corps',
  props: {    
  },
  // },
  data() {
    return {
      /* currentGroup: {
        groupId: 'calls',
        title: 'Звонки',
        icon: 'phone',
      },
      filterText: '', */
      curCorp: {},
      curReq: {},
      allCorps: [
        {
          name: "RusAll",
          corpId: 1,
          sphereId: 3,
        },
        {
          name: "БРАЛ",
          corpId: 2,
          sphereId: 3,
        },
        {
          name: "БСМП",
          corpId: 3,
          sphereId: 3,
        },
        {
          name: "Тракторный завод",
          corpId: 4,
          sphereId: 3,
        },
      ],      
      allRequests: [
        {
          desc: "Разработать технологию очистки выбросов",
          corpId: 1,
        },
        {
          desc: "Разработать ПО для учета кадров",
          corpId: 1,
        },
        {
          desc: "Разработать комплекс для воздухоочистки",
          corpId: 2,
        },
        {
          desc: "Автоматизировать прием заявок",
          corpId: 3,
        },
      ],
      spheres: [
        {
          name: "Медицина",
          sphereId: 1,
        },
        {
          name: "Транспорт",
          sphereId: 2,
        },
        {
          name: "Металлургия",
          sphereId: 3,
        },
      ],
      filtredReq: [],
      filtredIdeas: [],
    };
  },
  mounted() {
    this.filtredReq = this.allRequests;
  },
  methods: {   
    addCorp() {      
      this.$router.push({ path: '/addCorp' });
    },
    selectCorp(corp) {
      this.filtredReq = this.allRequests.filter((el) => el.corpId === corp.corpId);   
      console.log(this.filtredReq);         
    },
    selectReq(req) {
      this.curReq = req;
    },
    selectStartup(startup) {
      this.filtredIdeas = this.ideas.filter((el) => el.startupId === startup.startupId);       
    },
    selectSphere(sphere) {
      // this.filtredIdeas = this.ideas.filter((el) => el.startupId === startup.startupId);       
    },
  },
  computed: {
    searchedLeads() {
      return this.filterText !== ""
        ? this.leadsInCurrentGroup
          .filter((lead) => (lead.name ? lead.name.toLowerCase().includes(this.filterText.toLowerCase()) : false)
            || (lead.phone ? lead.phone.includes(this.filterText) : false))
        : this.leadsInCurrentGroup;
    },
    leadsInCurrentGroup() {
      return this.leads.filter((lead) => lead.groupId === this.currentGroup.groupId);
    },
    groupsWithoutUnparsed() {
      return this.groups.filter((group) => group.groupId !== 'unparsed');
    },
    unparsedGroup() {
      return this.groups.find((group) => group.groupId === 'unparsed');
    },
  }, 
};
</script>
