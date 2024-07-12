<script setup>
const accountData = {}

const refInputEl = ref()
const accountDataLocal = ref(structuredClone(accountData))
const isAccountDeactivated = ref(false)
const uploadedFile = ref(null)
const fileDescription = ref("")
const FileType = [
  "csv",
  "Excel",


 
]

const changeAvatar = file => {
  const fileReader = new FileReader()
  const { files } = file.target
  if (files && files.length) {
    uploadedFile.value = files[0]
    fileReader.readAsDataURL(files[0])
    fileReader.onload = () => {
      if (typeof fileReader.result === 'string') {
        accountDataLocal.value.avatarImg = fileReader.result
      }
    }
  }
}

const resetAvatar = () => {
  uploadedFile.value = null
  fileDescription.value = ""
  accountDataLocal.value.avatarImg = accountData.avatarImg
}
</script>

<template>
  <VCol cols="12">
    <VCard title="File Type">
  
        <form class="d-flex flex-column justify-center gap-5">
          <div class="d-flex flex-wrap gap-2">
  <v-select
    v-model="fileDescription"
    :items="FileType"
    label="File Type "
    outlined
    class="mt-3"
  ></v-select>
</div>


    
        </form>
      <VDivider />
    </VCard>
  </VCol>
</template>
