<script lang="ts" setup>

  // Import the "capitalize" function from the "str" module
  import { capitalize } from '~/utils/str'

  // Get the "t" function from the "useLang" composition API
  const { t } = useLang()

  // Define the page metadata
  definePageMeta({
    layout: 'page',
  })

  // Update the page head with a capitalized title and a meta description
  useHead(() => ({
    title: capitalize(t('Projet')),
    meta: [
      {
        name: 'description',
        // The meta description is currently commented out
        // content: t('pages.blank.description'),
      },
    ],
  }))

  // Fetch data from a local API endpoint and store it in the "tests" variable
  const { data: projet } = await useFetch('http://localhost:1337/api/projets')
  const projetData = projet.value

  // If the "projetData" is a reactive proxy, get its raw value
  var rawData = projetData
  if (isProxy(projetData)) {
    rawData = toRaw(projetData)
  }

  // If the "projetData" is null, set the "rawData" variable to an empty object
var rawData = {};
if (projetData) {
  // If the "projetData" is a reactive proxy, get its raw value
  if (isProxy(projetData)) {
    rawData = toRaw(projetData)
  } else {
    rawData = projetData.value
  }
}

const tests = rawData.data

console.log(tests)

</script>

<template>
  <PageWrapper>
    <PageHeader>
      <PageTitle :text="('Projet')" class="capitalize" />
    </PageHeader>
    <PageBody>
      <PageSection>
          <div v-for="test in tests" :key="test.id" class="text-6xl uppercase">
            {{ test.attributes.title }}

            <!-- a résoudre fetch des images -->
            <img src="http://localhost:1337/uploads/cover_Projet1_512fd6a945.jpg" alt="">

            {{ test.attributes.description }}
          </div>
      </PageSection>
    </PageBody>
  </PageWrapper>
</template> 