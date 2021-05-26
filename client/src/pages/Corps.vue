<template>
  <div class="q-pa-md" style="max-width: 350px">
    <q-list bordered separator>
     <q-item 
      v-for="item in allCorps"
      :key="item.id"
      :label="item.name"
      clickable 
      v-ripple     
      @click="selectCorp(group)"        
     >
        <q-item-section>
          <q-item-label>{{item.name}}</q-item-label>
          <q-item-label caption>Caption</q-item-label>
        </q-item-section>
      </q-item>
    </q-list>
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
          id: 1,
        },
        {
          name: "RusAll123",
          id: 2,
        },
      ],
    };
  },
  methods: {   
    selectGroup(group) {
      this.currentGroup = group;
      this.onGroupSelect(group);
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
