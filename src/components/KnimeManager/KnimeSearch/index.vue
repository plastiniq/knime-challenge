
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
            // Filter by name or ID
            return this.nodeList.filter(node => regExpQuery.test(node.name) || regExpQuery.test(node.id))
        }
        // Return the initial list when search query is empty
        return this.nodeList
      }
  },
  created () {
  },
  methods: {
  },
  components: {
      KnimeNode
  }
}
</script>

<style scoped>
    .knime-search {
        position: absolute;
        max-width: 100%;
        width: 385px;
        background-color: #fff;
        border-radius: var(--global-radius);
        border: 1px solid #A1A1A1;
        overflow: hidden;
    }

    .knime-search:focus-within {
        transition: box-shadow var(--global-duration-short);
        box-shadow: 0px 3px 10px rgba(0, 0, 0, 0.1);
    }

    .search-input {
        all: unset;
        height: var(--global-node-height);
        width: 100%;
        padding: 0 var(--global-gap-x);
        box-shadow: 0 1px 0 #F2F2F2;
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

    .knime-search:focus-within .search-list > li {
        opacity: 1;
    }

    .search-node-details {
        display: flex;
        flex-direction: column;
    }
</style>
