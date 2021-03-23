# CSS Grids
CSS Grid Layout (aka “Grid”), is a two-dimensional grid-based layout system that aims to completely change the way we design grid-based user interfaces. 
## Grid Properties
### Properties for the Parent
* display, Defines the element as a grid container and establishes a new grid formatting context for its contents and its values are:
    * grid – generates a block-level grid
    * inline-grid – generates an inline-level grid
* grid-template-columns and grid-template-rows, Define the columns and rows of the grid with a space-separated list of values. The values represent the track size, and the space between them represents the grid line. These values are:
    * < track-size > – can be a length, a percentage, or a fraction of the free space in the grid (using the fr unit)
    * < line-name > – an arbitrary name of your choosing
* grid-template-columns and grid-template-rows, Define the columns and rows of the grid with a space-separated list of values. The values represent the track size, and the space between them represents the grid line. Values:

    * < track-size > – can be a length, a percentage, or a fraction of the free space in the grid (using the fr unit)
    * < line-name > – an arbitrary name of your choosing
* grid-template, A shorthand for setting grid-template-rows, grid-template-columns, and grid-template-areas in a single declaration. Values:

    * none – sets all three properties to their initial values
    * < grid-template-rows > / < grid-template-columns > – sets grid-template-columns and grid-template-rows to the specified values, respectively, and sets grid-template-areas to none
* column-gap, row-gap, grid-column-gap, grid-row-gap: They Specifies the size of the grid lines. You can think of it like setting the width of the gutters between the columns/rows. Value:

    * < line-size > – a length value
* justify-items, Aligns grid items along the inline (row) axis (as opposed to align-items which aligns along the block (column) axis). This value applies to all grid items inside the container. Values:

    * start – aligns items to be flush with the start edge of their cell
    * end – aligns items to be flush with the end edge of their cell
    * center – aligns items in the center of their cell
    * stretch – fills the whole width of the cell (this is the default)

* align-items, Aligns grid items along the block (column) axis (as opposed to justify-items which aligns along the inline (row) axis). This value applies to all grid items inside the container. Values:

    * start – aligns items to be flush with the start edge of their cell
    * end – aligns items to be flush with the end edge of their cell
    * center – aligns items in the center of their cell
    * stretch – fills the whole height of the cell (this is the default)

* justify-content, Sometimes the total size of your grid might be less than the size of its grid container. This could happen if all of your grid items are sized with non-flexible units like px. In this case you can set the alignment of the grid within the grid container. This property aligns the grid along the inline (row) axis (as opposed to align-content which aligns the grid along the block (column) axis). Values:

    * start – aligns the grid to be flush with the start edge of the grid container
    * end – aligns the grid to be flush with the end edge of the grid container
    * center – aligns the grid in the center of the grid container
    * stretch – resizes the grid items to allow the grid to fill the full width of the grid container
    * space-around - places an even amount of space between each grid item, with half-sized spaces on the far ends
    * space-between – places an even amount of space between each grid item, with no space at the far ends
    * space-evenly – places an even amount of space between each grid item, including the far ends

* align-content, Sometimes the total size of your grid might be less than the size of its grid container. This could happen if all of your grid items are sized with non-flexible units like px. In this case you can set the alignment of the grid within the grid container. This property aligns the grid along the block (column) axis (as opposed to justify-content which aligns the grid along the inline (row) axis). Values:

    * start – aligns the grid to be flush with the start edge of the grid container
    * end – aligns the grid to be flush with the end edge of the grid container
    * center – aligns the grid in the center of the grid container
    * stretch – resizes the grid items to allow the grid to fill the full height of the grid container
    * space-around – places an even amount of space between each grid item, with half-sized spaces on the far ends
    * space-between – places an even amount of space between each grid item, with no space at the far ends
    * space-evenly – places an even amount of space between each grid item, including the far ends

* grid, A shorthand for setting all of the following properties in a single declaration: grid-template-rows, grid-template-columns, grid-template-areas, grid-auto-rows, grid-auto-columns, and grid-auto-flow (Note: You can only specify the explicit or the implicit grid properties in a single grid declaration). Values:

    * none – sets all sub-properties to their initial values.
    * < grid-template> – works the same as the grid-template shorthand.
    * < grid-template-rows> / [ auto-flow && dense? ] <grid-auto-columns>? – sets grid-template-rows to the specified value. If the auto-flow * keyword is to the right of the slash, it sets grid-auto-flow to column. If the dense keyword is specified additionally, the auto-placement algorithm uses a “dense” packing algorithm. If grid-auto-columns is omitted, it is set to auto.
    * [ auto-flow && dense? ] <grid-auto-rows>? / <grid-template-columns> – sets grid-template-columns to the specified value. If the auto-flow * keyword is to the left of the slash, it sets grid-auto-flow to row. If the dense keyword is specified additionally, the auto-placement * algorithm uses a “dense” packing algorithm. If grid-auto-rows is omitted, it is set to auto.

### Properties for the Children
* grid-column-start, grid-column-end, grid-row-start, grid-row-end. Determine a grid item’s location within the grid by referring to specific grid lines. grid-column-start/grid-row-start is the line where the item begins, and grid-column-end/grid-row-end is the line where the item ends. Values:

    * < line> – can be a number to refer to a numbered grid line, or a name to refer to a named grid line
    * span < number> - the item will span across the provided number of grid tracks
    * span < name> – the item will span across until it hits the next line with the provided name
    * auto – indicates auto-placement, an automatic span, or a default span of one
* grid-column and grid-row, Shorthand for grid-column-start + grid-column-end, and grid-row-start + grid-row-end, respectively. Value:

    * < start-line > / < end-line > – each one accepts all the same values as the longhand version, including span
* grid-area, Gives an item a name so that it can be referenced by a template created with the grid-template-areas property. Alternatively, this property can be used as an even shorter shorthand for grid-row-start + grid-column-start + grid-row-end + grid-column-end. Values:

    * < name> – a name of your choosing
    * < row-start> / < column-start> / < row-end> / < column-end> – can be numbers or named lines

* justify-self, Aligns a grid item inside a cell along the inline (row) axis (as opposed to align-self which aligns along the block (column) axis). This value applies to a grid item inside a single cell. Values:

    * start – aligns the grid item to be flush with the start edge of the cell
    * end – aligns the grid item to be flush with the end edge of the cell
    * center – aligns the grid item in the center of the cell
    * stretch – fills the whole width of the cell (this is the default)

* align-self, Aligns a grid item inside a cell along the block (column) axis (as opposed to justify-self which aligns along the inline (row) axis). This value applies to the content inside a single grid item. Values:

    * start – aligns the grid item to be flush with the start edge of the cell
    * end – aligns the grid item to be flush with the end edge of the cell
    * center – aligns the grid item in the center of the cell
    * stretch – fills the whole height of the cell (this is the default)

* place-self, place-self sets both the align-self and justify-self properties in a single declaration. Values:

    * auto – The “default” alignment for the layout mode.
    * < align-self > / < justify-self > – The first value sets align-self, the second value justify-self. If the second value is omitted, the first value is assigned to both properties.
    

