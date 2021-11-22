
<template>
    <div class="knime-search">
        <input 
            class="search-input" 
            v-model="searchValue" 
            type="text"
            placeholder="Add new node..."
        >
        <ul class="search-list">
            <li
                v-for="node in searchNodes" 
                :key="node.id" 
                :value="node" 
                @mousedown="select(node)"
            >
                <KnimeNode :value="node" />
                <div class="search-node-details">
                    <div>{{node.path}}</div>
                    <div>{{node.name}}</div>
                    <div>{{node.description}}</div>
                </div>
            </li>
        </ul>
    </div>
</template>

<script>
import KnimeNode from "../KnimeNode/"
import { SELECT } from "../../../constants/events"

export default {
  name: 'KnimeSearch',
  props: {
      nodeList: { type: Array, default: () => [] }
  },
  data: function () {
      return {
          searchValue: ''
      }
  },
  computed: {
      // Return nodes from list that match search query
      searchNodes () {
        if (this.searchValue) {
            // Create RegExp to test nodes with ignore case, `i`, flag
            const regExpQuery = new RegExp(this.searchValue, 'i')
            // Filter by name or path
            return this.nodeList.filter(node => regExpQuery.test(node.name) || regExpQuery.test(node.path))
        }
        // Return the initial list when search query is empty
        return this.nodeList
      }
  },
  created () {
  },
  methods: {
      select(node) {
          this.$emit(SELECT, node)
      }
  },
  components: {
      KnimeNode
  }
}
</script>

<style scoped>
    .knime-search {
        width: 100%;
        max-width: 400px;
        background-color: #fff;
        border-radius: var(--global-radius);
        border: 1px solid #A1A1A1;
        overflow: hidden;
        box-shadow: 0px 3px 10px rgba(0, 0, 0, 0.1);
        height: min-content;
    }

    .search-input {
        all: unset;
        height: calc(var(--global-node-height) - 2px);
        width: 100%;
        box-shadow: 0 1px 0 #F2F2F2;
        padding: 0 var(--global-gap-x);
    }

    .search-list {
        all: unset;
        display: block;
        max-height: 0;
        overflow: auto;
        transition: max-height var(--global-duration-short) ease;
    }

    .knime-search:focus-within .search-list {
        max-height: calc(var(--global-node-height) * 3 + var(--global-gap-y) * 6);
    }

    .search-list > li {
        padding: var(--global-gap-y) var(--global-gap-x);
        display: flex;
        opacity: 0;
        transition: opacity var(--global-duration-short) ease;
    }

    .search-list > li:hover {
        background-color: rgba(0, 0, 0, 0.05);
    }

    .knime-search:focus-within .search-list > li {
        opacity: 1;
    }

    .search-node-details {
        display: flex;
        flex-direction: column;
        line-height: 1;
        justify-content: center;
        padding-left: var(--global-gap-x);
    }

    .search-node-details > div:nth-child(1) {
        color: #CEA94B;
        font-size: var(--global-text-sm);
    }

    .search-node-details > div:nth-child(2) {
        font-size: var(--global-text-md);
    }

    .search-node-details > div:nth-child(3) {
        color: #9E9E9E;
        font-size: var(--global-text-sm);
    }
</style>
