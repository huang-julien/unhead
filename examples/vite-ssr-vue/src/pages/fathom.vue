<script lang="ts" setup>
import { onMounted } from 'vue'
import { useScript } from '@unhead/vue'

export interface FathomAnalyticsApi {
  beacon: (ctx: { url: string, referrer?: string }) => void
  blockTrackingForMe: () => void
  enableTrackingForMe: () => void
  isTrackingEnabled: () => boolean
  send: (type: string, data: unknown) => void
  setSite: (siteId: string) => void
  siteId: string
  trackPageview: (ctx?: { url: string, referrer?: string }) => void
  trackGoal: (goalId: string, cents: number) => void
  trackEvent: (eventName: string, value: { _value: number }) => void
}

const { trackPageview, blockTrackingForMe, siteId } = useScript<FathomAnalyticsApi>({
  src: 'https://cdn.usefathom.com/script.js',
  ['data-site']: 'KGILBQDV',
}, {
  use() {
    return window.fathom
  },
})

blockTrackingForMe()
trackPageview({
  url: '/test',
  referrer: '',
})
onMounted(async () => {
  console.log(siteId, await siteId())
})
</script>
<template>
<div>test</div>
</template>
