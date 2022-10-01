<script setup lang="ts">
  import Hero from './Hero.vue'
  import HeaderComponent from './HeaderComponent.vue'
  
  const router = useRouter();
  const { navigation, prev, next, page, toc } = useContent()
  useContentHead(page)
  const navigationLinks = [
  {
    title: 'Introduction',
    links: [
      { title: 'Getting started', href: '/' },
      { title: 'Installation', href: '/installation' },
    ],
  },
  {
    title: 'Core concepts',
    links: [
      { title: 'Understanding caching', href: '/understanding-caching' },
      {
        title: 'Predicting user behavior',
        href: '/predicting-user-behavior',
      },
      { title: 'Basics of time-travel', href: '/basics-of-time-travel' },
      {
        title: 'Introduction to string theory',
        href: '/introduction-to-string-theory',
      },
      { title: 'The butterfly effect', href: '/the-butterfly-effect' },
    ],
  },
  {
    title: 'Advanced guides',
    links: [
      { title: 'Writing plugins', href: '/writing-plugins' },
      { title: 'Neuralink integration', href: '/neuralink-integration' },
      { title: 'Temporal paradoxes', href: '/temporal-paradoxes' },
      { title: 'Testing', href: '/testing' },
      { title: 'Compile-time caching', href: '/compile-time-caching' },
      {
        title: 'Predictive data generation',
        href: '/predictive-data-generation',
      },
    ],
  },
  {
    title: 'API reference',
    links: [
      { title: 'CacheAdvance.predict()', href: '/cacheadvance-predict' },
      { title: 'CacheAdvance.flush()', href: '/cacheadvance-flush' },
      { title: 'CacheAdvance.revert()', href: '/cacheadvance-revert' },
      { title: 'CacheAdvance.regret()', href: '/cacheadvance-regret' },
    ],
  },
  {
    title: 'Contributing',
    links: [
      { title: 'How to contribute', href: '/how-to-contribute' },
      { title: 'Architecture guide', href: '/architecture-guide' },
      { title: 'Design principles', href: '/design-principles' },
    ],
  },
]
  let currentSection = navigationLinks.find((section) =>
    section.links.find((link) => link.href === router.currentRoute.value.path)
  )  

  function isActive(section) {
    if (section.id === currentSection) {
      return true
    }
    if (!section.children) {
      return false
    }
    return section.children.findIndex(isActive) > -1
  }

  let isHomePage = router.currentRoute.value.path === '/'
</script>

<template>
  <HeaderComponent :navigation="navigationLinks" />

  <Hero v-if="isHomePage"/>

  <div class="relative mx-auto flex max-w-8xl justify-center sm:px-2 lg:px-8 xl:px-12">
    <div class="hidden lg:relative lg:block lg:flex-none">
      <div class="absolute inset-y-0 right-0 w-[50vw] bg-slate-50 dark:hidden" />
      <div class="sticky top-[4.5rem] -ml-0.5 h-[calc(100vh-4.5rem)] overflow-y-auto py-16 pl-0.5">
        <div class="absolute top-16 bottom-0 right-0 hidden h-12 w-px bg-gradient-to-t from-slate-800 dark:block" />
        <div class="absolute top-28 bottom-0 right-0 hidden w-px bg-slate-800 dark:block" />
        <!-- <Navigation
          navigation="navigation.value"
          class="w-64 pr-8 xl:w-72 xl:pr-16"
        /> -->
      </div>
    </div>
    <div class="min-w-0 max-w-2xl flex-auto px-4 py-16 lg:max-w-none lg:pr-0 lg:pl-8 xl:px-16">
      <article>
          <header v-if="currentSection.title || page.title" class="mb-9 space-y-1">
              <p v-if="currentSection" class="font-display text-sm font-medium text-sky-500">
                {{currentSection.title}}
              </p>
              <h1 v-if="page" class="font-display text-3xl tracking-tight text-slate-900 dark:text-white">
                {{page.title}}
              </h1>
          </header>
      <ContentDoc />
      </article>
      <dl class="mt-12 flex border-t border-slate-200 pt-6 dark:border-slate-800">
        <div v-if="prev.title">
          <dt class="font-display text-sm font-medium text-slate-900 dark:text-white">
            Previous
          </dt>
          <dd class="mt-1">
            <NuxtLink
              :to="prev._path"
              class="text-base font-semibold text-slate-500 hover:text-slate-600 dark:text-slate-400 dark:hover:text-slate-300"
            >
              <span aria-hidden="true">&larr;</span> {{prev.title}}
            </NuxtLink>
          </dd>
        </div>
        <div v-if="next.title" class="ml-auto text-right">
          <dt class="font-display text-sm font-medium text-slate-900 dark:text-white">
            Next
          </dt>
          <dd class="mt-1">
            <NuxtLink
              :to="next._path"
              class="text-base font-semibold text-slate-500 hover:text-slate-600 dark:text-slate-400 dark:hover:text-slate-300"
            > 
              {{next.title}} <span aria-hidden="true">&rarr;</span>
            </NuxtLink>
          </dd>
        </div>
      </dl>
    </div>
    <div class="hidden xl:sticky xl:top-[4.5rem] xl:-mr-6 xl:block xl:h-[calc(100vh-4.5rem)] xl:flex-none xl:overflow-y-auto xl:py-16 xl:pr-6">
      <nav class="w-56" aria-labelledby="on-this-page-title">
            <div v-if="toc.links.length > 0">
            <h2
              id="on-this-page-title"
              class="font-display text-sm font-medium text-slate-900 dark:text-white"
            >
              On this page
            </h2>
            <ol role="list" class="mt-4 space-y-3 text-sm">
              <li v-for="section in toc.links" :key="section.id">
                <h3>
                  <NuxtLink 
                    :to="`#${section.id}`"
                    :class="[
                        isActive(section)
                          ? 'text-sky-500'
                          : 'font-normal text-slate-500 hover:text-slate-700 dark:text-slate-400 dark:hover:text-slate-300']"                  >
                    {{section.text}}
                  </NuxtLink>
                </h3>
                <ol
                  v-if="section.children.length > 0"
                  role="list"
                  class="mt-2 space-y-3 pl-5 text-slate-500 dark:text-slate-400"
                >
                  <li
                    v-for="subSection in section.children"
                    :key="subSection.id">
                    <NuxtLink
                      :to="`#${subSection.id}`"
                      :class="
                        isActive(subSection)
                          ? 'text-sky-500'
                          : 'hover:text-slate-600 dark:hover:text-slate-300'">
                      {{subSection.text}}
                    </NuxtLink>
                  </li>
                </ol>
              </li>
              <!-- {tableOfContents.map((section) => (
                <li key={section.id}>
                  <h3>
                    <Link
                      href={`#${section.id}`}
                      class={[
                        isActive(section)
                          ? 'text-sky-500'
                          : 'font-normal text-slate-500 hover:text-slate-700 dark:text-slate-400 dark:hover:text-slate-300'
                      )]
                    >
                      {section.title}
                    </Link>
                  </h3>
                  {section.children.length > 0 && (
                    <ol
                      role="list"
                      class="mt-2 space-y-3 pl-5 text-slate-500 dark:text-slate-400"
                    >
                      {section.children.map((subSection) => (
                        <li key={subSection.id}>
                          <Link
                            href={`#${subSection.id}`}
                            class={
                              isActive(subSection)
                                ? 'text-sky-500'
                                : 'hover:text-slate-600 dark:hover:text-slate-300'
                            }
                          >
                            {subSection.title}
                          </Link>
                        </li>
                      ))}
                    </ol>
                  )}
                </li>
              ))} -->
            </ol>
          </div>
      </nav>
    </div>
  </div>
</template>
