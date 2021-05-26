<template>
  <div class="row q-pa-md" style="max-width: 350px">
    <div class="col-5 q-pa-sm">      
      Стартапы
      <q-list bordered separator>
        <q-item 
          v-for="item in startups"
          :key="item.startupId"
          :label="item.name"
          clickable 
          v-ripple     
          @click="selectStartup(item)"        
        >
        <q-item-section>
          <q-item-label>{{item.name}}</q-item-label>          
        </q-item-section>
        </q-item>
      </q-list>
    </div>

    <div class="col-6 q-pa-sm">
      Идеи
      <q-list bordered separator v-if="filtredIdeas.length > 0">
        <q-item 
          v-for="item in filtredIdeas"
          :key="item.ideaId"
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
      <q-btn color="secondary" label="Предложить идею" @click="addIdea" />
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
          name: "RusAll123",
          corpId: 2,
          sphereId: 3,
        },
      ],      
      allRequests: [
        {
          desc: "Создать станок",
          corpId: 1,
        },
        {
          desc: "Создать технолгию",
          corpId: 2,
        },
      ],

      startups: [
        {
          name: "Стартап1",
          startupId: 1,
          sphereId: 3,
        },
        {
          name: "Стартап2",
          startupId: 2,
          sphereId: 3,
        },
        {
          name: "Стартап3",
          startupId: 3,
          sphereId: 2,
        },
        {
          name: "Стартап4",
          startupId: 4,
          sphereId: 2,
        },
      ],  
      ideas: [
        {
          name: "Idea1",
          startupId: 1,
        },
        {
          name: "Idea2",
          startupId: 1,
        },
        {
          name: "Idea3",
          startupId: 1,
        },
        {
          name: "Idea4",
          startupId: 4,
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
    addIdea() {
      console.log('add idea');
      this.$router.push({ path: '/login' });
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
