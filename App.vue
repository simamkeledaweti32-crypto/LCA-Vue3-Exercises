<template>
  <div>
    <header>
      <h1>Homes & Beyond</h1>
      <p>{{ filteredProperties.length }} Properties Available in Cape Town</p>
    </header>
    
    <div class="controls">
      <input v-model="searchQuery" placeholder="Search by title or location..." />
      <select v-model="sortOrder">
        <option value="asc">Price: Low to High</option>
        <option value="desc">Price: High to Low</option>
      </select>
    </div>
    
    <div class="properties-grid">
      <div class="property-card" v-for="property in filteredProperties" :key="property.id">
        <div v-if="!property.available" class="ribbon">Not Available</div>
        <img :src="property.image" :alt="property.title" />
        <div class="property-info">
          <h3 class="property-title">{{ property.title }}</h3>
          <div class="property-price">R{{ property.price }}/night</div>
          <div class="property-location">📍 {{ property.location }}</div>
          <div class="property-type">🏠 {{ property.type }}</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      searchQuery: '',
      sortOrder: 'asc',
      properties: [
        {
          id: 1,
          title: "Sea Point Apartment",
          price: 850,
          location: "Sea Point",
          type: "Apartment",
          image: "https://images.unsplash.com/photo-1560448204-e02f11c3d0e2?w=400",
          available: true
        },
        {
          id: 2,
          title: "Camps Bay Villa",
          price: 2200,
          location: "Camps Bay",
          type: "Villa",
          image: "https://images.unsplash.com/photo-1512917774080-9991f1c4c750?w=400",
          available: true
        },
        {
          id: 3,
          title: "Bo-Kaap Cottage",
          price: 650,
          location: "Bo-Kaap",
          type: "Cottage",
          image: "https://images.unsplash.com/photo-1502672023488-70e25813eb80?w=400",
          available: false
        },
        {
          id: 4,
          title: "Clifton Studio",
          price: 1200,
          location: "Clifton",
          type: "Studio",
          image: "https://images.unsplash.com/photo-1522708323590-d24dbb6b0267?w=400",
          available: true
        },
        {
          id: 5,
          title: "Constantia House",
          price: 1800,
          location: "Constantia",
          type: "House",
          image: "https://images.unsplash.com/photo-1571896349842-33c89424b32d?w=400",
          available: true
        },
        {
          id: 6,
          title: "Woodstock Loft",
          price: 750,
          location: "Woodstock",
          type: "Loft",
          image: "https://images.unsplash.com/photo-1493809842364-78817add7ffb?w=400",
          available: false
        }
      ]
    }
  },
  computed: {
    filteredProperties() {
      let filtered = this.properties.filter(p => 
        p.title.toLowerCase().includes(this.searchQuery.toLowerCase()) ||
        p.location.toLowerCase().includes(this.searchQuery.toLowerCase())
      );
      
      return filtered.sort((a, b) => {
        return this.sortOrder === 'asc' ? a.price - b.price : b.price - a.price;
      });
    }
  }
}
</script>
