<template>
  <div class="container-fluid">
    <table class="table table-bordered">
      <thead>
        <tr>
          <th v-for="column in columns" @click="sortData(sortColumn[$index])" :class="{'cansort': sortColumn[$index]}">{{column}}<span class="glyphicon" :class="{'glyphicon-menu-down': sortColumn[$index] === sort.key && sort.val === -1,'glyphicon-menu-up': sortColumn[$index] === sort.key && sort.val === 1  }"></span></th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="tr in data | orderBy sort.key sort.val | limitBy record currentPage*record ">
          <td v-for="td in tr">{{td}}</td>
        </tr>
      </tbody>
    </table>
    <ul class="pagination pagination-sm">
      <li>
        <a href="javascript:void(0);" aria-label="Previous" @click="preOrNext(0)">
          <span aria-hidden="true">&laquo;</span>
        </a>
      </li>
      <li :class="{'active': n-1 == currentPage}" v-show="currentPage > 7">
        <a href="javascript:void(0);" @click="changePage(0)">
          1
          <span class="sr-only">(current)</span>
        </a>
      </li>
      <li :class="{'active': n-1 == currentPage}" v-for="n in tabPageNum">
        <a href="javascript:void(0);" @click="changePage(n-1)">
          {{n}}
          <span class="sr-only">(current)</span>
        </a>
      </li>
      <li :class="{'active': n-1 == currentPage}" v-show="currentPage < pageNum - 5 && pageNum > 9">
        <a href="javascript:void(0);" @click="changePage(pageNum - 1)">
          {{pageNum}}
          <span class="sr-only">(current)</span>
        </a>
      </li>
      <li>
        <a href="javascript:void(0);" aria-label="Next" @click="preOrNext(1)">
          <span aria-hidden="true">&raquo;</span>
        </a>
      </li>
      <li>
        <a href="javascript:void(0);">
          共{{ pageNum }}页
          <span aria-hidden="true"></span>
        </a>
      </li>
    </ul>
  </div>
</template>

<script>
  export default {
    data () {
      return {
        currentPage: 0,
        sort: {
          key: '',
          val: 1
        }
      }
    },
    props: {
      columns: {
        type: Array
      },
      data: {
        type: Array
      },
      record: {
        type: Number,
        default: 10
      },
      sortColumn: {
        type: Array,
        default: () => {
          return []
        }
      }
    },
    computed: {
      pageNum () {
        return Math.ceil(this.data.length / this.record)
      },
      tabPageNum () {
        let left = 1
        let right = this.pageNum
        let ar = []
        if (this.pageNum >= 11) {
          if (this.currentPage > 7 && this.currentPage < this.pageNum - 5) {
            left = this.currentPage - 4
            right = this.currentPage + 2
          } else {
            if (this.currentPage <= 7) {
              left = 1
              right = 9
            } else {
              right = this.pageNum
              left = this.pageNum - 7
            }
          }
        }
        while (left <= right) {
          ar.push(left)
          left++
        }
        return ar
      }
    },
    methods: {
      changePage (index) {
        this.currentPage = index
      },
      preOrNext (toPre) {
        if ((this.currentPage === 0 && !toPre) || (this.currentPage + 1 === this.pageNum && toPre)) return
        toPre ? this.currentPage = this.currentPage + 1 : this.currentPage = this.currentPage - 1
      },
      sortData (name) {
        if (!this.sortColumn || this.sortColumn.length === 0) return
        if (!name) return
        this.sort = {
          key: name,
          val: -this.sort.val
        }
      }
    },
    watch: {
      data () {
        this.currentPage = 0
        this.sort = {
          key: '',
          val: 1
        }
      }
    }
  }
</script>

<style scoped>
  .container-fluid {
    position: relative;
  }
  table {
    background-color: #fff;
  }
  .cansort {
    cursor: pointer;
  }
  .pagination {
    position: absolute;
    top: -53px;
    right: 15px;
  }
</style>
