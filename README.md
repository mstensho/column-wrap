# Column wrapping

In multi-column (multicol) layout, content is fragmented into columns. When one column is full, another is created next to it, in the inline direction. If the block-size of the multicol container is unconstrained, and there are no forced breaks inside the columns, there will not be more columns than specified via the `column-width` and/or `column-count` CSS properties. If block-size is constrained by a specified size on the multicol container, and the multicol container isn't nested inside another fragmentation context (e.g. printing establishes a fragmentation context), there may be need for more columns than specified. Such additional columns will simply be created in the inline direction, overflowing the multicol container. If block-size is constrained by an outer fragmentation context, when paginating for printing, for instance, columns will take up all the available block-size on the page, and create at most as many columns as specified (still via `column-count` and `column-width`). If that's not enough to fit all the content, a page break will be inserted, and multicol layout will resume on the next page. This is essentially implicit column wrapping.

The new `column-wrap` property is intended to enable column wrapping in other scenarios than for nested multicol. If the value of `column-wrap` is `wrap`, and all the specified amount of columns have been filled in the inline direction, instead keeping going in the inline direction and overflowing the multicol container, a new row for columns will be created, so that more content can be added *below* the previous columns. The block-size of the rows can be set via the new `column-height` property. If it is `auto`, the block-size of the content box will be used instead. Treating `auto` like this is useful for scrollable overflow, so that there's room for one row of columns in the scrollport.

Column layout, and especially column layout with lots of content, where the order of the content matters [1], has been particularly useful for paged media (where it wraps into bite-size chunks, aka pages), whereas for interactive media on screen it's not as useful. Having to scroll all the way back up to the beginning of the next column is tedious. Adding column wrapping should allow for large-content use cases on screen as well.

[1] Wikipedia uses multicol for the references at the end of articles, and the columns become really tall if there are many references, but that's not a problem, since the order here isn't crucial.
