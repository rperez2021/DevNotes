## UI/UX Best Practices from Pencil & Paper IO

Part of this info comes from this guide: [pencilandpaper.io](https://pencilandpaper.io/articles/ux-pattern-analysis-enterprise-data-tables/)

- Left Align Text Columns
- Match Heading Alignment to Columns
- Don't ever use center alignment
- Avoid duplication of words between Headers and Content
- Right align quantitative numberical values (money, quantities, measures, percentages)
- Qualitative numbers can be left aligned (dates, postal codes, phone numbers)
- Lots more check out that article

## Styling Tips and Helper Elements & Attributes

### The `<col>` & `<colgroup>` Elements

These can be used to style entire columns without having to style individual `<td>` or `<th>` elements.

Styling columns like this is limited to a few properties: border, background, width, and visibility. To set other properties you'll have to either style every `<td>` or `<th>` in the column, or use a complex selector such as `:nth-child`.

The attribute `span` can also be used inside a `<col>` element to expand the styling size.

### The `colspan` and `rowspan` attributed

Allow us to expand a `<th>` or `<td>` element across several rows or columns.

<table>
  <tr>
    <th colspan="2">Animals</th>
  </tr>
  <tr>
    <th colspan="2">Hippopotamus</th>
  </tr>
  <tr>
    <th rowspan="2">Horse</th>
    <td>Mare</td>
  </tr>
  <tr>
    <td>Stallion</td>
  </tr>
  <tr>
    <th colspan="2">Crocodile</th>
  </tr>
  <tr>
    <th rowspan="2">Chicken</th>
    <td>Hen</td>
  </tr>
  <tr>
    <td>Rooster</td>
  </tr>
</table>

## A11y Concerns and Helpers

### The `<caption>` Element

You can give your table a caption by putting it inside a `<caption>` element and nesting that inside the `<table>` element. You should put it just below the opening `<table>` tag.

### The `<thead>`, `<tfoor>` and `<tbody>` Elements

These elements don't make the table any more accessible to screenreader users, and don't result in any visual enhancement on their own. They are however very useful for styling and layout — acting as useful hooks for adding CSS to your table.

### The `scope` Attribute

The Scope attribute, which can be added to the `<th>` element to tell screenreaders exactly what cells the header is a header for can use the scope attribute with values like `colgroup`, `rowgroup`, `col` or `row` to help screenreders determine what these subheadings are for.

### Using `id` and `header` Attributes

An alternative to using the scope attribute is to use id and headers attributes to create associations between headers and cells. The way they are used is as follows:

- You add a unique id to each <th> element.
- You add a headers attribute to each <td> element. Each headers attribute has to contain a list of the ids of all the <th> elements that act as a header for that cell, separated by spaces.
