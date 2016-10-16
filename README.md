_[Demo and API docs](https://chaspi.github.io/chaspi-grid/)_

##&lt;chaspi-grid&gt;

`<chaspi-grid>` is a simple html table which dynamically renders itself according to the bind data.

To achieve this dynamic behavior, a column model must be provided. This column model knows about how to get the
data out of the main model to place it in the table cell. It can be defined by using the `<chaspi-col>` element.

In the most simple case the property attribute defines the name of the property on the row data which belongs to the cell:

    <chaspi-col property="name"></chaspi-col>

By providing a cell renderer function, more complex things can be done:

    <chaspi-col cell-renderer="{{myRenderer}}"></chaspi-col>

    ready : function() {
        this.myRenderer = function(item) {
            return {
                content: item.name,
                style: 'font-weight:bold;',
                class: 'myClass'
            }
        }
    }

Because `<chaspi-col>` is nothing else than a table <col> element. The `<chaspi-col>` must be grouped
within a `<chaspi-colgroup>` element. `<chaspi-colgroup>` itself must be a child of `<chaspi-grid>`:

    <chaspi-grid items="{{items}}">
        <chaspi-colgroup>
            <chaspi-col property="name"></chaspi-col>
            <chaspi-col property="start"></chaspi-col>
            <chaspi-col property="end"></chaspi-col>
        </chaspi-colgroup>
    </chaspi-grid>

The above snipped is already enough to display following data in the grid:

    ready : function() {
        this.items = [
            {name: 'Breakfast', start: '10:00', end: '10:15'},
            {name: 'Lunch', start: '13:00', end: '14:00'},
            {name: 'Dinner', start: '19:00', end: '20:00'}
        ]
    }

The grid can also contain headers and footers:

    <chaspi-grid>
        ...
        <chaspi-header>
            <chaspi-row>
                <chaspi-cell>Event</chaspi-cell>
                <chaspi-cell>Start Time</chaspi-cell>
                <chaspi-cell>End Time</chaspi-cell>
            </chaspi-row>
        </chaspi-header>
        <chaspi-footer>
            <chaspi-row>
                <chaspi-cell>...</chaspi-cell>
                ...

The current implementation does not use `<table>`, `<tr>`, `<td>` elements. Instead it uses `<div>` elements and the 
table elements corresponding display CSS property. This is because IE and FF do not support `dom-repeat` inside a
`<table>` element. Therefore the grid cannot support colspan at the moment.

### Styling

Style the grid with CSS as you would a normal DOM element.

To style the header:

    chaspi-header {
        padding: 10px;
    }

To style all columns

    chaspi-col {
        border-right: thin solid grey;
    }

`<chaspi-row>` provides the following custom properties and mixins for styling:

Custom property | Description | Default
----------------|-------------|----------
`--chaspi-row` | Style of the rows it the table | `{}`
`--chaspi-cell` | Style of cells in the table | `{}`