<template>
  <div class="row q-pa-md" style="max-width: 350px">
    <div class="col-5 q-pa-sm">
      Корпорации
      <q-list bordered separator>
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

    <div class="col-5 q-pa-sm">
      Запросы
      <q-list bordered separator v-if="filtredReq.length > 0">
        <q-item 
          v-for="item in filtredReq"
          :key="item.id"
          :label="item.desc"
          clickable 
          v-ripple     
          @click="selectCorp(group)"        
        >
        <q-item-section>
          <q-item-label>{{item.desc}}</q-item-label>
        </q-item-section>
        </q-item>
      </q-list>
    </div>

    <div class="col-5 q-pa-sm">
      Стартапы
      <q-list bordered separator>
        <q-item 
          v-for="item in startups"
          :key="item.startupId"
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
      allCorps: [
        {
          name: "RusAll",
          corpId: 1,
        },
        {
          name: "RusAll123",
          corpId: 2,
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
        },
        {
          name: "Стартап2",
          startupId: 2,
        },
        {
          name: "Стартап3",
          startupId: 3,
        },
        {
          name: "Стартап4",
          startupId: 4,
        },
      ],  
      filtredReq: [],
    };
  },
  methods: {   
    selectCorp(corp) {
      this.filtredReq = this.allRequests.filter((el) => el.corpId === corp.corpId);   
      console.log(this.filtredReq);   
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
