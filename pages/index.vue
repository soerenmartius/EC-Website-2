<template lang="pug">
.section-wrapper(v-if='pages')
  div
    v-img.hero-image.hellGrau.align-end.angle--bottom-right(
      :src='require("~/assets/img/hero-image.jpg")',
      height='400',
      width='auto',
      min-width='100%',
      gradient='180deg, rgba(0,0,0,0.16) 0%, rgba(0,0,0,0.02) 16%, rgba(0,0,0,0.02) 80%, rgba(0,0,0,0.48) 100%'
    )
      v-container.countdown.pb-0.pb-md-1.pb-lg-2.pb-xl-4
        v-row(justify='center', no-gutters)
          v-col(cols='12', md='7')
            v-card.px-3.ec-gradient.text-center.pt-4.pb-8(tile)
              span.text-h6.pb-5.white--text Die Anmeldephase hat begonnen!
              //- ec-countdown(target='2020-11-08T14:00:00Z', keep-zeros)
              //-   template(v-slot:digits='slotProp')
              //-     span.text-h4.font-weight-bold.white--text(slot='digits') {{ slotProp.digits }}
              //-   template(v-slot:units='slotProp')
              //-     span.text-caption.text-uppercase.white--text(slot='units') {{ slotProp.unit }}
    v-container.mb-4
      .d-flex.flex-row.justify-space-between.align-end
        h2#aktuelles Aktuelles
        v-btn(
          text,
          depressed,
          tile,
          large,
          to='/blog/',
          aria-label='Mehr Beiträge anzeigen'
        )
          span.hidden-xs-only Mehr Beiträge
          v-icon.ml-1.mr-n1 mdi-arrow-right
      v-row.mb-4
        v-col(
          cols='12',
          sm='6',
          md='4',
          v-for='item in pages.recentPosts',
          :key='item.slug'
        )
          v-card(tile, hover, outlined, :to='`/blog/${item.slug}`')
            ec-image-item.hellGrau(
              :image='item.featuredImage',
              :title='item.title',
              :subTitle='`Vom ${item.published.split("T")[0].split("-").reverse().join(".")}`'
            )
      .d-flex.flex-row.justify-space-between.align-end
        h2(id='nächste-veranstaltungen') Nächste Veranstaltungen
        v-btn(
          text,
          depressed,
          tile,
          large,
          to='/veranstaltungen/',
          aria-label='Mehr Veranstaltungen anzeigen'
        )
          span.hidden-xs-only Mehr Veranstaltungen
          v-icon.ml-1.mr-n1 mdi-arrow-right
      v-row.mb-4
        v-col(
          cols='12',
          sm='6',
          md='4',
          v-for='item in pages.upcomingEvents',
          :key='item.slug'
        )
          v-card(tile, hover, outlined, :to='`/veranstaltungen/${item.slug}`')
            ec-image-item.hellGrau(
              :image='item.featuredImage.split(".")[0] + (supportWebp() ? ".webp" : ".jpg")',
              :title='item.title',
              :subTitle='`Vom ${item.begin.split("-").reverse().join(".")} bis ${item.ende.split("-").reverse().join(".")}`'
            )
  .angle--both-left-right(style='background: #f5f5f5;')
    v-container
      h2(id='über-uns') Über uns
      //- p 
        | Der EC-Nordbund ist einer von 18 Landesverbänden des Deutschen EC-Verbandes.
        | EC bedeutet: „Entschieden für Christus“ und markiert die grundsätzlich evangelische Ausrichtung aller Aktivitäten.
        | Im EC-Nordbund sind alle EC-Kinder- und Jugendarbeiten aus Schleswig-Holstein und Hamburg.
      p
        | Die EC-Arbeit in Deutschland hat den Auftrag,
        | junge Menschen zu Jüngern zu machen
        | und sie zu prägenden Persönlichkeiten heranzubilden,
        | durch die wiederum Menschen ihrer Generation
        | zu Jüngern werden.
      p
        | Der EC-Nordbund ist einer der 18 Landesverbänden des Deutschen EC-Verbandes. Im EC-Nordbund sind alle EC-Kinder- und Jugendarbeiten aus Schleswig-Holstein und Hamburg vereint.
      p
        | EC bedeutet: „Entschieden für Christus“ und markiert die Aurichtung auf Jesus in allen unseren Aktivitäten.
      p
        | Der EC-Nordbund arbeitet eng mit dem Verband der Gemeinschaften in der Evangelischen Kirche in Schleswig-Holstein e.V. (kurz VG) zusammen. Wir betreiben gemeinsam das Erholungs- und Bildungszentrum Wittensee (kurz EBZ) und unser Ferienlager in Karlsminde (bei Eckernförde).
      p
        | Der EC-Nordbund basiert als Gemeinnütziger Verein auf Ehrenamt wir haben nur 2 Hauptamtliche Mitarbeiter.
      v-row
        v-col.person(align='center', @click='mail("referent@ec-nordbund.de")')
          v-img.hexagon-shape(
            :src='require("~/assets/img/thomas_seeger.jpg")',
            :width='128',
            :height='128'
          )
            .hexa-image-overlay(v-ripple)
          .text-h6 Thomas Seeger
          | Jugendreferent
        v-col.person(
          align='center',
          @click='mail("kinder-referent@ec-nordbund.de")'
        )
          v-img.hexagon-shape(
            :src='require("~/assets/img/dortje_gaertner.jpg")',
            :width='128',
            :height='128'
          )
            .hexa-image-overlay(v-ripple)
          .text-h6 Dortje Gaertner
          | Kinder- und Jungschararbeit
p(v-else) Loading...
</template>
<style lang="scss" scoped>
@import '~vuetify/src/styles/settings/_variables';

.hero-image {
  height: calc(100vh + 3.492vw - 96px);

  @media #{map-get($display-breakpoints, 'md-and-up')} {
    height: 400px;
  }
}

.section-wrapper > div:last-child {
  &.angle--bottom-left,
  &.angle--bottom-right,
  &.angle--both-right-right,
  &.angle--both-left-right,
  &.angle--both-right-left,
  &.angle--both-left-left {
    margin-bottom: -3.492vw;
  }
}

.countdown {
  margin-bottom: -3.493vw;

  .v-sheet {
    box-shadow: 0px 3px 1px -2px rgba(0, 0, 0, 0.2),
      0px 2px 2px 0px rgba(0, 0, 0, 0.14), 0px 1px 5px 0px rgba(0, 0, 0, 0.12),
      0 11px 15px -7px rgba(0, 0, 0, 0.2), 0 24px 38px 3px rgba(0, 0, 0, 0.14),
      0 9px 46px 8px rgba(0, 0, 0, 0.12) !important;
  }
}

.hexagon-shape {
  clip-path: polygon(50% 100%, 5% 75%, 5% 25%, 50% 0%, 95% 25%, 95% 75%);
}

.hexa-image-overlay {
  height: 128px;
  background: var(--v-primary-base);
  opacity: 0;
  will-change: opacity;
  transition: opacity 0.3s;
}

.person {
  cursor: pointer;

  // transition: background-color .3s;
  &:hover {
    // background-color: var(--v-primary-base);

    & .hexa-image-overlay {
      opacity: 0.7;
    }
  }
}
</style>
<script>
import {
  defineComponent,
  useContext,
  useAsync,
  ssrRef,
  computed,
} from '@nuxtjs/composition-api'
import { supportWebp } from '../helpers/webp'
export default defineComponent({
  setup() {
    const { $content } = useContext()

    const pages_loading = useAsync(async () => {
      const upcomingEvents = await $content('veranstaltung')
        .only(['slug', 'title', 'begin', 'ende', 'featuredImage', 'tags'])
        .sortBy('begin') // TODO: compare to today's date
        .limit(3)
        .fetch()

      const recentPosts = await $content('blog')
        .only([
          'title',
          'tags',
          'description',
          'featuredImage',
          'slug',
          'published',
        ])
        .sortBy('published', 'desc')
        .limit(3)
        .fetch()

      return { upcomingEvents, recentPosts }
    })

    const pages = computed(() =>
      pages_loading.value
        ? pages_loading.value
        : { upcomingEvents: [], recentPosts: [] }
    )

    return { pages, supportWebp, mail: (m) => (location.href = `mailto:${m}`) }
  },
  head: {
    title: 'Startseite',
    meta: [
      {
        hid: 'description',
        name: 'description',
        content:
          'Die EC-Arbeit in Deutschland hat den Auftrag, junge Menschen zu Jüngern zu machen und sie zu prägenden Persönlichkeiten heranzubilden, durch die wiederum Menschen ihrer Generation zu Jüngern werden. Der EC-Nordbund ist einer der 18 Landesverbänden des Deutschen EC-Verbandes. Im EC-Nordbund sind alle EC-Kinder- und Jugendarbeiten aus Schleswig-Holstein und Hamburg vereint. EC bedeutet: „Entschieden für Christus“ und markiert die Aurichtung auf Jesus in allen unseren Aktivitäten.',
      },
      // Open Graph
      { hid: 'og:title', property: 'og:title', content: 'EC-Nordbund' },
      {
        hid: 'og:description',
        property: 'og:description',
        content:
          'Die EC-Arbeit in Deutschland hat den Auftrag, junge Menschen zu Jüngern zu machen und sie zu prägenden Persönlichkeiten heranzubilden, durch die wiederum Menschen ihrer Generation zu Jüngern werden. Der EC-Nordbund ist einer der 18 Landesverbänden des Deutschen EC-Verbandes. Im EC-Nordbund sind alle EC-Kinder- und Jugendarbeiten aus Schleswig-Holstein und Hamburg vereint. EC bedeutet: „Entschieden für Christus“ und markiert die Aurichtung auf Jesus in allen unseren Aktivitäten.',
      },
      // Twitter Card
      {
        hid: 'twitter:title',
        name: 'twitter:title',
        content: 'EC-Nordbund!',
      },
      {
        hid: 'twitter:description',
        name: 'twitter:description',
        content:
          'Die EC-Arbeit in Deutschland hat den Auftrag, junge Menschen zu Jüngern zu machen und sie zu prägenden Persönlichkeiten heranzubilden, durch die wiederum Menschen ihrer Generation zu Jüngern werden. Der EC-Nordbund ist einer der 18 Landesverbänden des Deutschen EC-Verbandes. Im EC-Nordbund sind alle EC-Kinder- und Jugendarbeiten aus Schleswig-Holstein und Hamburg vereint. EC bedeutet: „Entschieden für Christus“ und markiert die Aurichtung auf Jesus in allen unseren Aktivitäten.',
      },
    ],
  },
})
</script>