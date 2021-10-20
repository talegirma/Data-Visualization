# Data-Visualization
require(dplyr)
zonal <- mutate(zonal, np_diff = abs(X64N.90N - Glob), sp_diff = abs(X90S.64S - Glob), eq_diff = abs(X24S.24N - Glob))

require(plotly)

y_axis <- list(title = "Difference in .01 degrees", showgrid = TRUE)
x_axis <- list(title = "")
sub_legend <- list(orientation = "h", x = 0.25, y = -0.2)

n_difference <- plot_ly(data = zonal, x = ~Year) %>%
   add_trace(y = ~np_diff, mode = 'lines', name = "North pole") %>%
   layout(title = "North pole", xaxis = x_axis)

s_difference <- plot_ly(data = zonal, x = ~Year) %>%
   add_trace(y = ~sp_diff, mode = 'lines', name = "South pole") %>%
   layout(title = "South pole", xaxis = x_axis)

eq_difference <- plot_ly(data = zonal, x = ~Year) %>%
   add_trace(y = ~eq_diff, mode = 'lines', name = "Equator") %>%
   layout(title = "Equator")

subplot(
   s_difference,
   eq_difference,
   n_difference,
   shareX = TRUE, shareY = TRUE, nrows = 1
) %>%
   layout(title = "Absolute difference of temperature change with global average", yaxis = y_axis, legend = sub_legend)
