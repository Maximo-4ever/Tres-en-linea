<template>
  <div class="flex items-center justify-center h-screen relative">
    <div v-if="game.winner" class="absolute top-0 left-0 text-3xl p-4">
      El ganador es: {{ game.winner }}
    </div>
    <div class="grid grid-cols-3 w-[300px] h-[300px] gap-3">
      <div
        v-for="({ icon }, index) in configuration.grid"
        :key="index"
        class="bg-gray-100 p-8 relative flex items-center justify-center hover:cursor-pointer"
        @click="event(index)"
      >
        <div
          class="absolute flex items-center justify-center"
          v-html="icon"
        ></div>
      </div>
    </div>
  </div>
</template>

<script>
import { winner } from '@/util/game'

export default {
  name: 'IndexPage',
  data() {
    return {
      configuration: {
        grid: [
          { icon: '', element: '' },
          { icon: '', element: '' },
          { icon: '', element: '' },
          { icon: '', element: '' },
          { icon: '', element: '' },
          { icon: '', element: '' },
          { icon: '', element: '' },
          { icon: '', element: '' },
          { icon: '', element: '' },
        ],
        isGaming: true,
        elements: {
          x: '<svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" style="fill: rgba(0, 0, 0, 1);transform: ;msFilter:;"><path d="m16.192 6.344-4.243 4.242-4.242-4.242-1.414 1.414L10.535 12l-4.242 4.242 1.414 1.414 4.242-4.242 4.243 4.242 1.414-1.414L13.364 12l4.242-4.242z"></path></svg>',
          0: '<svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" style="fill: rgba(0, 0, 0, 1);transform: ;msFilter:;"><path d="M5 12c0 3.859 3.14 7 7 7 3.859 0 7-3.141 7-7s-3.141-7-7-7c-3.86 0-7 3.141-7 7zm12 0c0 2.757-2.243 5-5 5s-5-2.243-5-5 2.243-5 5-5 5 2.243 5 5z"></path></svg>',
        },
      },
      game: {
        zero: false,
        winner: null,
      },
    }
  },
  methods: {
    event(index) {
      if (this.configuration.grid[index].element === '') {
        this.game.zero = !this.game.zero
        if (!this.game.zero) {
          this.configuration.grid.splice(index, 1, {
            icon: this.configuration.elements.x,
            element: 'x',
          })
        } else {
          this.configuration.grid.splice(index, 1, {
            icon: this.configuration.elements['0'],
            element: '0',
          })
        }
        if (winner(this.configuration.grid)) {
          const { element } = winner(this.configuration.grid)
          this.game.winner = element
        }
      }
    },
  },
}
</script>
