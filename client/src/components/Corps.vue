<template>
  <div class="row">    
    <div class="col-5 q-pa-sm">
      <q-list bordered padding class="rounded-borders text-primary bg-white shadow-2">
        <q-item
          v-for="group in groupsWithoutUnparsed"
          :key="group.groupId"
          :label="group.groupId"
          clickable
          v-ripple          
          @click="selectGroup(group)"
          active-class="my-menu-link"
          :active="currentGroup.groupId === group.groupId"          
        >        
          <q-item-section avatar>
            <q-icon :name="group.icon"></q-icon>
          </q-item-section>

          <q-item-section>{{group.title}}</q-item-section>
          <q-item-section side>
            <!-- {{ group.amountOfUnread }} -->
            <q-badge align="middle" rounded transparent :color="getColor(group.amountOfUnread)" v-if="group.amountOfUnread > 0">
                  {{ group.amountOfUnread }}
            </q-badge>
          </q-item-section>
        </q-item>        
        <q-separator color="primary" inset />    
        <q-item
          :key="unparsedGroup.groupId"
          :label="unparsedGroup.groupId"
          clickable
          v-ripple          
          @click="selectGroup(unparsedGroup)"
          active-class="my-menu-link"
          :active="currentGroup.groupId === unparsedGroup.groupId"          
        >        
        
          <q-item-section avatar>
            <q-icon :name="unparsedGroup.icon"></q-icon>
          </q-item-section>
        
          <q-item-section>{{unparsedGroup.title}}</q-item-section>
          <q-item-section side>            
            <q-badge align="middle" rounded transparent :color="getColor(unparsedGroup.amountOfUnread)" v-if="unparsedGroup.amountOfUnread > 0">
                  {{ unparsedGroup.amountOfUnread }}
            </q-badge>

          </q-item-section>
        </q-item>
      </q-list>
    </div>

    <div class="col-7 q-pa-sm">
      <q-card class="height85">
        <q-item>
          <q-item-section>
            <div class="text-h6">{{currentGroup.title}}</div>
          </q-item-section>
          <q-item-section side>
            <q-card-actions vertical class="justify-around">
              <q-btn round icon="add" dense @click="showAddLeadDialog" />
            </q-card-actions>
          </q-item-section>
        </q-item>

        <q-toolbar>
          <q-input rounded outlined dense 
            class="full-width" 
            bg-color="white" 
            v-model="filterText" 
            placeholder="Фильтр по имени или номеру">
            <template v-slot:append>
              <q-icon v-if="filterText !== ''" name="close" @click="filterText=''" class="cursor-pointer" />
              <q-icon v-if="filterText === ''" name="search" />
            </template>
          </q-input>
        </q-toolbar>

        <q-scroll-area style="height: 67vh; max-width: 300px;" ref="scrollAreaLeads">
          <q-list class="scroll">
            <q-item
              v-for="lead in searchedLeads"
              :key="lead.id"
              clickable
              v-ripple          
              @click="selectLead(lead)"
              active-class="my-menu-link"
              :active="currentLead.leadId === lead.leadId"
            >              
              <q-item-section avatar>
                <q-avatar>
                  <img :src="avatarUrl(lead)" :style="styleAvatar(lead)"/>                         
                </q-avatar>                                                                         
              </q-item-section>
          
              <q-item-section>
                <q-item-label lines="1">
                  {{ lead.name || lead.phone }}
                </q-item-label>
                <q-item-label caption lines="1">
                  {{ lead.company }} 
                </q-item-label>

                <!-- <q-item-label caption>
                  {{ lead.phone }}  
                </q-item-label> -->

                <q-item-label caption>
                  {{ formatDate(lead.lastModifiedDate) }}
                </q-item-label>
              </q-item-section>

              <q-item-section side>
                <template v-if="lead.isWhatsapp === 'present'">
                  <q-badge align="top" color="teal" rounded  transparent outline style="fontSize:9px">WhatpsApp</q-badge> 
                  <br/>
                </template>
                <q-badge align="middle" rounded transparent  :color="getColor(lead.amountOfUnread)" v-if="lead.amountOfUnread > 0">{{ lead.amountOfUnread }}</q-badge>                
              </q-item-section>                                             
            </q-item>            
          </q-list>
        </q-scroll-area>

        <q-card-actions class="absolute-bottom" >
          <q-btn flat color="dark" :label="`Всего ${leadsInCurrentGroup.length}`"/>
        </q-card-actions>
      </q-card>
    </div>

  </div>
</template>

<script>
//import LeadAddCard from './LeadAddCard';
// import { getBaseUrl } from '../utils';

export default {
  name: 'Leads',
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
    };
  },
  /* methods: {
    getColor(amountOfUnread) {
      if (amountOfUnread > 20) return 'red';
      if (amountOfUnread > 10) return 'orange';
      return 'teal';
    },
    showAddLeadDialog() {
      this.$q.dialog({
        component: LeadAddCard,
      }).onOk((data) => {
        console.log('data', data);
        const newLead = {
          name: data.name,
          phone: data.phone,
          groupId: this.currentGroup.groupId,
          userId: this.$store.getters.userId,
        };
        this.onLeadAdd(newLead);
      });
    },
    selectLead(lead) {      
      this.onLeadSelect(lead);  
    },
    selectGroup(group) {     
      this.currentGroup = group;
      this.onGroupSelect(group);
    },
    formatDate(date) {
      return moment(date).format('D.MM.YYYY HH:mm');
    },
    avatarUrl(lead) {
      return lead && lead.avatar ? lead.avatar : `${getBaseUrl()}/leads/avatar/default.png`;
    },
    styleAvatar(lead) {
      return lead.isWhatsapp === 'present' ? 'border: 3px teal solid' : '';
    },
    styleUnparsed() {
      const count = this.leads.reduce((acc, lead) => {
        const res = acc + (lead.groupId === 'unparsed' ? 1 : 0);
        return res;
      }, 0);
      return count > 0 ? 'color: #ff0042' : 'color: #ccc';
    },
    scrollLeadsToTop() {
      console.log('scrollLeadsToTop');
      this.$refs.scrollAreaLeads.setScrollPercentage(0, 0);
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
  }, */
};
</script>

<style scoped>
.height85 {
  height: calc(85vh);
}
</style>

<style lang="sass">
.my-menu-link
  color: white
  background: #128C7E
</style>
