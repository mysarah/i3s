<script setup>
definePageMeta({
  title: "Manage School Holiday",
  
});

const data = [
  {
    "Holiday Name": "Cuti Sukan",
    "Start Date": "31/08/2024",
    "End Date": "31/08/2024",
    "School": "SK Saujana Impian 2, MRSM Lenggong",
    "Status": "Expired",
    "Action": ""
  },
]

const ModalDeleteSchoolHoliday = ref(false);
const showModalDeleteForm = ref({
  holiday_name: "Cuti Sukan",
});


</script>
<template>
  <div>
    <div>
      <div class="flex justify-between">
        <h4 class="mb-4 uppercase"></h4>
      </div>
      <rs-card class="py-5">
        <div class="flex flex-col md:flex-row justify-between items-start md:items-center gap-y-2 px-5">
          <div>
            <h5 class="font-semibold">School Holiday</h5>
            <span class="text-sm text-gray-500">
              Below is the list of all school holiday
            </span>
          </div>

          <nuxt-link to="/settings/school-holiday/add">
            <rs-button class="mb-4" variant = "warning">
              <Icon name="fe:plus" class="mr-1" />
              Add School Holiday
            </rs-button>
          </nuxt-link>
            
        </div>

        <rs-table
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
          class="mt-4"
        >
        <template v-slot:Status="data" >
          <rs-badge variant="success" v-if="data.value.status == 'Active'">Aktif</rs-badge>
          <rs-badge variant="danger" v-else>Expired</rs-badge>
        </template>

        <template v-slot:Action="data">
          <div class="flex flex-row gap-x-2">
            <div class="flex items-center gap-x-2">
              <nuxt-link :to="`/settings/school-holiday/edit/[id]`">
                <rs-button variant="warning">
                  <Icon name="material-symbols:edit-outline" /> 
                </rs-button>
              </nuxt-link>
            </div>
            <div class="flex items-center gap-x-2">
              <nuxt-link :to="``">
                <rs-button variant="danger" @click = "ModalDeleteSchoolHoliday = true" >
                  <Icon name="material-symbols:delete-outline" /> 
                </rs-button>
              </nuxt-link>
            </div>
          </div>
        </template>
        </rs-table>
      </rs-card>

      <rs-modal title="Delete Confirmation" ok-title="Yes" cancel-title="No" :ok-callback="delete" v-model = "ModalDeleteSchoolHoliday">
      <p>
        Are you sure want to delete this name ({{ showModalDeleteForm.holiday_name }})?
      </p>
    </rs-modal>

    </div>
  </div>
</template>
