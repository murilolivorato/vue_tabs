# Building a Customizable Vue.js Tab Component

A comprehensive guide to creating reusable and customizable tab components in Vue.js using composition API, inject/provide, and slots.



<p align="center"><br><br>
<img src="https://miro.medium.com/v2/resize:fit:700/1*6ZXDxCgGrqZnFcpRdBTAzQ.png" alt="Login Page" /><br><br>
</p>

More information -
https://medium.com/@murilolivorato/building-a-customizable-vue-js-tab-component-eab1bad461f0

## Overview

This project demonstrates how to build:
- A reusable tab system
- Dynamic content switching
- Customizable tab components
- Component communication using inject/provide
- Slot-based content rendering

## Features

- Dynamic tab switching
- Customizable tab styling
- Slot-based content rendering
- Component communication
- Responsive design
- Bulma CSS integration
- SCSS support

## Prerequisites

- Node.js (v14 or higher)
- Vue.js 3.x
- npm or yarn
- Basic understanding of Vue.js components
- Basic knowledge of SCSS

## Installation

1. Create a new Vue project:
```bash
npm create vue@latest
```

2. Navigate to project directory:
```bash
cd your-project-name
```

3. Install dependencies:
```bash
# Install Bulma and SASS
npm install bulma
npm install -D sass
```

## Project Structure
```bash
src/
├── components/
│ ├── Tabs/
│ │ ├── Tab.vue
│ │ └── Tabs.vue
│ └── examples/
│ └── TabExample.vue
├── assets/
│ └── styles/
│ └── tabs.scss
└── App.vue
```



## Implementation

### 1. Tab Component
```vue
<!-- src/components/Tabs/Tab.vue -->
<template>
  <div class="tab-content" v-show="value === selectedTitle">
    <slot></slot>
  </div>
</template>

<script>
import { inject } from 'vue'

export default {
  name: 'Tab',
  props: {
    title: {
      type: String,
      required: true
    },
    value: {
      type: String,
      required: true
    },
    active: {
      type: Boolean,
      default: false
    }
  },
  setup() {
    const selectedTitle = inject('selectedTitle')
    return {
      selectedTitle
    }
  }
}
</script>

<style lang="scss" scoped>
.tab-content {
  padding: 1rem;
  border: 1px solid #dbdbdb;
  border-top: none;
  border-radius: 0 0 4px 4px;
}
</style>
```

### 2. Tabs Component
```vue
<!-- src/components/Tabs/Tabs.vue -->
<template>
  <div class="tabs-container">
    <div class="tabs">
      <ul>
        <li 
          v-for="tab in tabs" 
          :key="tab.value"
          :class="{ 'is-active': tab.value === selectedTitle }"
          @click="selectTab(tab.value)"
        >
          <a>{{ tab.title }}</a>
        </li>
      </ul>
    </div>
    <slot></slot>
  </div>
</template>

<script>
import { ref, provide, onMounted } from 'vue'

export default {
  name: 'Tabs',
  props: {
    initialTab: {
      type: String,
      default: ''
    }
  },
  setup(props) {
    const selectedTitle = ref(props.initialTab)
    const tabs = ref([])

    provide('selectedTitle', selectedTitle)

    const selectTab = (value) => {
      selectedTitle.value = value
    }

    onMounted(() => {
      // Get all tab components
      const tabComponents = document.querySelectorAll('.tab-content')
      tabs.value = Array.from(tabComponents).map(tab => ({
        title: tab.getAttribute('data-title'),
        value: tab.getAttribute('data-value')
      }))

      // Set initial tab if not provided
      if (!selectedTitle.value && tabs.value.length > 0) {
        selectedTitle.value = tabs.value[0].value
      }
    })

    return {
      selectedTitle,
      tabs,
      selectTab
    }
  }
}
</script>

<style lang="scss" scoped>
.tabs-container {
  margin: 1rem 0;
}

.tabs {
  ul {
    border-bottom-color: #dbdbdb;
    border-bottom-style: solid;
    border-bottom-width: 1px;
  }

  li {
    margin-bottom: -1px;
    
    &.is-active a {
      border-bottom-color: #485fc7;
      color: #485fc7;
    }

    a {
      border-bottom: 1px solid #dbdbdb;
      margin-bottom: -1px;
      padding: 0.5em 1em;
      cursor: pointer;
      
      &:hover {
        border-bottom-color: #485fc7;
        color: #485fc7;
      }
    }
  }
}
</style>
```

## Usage

### Basic Implementation
```vue
<!-- src/components/examples/TabExample.vue -->
<template>
  <Tabs>
    <Tab title="First Tab" value="tab1">
      <h2>First Tab Content</h2>
      <p>This is the content of the first tab.</p>
    </Tab>
    
    <Tab title="Second Tab" value="tab2">
      <h2>Second Tab Content</h2>
      <p>This is the content of the second tab.</p>
    </Tab>
    
    <Tab title="Third Tab" value="tab3">
      <h2>Third Tab Content</h2>
      <p>This is the content of the third tab.</p>
    </Tab>
  </Tabs>
</template>

<script>
import Tabs from '../Tabs/Tabs.vue'
import Tab from '../Tabs/Tab.vue'

export default {
  name: 'TabExample',
  components: {
    Tabs,
    Tab
  }
}
</script>
```

### With Initial Tab
```vue
<Tabs initial-tab="tab2">
  <Tab title="First Tab" value="tab1">
    Content 1
  </Tab>
  <Tab title="Second Tab" value="tab2">
    Content 2
  </Tab>
</Tabs>
```

## Customization

### Styling
The components use Bulma CSS classes and can be customized using SCSS:

```scss
// src/assets/styles/tabs.scss
.tabs-container {
  // Custom container styles
  .tabs {
    // Custom tabs styles
    ul {
      // Custom ul styles
    }
    li {
      // Custom li styles
      &.is-active {
        // Custom active state styles
      }
    }
  }
}

.tab-content {
  // Custom tab content styles
}
```

### Props

#### Tab Component Props
- `title`: String (required) - The tab title
- `value`: String (required) - The tab value
- `active`: Boolean (optional) - Whether the tab is active by default

#### Tabs Component Props
- `initialTab`: String (optional) - The initially selected tab value

## Best Practices

1. **Component Structure**
   - Keep components focused and single-responsibility
   - Use proper naming conventions
   - Implement proper prop validation

2. **Styling**
   - Use scoped styles
   - Follow BEM naming convention
   - Implement responsive design
   - Use CSS variables for theming

3. **Performance**
   - Use v-show instead of v-if for tab content
   - Implement proper component caching
   - Optimize re-renders


## 👥 Author

For questions, suggestions, or collaboration:
- **Author**: Murilo Livorato
- **GitHub**: [murilolivorato](https://github.com/murilolivorato)
- **linkedIn**: https://www.linkedin.com/in/murilo-livorato-80985a4a/


## 📸 Screenshots

### Login Page
![Login Page](https://miro.medium.com/v2/resize:fit:700/1*7WW7uR_QZVZNPY0Bvi53pQ.png)

### Dashboard
![Dashboard](https://miro.medium.com/v2/resize:fit:700/1*RGq64nAesyDERi8lXOs52g.png)

### Edit Profile
![Edit Profile](https://miro.medium.com/v2/resize:fit:700/1*YEOwx1_C3tV9j0SZqf-T8Q.png)

<div align="center">
  <h3>⭐ Star This Repository ⭐</h3>
  <p>Your support helps us improve and maintain this project!</p>
  <a href="https://github.com/murilolivorato/vue_tabs/stargazers">
    <img src="https://img.shields.io/github/stars/murilolivorato/vue_tabs?style=social" alt="GitHub Stars">
  </a>
</div>
