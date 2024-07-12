<script setup>
const accountData = {}

const refInputEl = ref()
const accountDataLocal = ref(structuredClone(accountData))
const isAccountDeactivated = ref(false)
const uploadedFile = ref(null)
const fileDescription = ref("")

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
    <VCard title="Account Details">
      <VCardText class="d-flex">
        <!-- 👉 Avatar -->
        <VAvatar
          rounded="lg"
          size="100"
          class="me-6"
          :image="accountDataLocal.avatarImg"
        />

        <!-- 👉 Upload Photo -->
        <form class="d-flex flex-column justify-center gap-5">
          <div class="d-flex flex-wrap gap-2">
            <VBtn
              color="primary"
              @click="refInputEl?.click()"
            >
              <VIcon
                icon="ri-upload-cloud-line"
                class="d-sm-none"
              />
              <span class="d-none d-sm-block">Upload new file</span>
            </VBtn>

            <input
              ref="refInputEl"
              type="file"
              name="file"
              hidden
              @input="changeAvatar"
            />

            <VBtn
              type="reset"
              color="error"
              variant="outlined"
              @click="resetAvatar"
            >
              <span class="d-none d-sm-block">Reset</span>
              <VIcon
                icon="ri-refresh-line"
                class="d-sm-none"
              />
            </VBtn>
          </div>

          <div v-if="uploadedFile">
            <p class="text-body-1 mb-0">
              File Name: {{ uploadedFile.name }}<br>
              File Size: {{ (uploadedFile.size / 1024).toFixed(2) }} KB
            </p>

          </div>
        </form>
      </VCardText>
      <VDivider />
    </VCard>
  </VCol>
</template>
