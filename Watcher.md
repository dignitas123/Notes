watch(data, (currentValue, oldValue) => {
  console.log(currentValue);
  console.log(oldValue);
});

Ein Array watchen

import { watch, ref } from "vue";
export default defineComponent({
  setup() {
    const level = ref([1, 2, 3, 4]);
    watch(() => [...level.value], (currentValue, oldValue) => {
      console.log(currentValue);
      console.log(oldValue);
    });
  },
});

Deep nested array watchen

import { watch, ref } from "vue";
import _ from "lodash";
export default {
  setup() {
    const secondLevel = ref([5, 6, 7]);
    const level = ref([1, 2, 3, 4, secondLevel.value]);

    watch(() => _.cloneDeep(level.value), (currentValue, oldValue) => {
        console.log(currentValue);
        console.log(oldValue);
      }
    );
  },
};

Spezifische Eigenschaft eines reactive Objekts waschen

import { reactive, toRefs, watch } from 'vue'
export default {
  setup() {
    const state = reactive({
      name: "",
    })
    watch(() => state.name, (currentValue, oldValue) => {
      console.log(currentValue)      
      console.log(oldValue)
    })
  }
}

Den watcher vor Component Unmount stoppen:

const stop = watchEffect(() => {
  /* ... */
})

// later
stop()

Jegliches Component update abfangen mit watchEffect

watchEffect(() => {
      // Funktion triggert vor component update
	console.log(“component is updating”)
    })

Oder

watchEffect(() => {
	// Funktion triggert nach component update
	console.log(“component was updated”)
},
{
flush: ‘post’
})

async data load mit computed property und composable


export default defineComponent({
  setup() {
    const products = reactive([]);
    onMounted(() => {
      loadProducts();
    });
    const loadProducts = async () {
      try {
        const productsSnap = await graphQLProductRequest()
      } catch (e) {
        console.log("Error Loading Products");
      }
    }
    return {
      products,
    };
  },
});

// wiederverwertbares "composable"
import { reactive, toRefs } from "vue";
import graphQL from "apolloGraphQL";

// dieser state ist global persisted, products müssen nicht neugeladen werden
const state = reactive({
  products: [],
});

export default function useProduct() {
  const loadProducts = async() => {
    try {
      const products = await graphQLQuery();
      products.forEach(doc => {
        state.products.push(product);
      });
    } catch (e) {
      console.log("Error Loading Products")
    }
  }
  // durch ...toRefs wird ein destrukturierbares Javascript Objekt erstellt (nützlich für mehr als 1 state)
  return { ...toRefs(state),
    loadProducts
  }
}

// 
import { onMounted } from "vue";
import useProduct from "@/modules/product";
export default {
  setup() {
    const { products, loadProducts } = useProduct(); // man kann auch nur products laden
    onMounted(async () => {
      await loadProducts();
    });
    return {
      products,
    };
  },
};
