# rapm-project

The purpose of this repo is to create a foundation for an interactive data visualization dashboard webpage using [**DC.js**](https://dc-js.github.io/dc.js/), [**D3.js**](https://d3js.org/) and [**crossfilter.js**](https://square.github.io/crossfilter/).

## Setup

This repo uses **Jekyll**, which you will need to set up with **Ruby** if you wish to run this page locally. Information on how to set up a **Jekyll** site [can be found here](https://jekyllrb.com/docs/).

The local site can be run with:

```
bundle exec jekyll serve
```

## Loading Data

Data is loaded through the `_data/` folder, in **.yaml** format. If your data is in [**json**](https://www.json2yaml.com/) or [**csv**](http://convertcsv.com/csv-to-yaml.htm) formats, you can find websites to perform conversions by clicking on the corresponding hyperlinks.

After dropping your data file into `_data/`, we will add a short [**liquid** script](https://shopify.github.io/liquid/) into `data/` to load it as a **json** file. The benefits of loading data this way ensures that only the variables we need will be loaded. For instance, here is `data/music.json`, which reads from `_data/music.yaml`:

```
---
layout: none
---
[{% for chart in site.data.music %}
  {
    "id": "{{ chart.id }}",
    "date": "{{ chart.date }}",
    "pub_city": "{{ chart.place-of-publication }}",
    "genre": "{{ chart.style }}",
    "affiliation": "{{ chart.current-affiliation-author-primary-1 }}",
    "gender": "{{ chart.Gender }}",
    "language": "{{ chart.Language }}",
    "source_genre": "{{ chart.source-genre-folder }}"
  }{% if forloop.last == false %},{% endif %}
{% endfor %}]
```

The loop iterates over `site.data.music`, which is equivalent to `_data/music.yaml`. From there, we map key values from the **yaml** file to a **json** with new key names (`place-of-publication` becomes `pub_city`, etc).

After loading data like this, we then can access it by referencing it as `/data/music.json`. An example of this can be seen in `music-test-charts-dc/index.html`, where we load the data with **D3.js**:

```
d3.json("/data/music.json").then(function(data) {
// code here
}
```

## Further Development

Work on this repo is not complete. The dashboard formatting needs to be rectified, with a **css** framework such as [Bootstrap](https://getbootstrap.com/), so that the graphs are more aligned, and react to different browser window sizes.

This dashboard can be adapted to display different data sets by using the methods above, as well as use different charts that were not used in this dashboard. [Different types of charts, with examples, can be found here](https://dc-js.github.io/dc.js/examples/).
