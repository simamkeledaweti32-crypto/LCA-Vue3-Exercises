<template>
  <div class="container">
    <h1>FlexCore Fitness Scheduler</h1>
    
    <div class="stats">
      <div class="stat-card">
        <div class="stat-number">{{ sessions.length }}</div>
        <div>Sessions Scheduled</div>
      </div>
      <div class="stat-card">
        <div class="stat-number">{{ totalCapacity }}</div>
        <div>Total Spots</div>
      </div>
    </div>
    
    <div class="form-card">
      <h2 style="margin-bottom: 15px;">Add New Class</h2>
      <div class="form-group">
        <label>Class Name</label>
        <input v-model="newSession.name" placeholder="e.g. Yoga Flow" />
        <div v-if="errors.name" class="error">{{ errors.name }}</div>
      </div>
      <div class="form-group">
        <label>Instructor</label>
        <input v-model="newSession.instructor" placeholder="e.g. Sarah" />
        <div v-if="errors.instructor" class="error">{{ errors.instructor }}</div>
      </div>
      <div class="form-group">
        <label>Time</label>
        <input v-model="newSession.time" type="time" />
        <div v-if="errors.time" class="error">{{ errors.time }}</div>
      </div>
      <div class="form-group">
        <label>Duration (minutes)</label>
        <input v-model.number="newSession.duration" type="number" min="1" />
        <div v-if="errors.duration" class="error">{{ errors.duration }}</div>
      </div>
      <div class="form-group">
        <label>Capacity</label>
        <input v-model.number="newSession.capacity" type="number" min="1" />
        <div v-if="errors.capacity" class="error">{{ errors.capacity }}</div>
      </div>
      <button class="create-btn" @click="addSession">Create Session</button>
    </div>
    
    <div v-if="sessions.length === 0" class="empty-msg">
      <h3>No sessions scheduled yet</h3>
      <p>Add your first class session above</p>
    </div>
    
    <div v-else>
      <div class="session-card" v-for="session in sessions" :key="session.id">
        <div class="session-info">
          <h3>{{ session.name }}</h3>
          <p>Instructor: {{ session.instructor }} | Time: {{ session.time }} | Duration: {{ session.duration }}min | Capacity: {{ session.capacity }}</p>
        </div>
        <button class="delete-btn" @click="deleteSession(session.id)">Cancel</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      sessions: [],
      newSession: {
        name: '',
        instructor: '',
        time: '',
        duration: '',
        capacity: ''
      },
      errors: {}
    }
  },
  computed: {
    totalCapacity() {
      return this.sessions.reduce((sum, s) => sum + s.capacity, 0);
    }
  },
  methods: {
    addSession() {
      this.errors = {};
      
      if (!this.newSession.name) this.errors.name = 'Class name is required';
      if (!this.newSession.instructor) this.errors.instructor = 'Instructor is required';
      if (!this.newSession.time) this.errors.time = 'Time is required';
      if (!this.newSession.duration || this.newSession.duration < 1) this.errors.duration = 'Duration must be at least 1 minute';
      if (!this.newSession.capacity || this.newSession.capacity < 1) this.errors.capacity = 'Capacity must be at least 1';
      
      if (Object.keys(this.errors).length > 0) return;
      
      this.sessions.push({
        id: Date.now(),
        ...this.newSession
      });
      
      this.newSession = { name: '', instructor: '', time: '', duration: '', capacity: '' };
    },
    deleteSession(id) {
      this.sessions = this.sessions.filter(s => s.id !== id);
    }
  }
}
</script>
