<script setup>
definePageMeta({
  title: "Upload Excel Card Assignment",
  
});

const form = ref ({
    cardassign_doc = "",
    user_role = "",
    school_name = "",
})
</script>

<template>
 

  <!-- UPLOAD DOC -->
  <rs-card class="flex-wrap justify-between p-5 bg-white text-black rounded-md flex-col" >

    <div class="p-5">
       <FormKit type="form" :actions="false" :incomplete-message="true" @submit="submit" id="myForm"> 
        <div class="flex flex-row justify-between">
          <div class="basis-1/2 mr-5">
            <FormKit type="file" label="Documents" accept=".pdf,.doc,.docx,.xml,.md,.csv" validation="required|length:0,200" v-model="form.cardassign_doc">
              <template #label>
              <label class="formkit-label text-gray-700 dark:text-gray-200 block mb-2 font-semibold text-sm formkit-invalid:text-red-500">Documents <span class="text-danger">*</span></label>
              </template>
            </FormKit>
          </div>
          <div class="basis-1/2 mr-5">
            <FormKit 
              type="select" 
              label="School Name"
              :options="school"
              validation="required|length:0,200"
              v-model="form.student_school"
            >
              <template #label>
              <label class="formkit-label text-gray-700 dark:text-gray-200 block mb-2 font-semibold text-sm formkit-invalid:text-red-500">School Name <span class="text-danger">*</span></label>
              </template>
            </FormKit>
          </div>
          <div class="basis-1/2">
          <FormKit type="select" label="User Role" :options="userRole" validation="required|length:0,200" v-model="form.user_role" >
            <template #label>
            <label class="formkit-label text-gray-700 dark:text-gray-200 block mb-2 font-semibold text-sm formkit-invalid:text-red-500">Class <span class="text-danger">*</span></label>
            </template>
          </FormKit>
        </div>
        </div>
      </FormKit>
    </div>
    
     <rs-button variant="warning" class="w-68" style="margin-left: 9%;">Update</rs-button> 
      &nbsp;&nbsp;&nbsp;
     <nuxt-link :to="`/usermanagement/student`">    
        <rs-button variant="primary" class="w-68" style="margin-left: 2%;margin-top: -4.6%;">Cancel</rs-button>
     </nuxt-link>

  </rs-card>

  <!--- DATATABLE  -->
  <rs-card
    class="flex-wrap justify-between p-5 bg-white text-black rounded-md flex-col"
  >
    <template #header>
      <div class="flex">List of Student</div>
    </template>

    <!-- TABLE LIST STUDENT -->
    <rs-table v-if="data && data.length > 0"
      :field="field"
      :data="data"
      :options="{
        variant: 'default',
        striped: true,
        bordered: true,
        borderless: true,
        hover: true,
        fixed: false,
      }"
      advanced
    >
    <template v-slot:Id="data" >
        <p class="">
          {{ data.value.id }}
        </p>
      </template>

      <template v-slot:FullName="data" >
        <p class="">
          {{ data.value.fullname }}
        </p>
      </template>

      <template v-slot:Nric="data" >
        <p class="">
          {{ data.value.nric }}
        </p>
      </template>

      <template v-slot:WalletNumber="data" >
        <p class="">
          {{ data.value.walletNo }}
        </p>
      </template>

      <template v-slot:Status="data" >
        <rs-badge variant="success" v-if="data.value.status == 'Active'">Aktif</rs-badge>
        <rs-badge variant="danger" v-else>Tidak Aktif</rs-badge>
      </template>

      <template v-slot:Action="data">
        <div class="flex flex-row">
          <nuxt-link :to="``" class="ml-2">
            <rs-button variant="danger">
              <Icon name="material-symbols:delete-outline"></Icon>
            </rs-button>
          </nuxt-link>
        </div>  
        
      </template>

    </rs-table>
    <div v-else class="">
      <rs-empty-table :field="field"></rs-empty-table>        
    </div>
  </rs-card>
</template>
