<template>
  <d3-network
    ref="d3"
    :net-nodes="nodes"
    :net-links="links"
    :options="options"
    @node-click="onNodeClick"
  />
</template>

<script>
// import d3 from "d3";
import D3Network from "vue-d3-network";

const PATTERN_TYPES = {
  SELECTED_NODE: "selected",
  DIRECT_LINK: "direct-link",
  INDIRECT_LINK: "indirect-link"
};

const COLORS = {
  DIRECT_LINK: "#f53251",
  INDIRECT_LINK: "#03313f",
  SELECTED_NODE: "#fcb827"
};

const SIZES = {
  SELECTED_NODE: 60,
  DIRECT_LINK: 30,
  INDIRECT_LINK: 30
};

export default {
  components: { D3Network },
  props: {
    graph: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      selectedNode: null,
      nodes: [
        {
          id: 1,
          name: "Stitch Data",
          data: {
            location: "United States",
            employees: 140,
            founded: "2016",
            website: "stitchdata.com",
            industry: "Data Management Technology"
          }
        },
        {
          id: 2,
          name: "Stripe",
          data: {
            location: "United States",
            employees: 20,
            founded: "2014",
            website: "stripe.com",
            industry: "Financial Tech"
          }
        },
        {
          id: 3,
          name: "Marketo",
          data: {
            location: "United States",
            employees: 300,
            founded: "2009",
            website: "marketo.com",
            industry: "Marketing Tech"
          }
        },
        {
          id: 4,
          name: "Magento",
          data: {
            location: "United States",
            employees: 400,
            founded: "2012",
            website: "magento.com",
            industry: "Content Management"
          }
        },
        {
          id: 5,
          name: "Adobe",
          data: {
            location: "United States",
            employees: 14000,
            founded: "1990",
            website: "adobe.com",
            industry: "Technology"
          }
        },
        {
          id: 6,
          name: "Google",
          data: {
            location: "United States",
            employees: 43000,
            founded: "1996",
            website: "google.com",
            industry: "Technology"
          }
        },
        {
          id: 7,
          name: "Facebook",
          data: {
            location: "United States",
            employees: 32000,
            founded: "2001",
            website: "facebook.com",
            industry: "Advertising"
          }
        },
        {
          id: 8,
          name: "Twitter",
          data: {
            location: "United States",
            employees: 8900,
            founded: "2002",
            website: "twitter.com",
            industry: "Technology"
          }
        },
        {
          id: 9,
          name: "Oracle",
          data: {
            location: "United States",
            employees: 43000,
            founded: "1994",
            website: "oracle.com",
            industry: "Ruinous M&A"
          }
        },
        {
          id: 10,
          name: "Microsoft",
          data: {
            location: "United States",
            employees: 41231,
            founded: "1982",
            website: "microsoft.com",
            industry: "Technology"
          }
        },
        {
          id: 11,
          name: "Zendesk",
          data: {
            location: "United States",
            employees: 412,
            founded: "2005",
            website: "zendesk.com",
            industry: "SaaS"
          }
        },
        {
          id: 12,
          name: "GitHub",
          data: {
            location: "United States",
            employees: 311,
            founded: "2006",
            website: "github.com",
            industry: "Technology"
          }
        },
        {
          id: 13,
          name: "GitLab",
          data: {
            location: "United States",
            employees: 450,
            founded: "2011",
            website: "gitlab.com",
            industry: "Technology"
          }
        },
        {
          id: 14,
          name: "Trello",
          data: {
            location: "United States",
            employees: 212,
            founded: "2010",
            website: "trello.com",
            industry: "Technology"
          }
        },
        {
          id: 15,
          name: "Intercom",
          data: {
            location: "United States",
            employees: 121,
            founded: "2012",
            website: "intercom.io",
            industry: "Data Management Technology"
          }
        },
        {
          id: 16,
          name: "Amazon Web Services",
          data: {
            location: "United States",
            employees: 9112,
            founded: "2005",
            website: "aws.com",
            industry: "Cloud Provider"
          }
        }
      ],
      links: [
        { sid: 1, tid: 2 },
        { sid: 1, tid: 3 },
        { sid: 1, tid: 4 },
        { sid: 1, tid: 5 },
        { sid: 1, tid: 6 },
        { sid: 1, tid: 7 },
        { sid: 1, tid: 8 },

        { tid: 1, sid: 2 },
        { tid: 1, sid: 3 },
        { tid: 1, sid: 4 },
        { tid: 1, sid: 5 },
        { tid: 1, sid: 6 },
        { tid: 1, sid: 7 },

        { sid: 2, tid: 7 },
        { sid: 2, tid: 8 },
        { sid: 2, tid: 9 },
        { sid: 2, tid: 10 },
        { sid: 2, tid: 11 },
        { sid: 2, tid: 12 },

        { tid: 2, sid: 7 },
        { tid: 2, sid: 8 },
        { tid: 2, sid: 9 },
        { tid: 2, sid: 10 },
        { tid: 2, sid: 11 },
        { tid: 2, sid: 12 },

        { sid: 3, tid: 10 },
        { sid: 3, tid: 11 },
        { sid: 3, tid: 14 },

        { tid: 3, sid: 10 },
        { tid: 3, sid: 11 },
        { tid: 3, sid: 14 },

        { sid: 4, tid: 13 },
        { sid: 4, tid: 15 },
        { sid: 4, tid: 16 },

        { tid: 4, sid: 13 },
        { tid: 4, sid: 15 },
        { tid: 4, sid: 16 }
      ],
      options: {
        force: 1500,
        nodeSize: SIZES.INDIRECT_LINK,
        nodeLabels: true,
        linkWidth: 2,
        canvas: false
      }
    };
  },
  computed: {
    company() {
      return this.graph.root_companies[0];
    },
    allied_company() {
      return this.graph.root_companies.length > 1
        ? this.graph.root_companies[1]
        : null;
    }
  },
  async mounted() {
    let defs = document.createElementNS("http://www.w3.org/2000/svg", "defs");
    await Promise.all(
      this.nodes.map(node => this.createPatterns(defs, node.data.website))
    );

    // let background = document.createElementNS(
    //   "http://www.w3.org/2000/svg",
    //   "circle"
    // );
    // background.setAttribute("r", SIZES.SELECTED_NODE / 2);
    // background.setAttribute("fill", COLORS.DIRECT_LINK);
    // background.setAttribute("cx", SIZES.SELECTED_NODE / 2);
    // background.setAttribute("cy", SIZES.SELECTED_NODE / 2);

    // if (image) {
    //   pattern.appendChild(image);
    // }
    // pattern.appendChild(background);

    // See: http://bl.ocks.org/SpaceActuary/25e72aadac28f2c87667816e82c609db
    this.replaceDefs(defs);
  },
  methods: {
    async createPatterns(defs, domain) {
      await Promise.all(
        Object.keys(PATTERN_TYPES).map(async key => {
          let pattern = document.createElementNS(
            "http://www.w3.org/2000/svg",
            "pattern"
          );
          pattern.setAttribute("id", `${domain}--${PATTERN_TYPES[key]}`);
          pattern.setAttribute("patternUnits", "objectBoundingBox");
          pattern.setAttribute("height", 1);
          pattern.setAttribute("width", 1);

          let background = document.createElementNS(
            "http://www.w3.org/2000/svg",
            "circle"
          );
          background.setAttribute("r", SIZES[key] / 2);
          background.setAttribute("fill", COLORS[key]);
          background.setAttribute("cx", SIZES[key] / 2);
          background.setAttribute("cy", SIZES[key] / 2);
          pattern.appendChild(background)
          
          let image = await this.createImageForSvg(domain, SIZES[key]);
          if (image) {
            pattern.appendChild(image);
          }
          defs.appendChild(pattern);
        })
      );
    },
    async createImageForSvg(domain, size) {
      try {
        let url = `https://logo.clearbit.com/${domain}`;
        let response = await fetch(url);
        if (response.status !== 200) {
          throw new Exception(`Clearbit Logo not found`);
        }
        let image = document.createElementNS(
          "http://www.w3.org/2000/svg",
          "image"
        );
        image.setAttribute("x", 0);
        image.setAttribute("y", 0);
        image.setAttribute("href", url);
        image.setAttribute("height", size);
        image.setAttribute("width", size);
        return image;
      } catch (exception) {
        // If Clearbit 404's, do not create an image tag
        console.log(exception);
        return null;
      }
    },
    replaceDefs(defs) {
      let svg = this.$refs.d3.$el.querySelector("svg");
      let existingDefs = svg.querySelector("defs");
      if (existingDefs) {
        existingDefs.remove();
      }
      svg.insertBefore(defs, svg.childNodes[0]);
    },
    onNodeClick(event, node) {
      this.select(node);
      this.$emit("selected", {
        name: node.name,
        partners: this.partners(node),
        ...node.data
      });
    },
    partners(selectedNode) {
      this.nodes
        .filter(node => this.links.find(link => link.sid === selectedNode.id))
        .map(node => node.data);
    },
    select(node) {
      this.links = this.links.map(link => {
        if (link.sid === node.id || link.tid === node.id) {
          link._svgAttrs = { "stroke-width": 5 };
          link._color = COLORS.DIRECT_LINK;
        } else {
          link._svgAttrs = { "stroke-width": 2 };
          link._color = null;
        }
        return link;
      });
      this.nodes = this.nodes.map(otherNode => {
        let linkExists = this.links.find(
          link =>
            (link.sid === node.id && link.tid === otherNode.id) ||
            (link.tid === node.id && link.sid === otherNode.id)
        );
        if (linkExists || otherNode.id === node.id) {
          otherNode._color = COLORS.DIRECT_LINK;
          if (otherNode.id === node.id) {
            otherNode._color = null;
            otherNode._size = SIZES.SELECTED_NODE;
            otherNode._cssClass = "node--selected";
            otherNode._labelClass = "node__label--selected";
            otherNode._svgAttrs = {
              fill: `url(#${otherNode.data.website}--selected)`,
              style: null
            };
          } else {
            otherNode._color = null;
            otherNode._size = SIZES.DIRECT_LINK;
            otherNode._cssClass = "node--direct-link";
            otherNode._labelClass = "node__label--direct-link";
            otherNode._svgAttrs = {
              fill: `url(#${otherNode.data.website}--direct-link)`,
              style: null
            };
          }
        } else {
          // otherNode._color = COLORS.INDIRECT_LINK;
          otherNode._size = SIZES.INDIRECT_LINK;
          otherNode._cssClass = "node";
          otherNode._labelClass = "node__label";
          otherNode._svgAttrs = {
              fill: `url(#${otherNode.data.website}--indirect-link)`,
              style: null
            };
        }
        return otherNode;
      });
    }
  }
};
</script>
<style lang="scss">
.net {
  height: 100%;
}
.link {
  stroke: var(--navy);
}
.node {
  color: var(--navy);
  &:hover {
    stroke: var(--yellow);
    stroke-width: 4px;
  }
}

.node--selected {
  stroke: var(--yellow);
  stroke-width: 4px;
}

.node__label--selected {
  font-size: 14px;
  font-weight: 500;
}

.node__label--direct-link {
  font-size: 14px;
  font-weight: 500;
}
</style>
