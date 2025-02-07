<template>
  <div
    v-if="isVisible || delayMilliseconds === 0"
    :class="{ 'w-100': type !== 'spinner' }"
    class="d-flex flex-wrap">
    <CardSkeleton
      v-if="type === 'card'"
      :card-count="cardCount ">
      <template slot="card-header">
        <slot name="card-header" />
      </template>
      <template slot="card-content">
        <slot name="card-content" />
      </template>
      <template slot="card-footer">
        <slot name="card-footer" />
      </template>
    </CardSkeleton>
    <TableSkeleton
      v-else-if="type === 'table'"
      :columns="tableColumns"
      :rows="tableRows">
      <slot />
    </TableSkeleton>
    <FormSkeleton v-else-if="type === 'form'"/>
    <FullScreenKongSkeleton
      v-else-if="type === 'fullscreen-kong'"
      :progress="progress"/>
    <KIcon
      v-else-if="type === 'spinner'"
      icon="spinner"
      view-box="0 0 16 16"
      color="#000"/>
    <Skeleton v-else />
  </div>
</template>

<script>
import Skeleton from './Skeleton'
import CardSkeleton from './CardSkeleton'
import TableSkeleton from './TableSkeleton'
import FormSkeleton from './FormSkeleton'
import FullScreenKongSkeleton from './FullScreenKongSkeleton'
import KIcon from '@kongponents/kicon/KIcon.vue'

export default {
  name: 'KSkeleton',
  components: {
    Skeleton,
    CardSkeleton,
    TableSkeleton,
    FormSkeleton,
    FullScreenKongSkeleton,
    KIcon
  },
  props: {
    delayMilliseconds: {
      type: Number,
      required: false,
      default: 750
    },
    type: {
      type: String,
      default: '',
      validator: (val) => [
        'table',
        'card',
        'form',
        'spinner',
        'fullscreen-kong',
        '' // default Skeleton.vue
      ].indexOf(val) !== -1
    },
    progress: {
      type: Number,
      required: false,
      default: null
    },
    cardCount: {
      type: Number,
      default: 1
    },
    tableColumns: {
      type: Number,
      required: false,
      default: 6
    },
    tableRows: {
      type: Number,
      required: false,
      default: 6
    }
  },
  data () {
    return {
      isVisible: false
    }
  },

  mounted () {
    setTimeout(() => {
      this.isVisible = true
    }, this.delayMilliseconds)
  }
}
</script>
