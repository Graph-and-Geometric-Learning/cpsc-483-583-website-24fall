<template>
  <v-container>
    <v-row>
      <v-col>
        <v-table>
          <thead>
            <tr>
              <th>Date</th>
              <th>Lecture</th>
              <th>Slides</th>
              <th>Recording</th>
              <th>Readings</th>
              <th>Assignment</th>
              <th>Deadlines</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="item in items">
              <td>{{ item.date }}</td>
              <td>
                {{ item.lecture }}
                <a v-if="item.date === 'Mon 10/02'" href="https://yale.zoom.us/j/94207787464?from=addon">[Zoom]</a>
              </td>
              <td><a v-if="item.slide" :href="item.slide">[slide]</a></td>
              <td><a v-if="item.recording" :href="item.recording">[recording]</a></td>
              <td>{{ item.reading }}</td>
              <td>
              <div v-if="item.hw">
                {{ item.hw.name }} released <a :href="item.hw.pdf">[pdf]</a> <a :href="item.hw.zip">[zip]</a>
              </div>
              <br v-if="item.colab" />
              <div v-if="item.colab">
              <a target="_blank" :href="item.colab.url">
                <img src="https://colab.research.google.com/assets/colab-badge.svg" :alt="item.colab.name" />
              </a>
                <!-- {{ item.colab.name }} released <a :href="item.colab.url">[ipynb]</a> -->
              </div>

              </td>
              <td>{{ item.deadline }}</td>
            </tr>
          </tbody>
        </v-table>
      </v-col>
    </v-row>
  </v-container>
</template>

<script lang="ts">
import HelloWorld from "@/components/HelloWorld.vue";
import { defineComponent } from "vue";

interface HW {
  name: string,
  pdf: string,
  zip: string,
}

interface Colab {
  name: string,
  url: string,
}

interface Item {
  date: string;
  lecture: string;
  slide?: string;
  reading?: string;
  event?: string;
  deadline?: string;
  hw?: HW;
  colab?: Colab;
  recording?: string;
}

enum EventType {
  homework,
  colab,
}

var items: Item[] = [
  {
    "date": "Wed 08/28",
    "lecture": "Introduction",
    slide: "https://yaleedu-my.sharepoint.com/:b:/g/personal/rex_ying_yale_edu/EYJG3bz_K9NKlTVN4dUEDvwBvkR_Zr70aSTumbze55AdRA",
    recording: "https://yale.zoom.us/rec/share/ZfE4JpS8Cn89Q4y2n_c6SNMskydJuK4LOhtpd96X0FlTCKPZzUYlAKECSDgy1ga9.acNVUGRt658ZkIuS",
  },
  {
    "date": "Fri 08/30",
    "lecture": "Graph Learning Tasks",
    slide: "https://yaleedu-my.sharepoint.com/:b:/g/personal/rex_ying_yale_edu/EZq9BTaRaKJLrhXWV_P-KeABQlyQVwrb6zrPGt2HAA5kqA?e=qEyfed",
    hw: {
      name: "HW1",
      pdf: import.meta.env.BASE_URL + "assignment_1.pdf",
      zip: import.meta.env.BASE_URL + "assignment_1.zip",
    },
  },
  {
    "date": "Wed 09/04",
    "lecture": "Deep Learning Background and GNN basics",
    slide: "https://yaleedu-my.sharepoint.com/:b:/g/personal/rex_ying_yale_edu/EVYWpzh4wuNCj09z_7UDSwgBQ7fW2wbthcnMzS7h1zK4lQ?e=CgREVg",
    colab: {
      name: "Colab1",
      url: "https://colab.research.google.com/github/Graph-and-Geometric-Learning/cpsc483-583-website-24fall/blob/gh-pages/colab1.ipynb",
    },
  },
  {
    "date": "Mon 09/09",
    "lecture": "Graph Neural Networks Designs",
    slide: "https://yaleedu-my.sharepoint.com/:b:/g/personal/rex_ying_yale_edu/ET2VRlrqey9Drn6jB90qva4BBGcMBWATYz2EbIYw4EmV9A?e=HlkaeY",
  },
  {
    "date": "Mon 09/16",
    "lecture": "GNN Implementations, Objectives and Loss Functions",
    slide: "https://yaleedu-my.sharepoint.com/:b:/g/personal/rex_ying_yale_edu/EUV-P3eRkwRNreVBp9YlZ4sBQz_cCScQviMTJ7ALHSFtqQ?e=4yGMol",
  },
  {
    "date": "Wed 09/18",
    "lecture": "Scalable GNN Architectures",
    slide: "https://yaleedu-my.sharepoint.com/:b:/g/personal/rex_ying_yale_edu/ERY5igrXpbRMtpmYSsZFEcQBdZWxKNUOflI1bI6YKMdg1Q?e=xvS6qD",
  },
  {
    "date": "Fri 09/20",
    "lecture": "No classes",
    deadline: "Colab 1 Due",
    hw: {
      name: "HW2",
      pdf: import.meta.env.BASE_URL + "assignment_2.pdf",
      zip: import.meta.env.BASE_URL + "assignment_2.zip",
    },
  },
  {
    "date": "Mon 09/23",
    "lecture": "Graph Attention Networks and Heterogeneous graphs",
    slide: "https://yaleedu-my.sharepoint.com/:b:/g/personal/rex_ying_yale_edu/EZVvAZLiBlxJrZJBYa0Owf4BEieEIfsuVdfR1irb_742eg?e=VsLNRk",
  },
  {
    "date": "Wed 09/25",
    "lecture": "GNNs and Transformers"
  },
  {
    "date": "Mon 09/30",
    "lecture": "Theory of Graph Neural Networks"
  },
  {
    "date": "Wed 10/02",
    "lecture": "Guest Lecture 1"
  },
  {
    date: "Fri 10/04",
    "lecture": "No classes",
  },
  {
    "date": "Mon 10/07",
    "lecture": "GNN Expressive Power",
    deadline: "HW2 Due"
  },
  {
    "date": "Wed 10/09",
    "lecture": "GNN Expressive Power (2)"
  },
  {
    "date": "Mon 10/14",
    "lecture": "Graph Learning Tools"
  },
  {
    "date": "Mon 10/21",
    "lecture": "Graph Transformers"
  },
  {
    "date": "Wed 10/23",
    "lecture": "Self-supervised Learning with GNNs"
  },
  {
    "date": "Mon 10/28",
    "lecture": "Foundation models and Pre-trained GNNs"
  },
  {
    "date": "Wed 10/30",
    "lecture": "Explaining GNN Predictions"
  },
  {
    "date": "Mon 11/04",
    "lecture": "Guest Lecture 2 (applications)"
  },
  {
    "date": "Wed 11/06",
    "lecture": "Distributed Node Embeddings"
  },
  {
    "date": "Mon 11/11",
    "lecture": "Knowledge Graph Reasoning"
  },
  {
    "date": "Wed 11/13",
    "lecture": "Hyperbolic Embeddings and Hyperbolic GNNs"
  },
  {
    "date": "Mon 11/18",
    "lecture": "Advanced non-Euclidean Models"
  },
  {
    "date": "Wed 11/20",
    "lecture": "Graph Generative Models"
  },
  {
    "date": "Mon 12/02",
    "lecture": "Multimodal Graph Learning"
  },
  {
    date: "Wed 12/04",
    "lecture": "Applications in Graphics, Neuroscience and Scientific Simulations"
  }

];

export default defineComponent({
  name: "Syllabus",

  data: () => ({
    items: items,
  }),
  methods: {
    baseName(str) {
      var base = new String(str).substring(str.lastIndexOf("/") + 1);
      if (base.lastIndexOf(".") != -1)
        base = base.substring(0, base.lastIndexOf("."));
      return base;
    },
  },
});
</script>
