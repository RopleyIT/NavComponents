# NavComponents collapsible menu layout
This project contains an implementation of a simple alternative Blazor layout that has a collapsible left vertical menu bar. The menu bar either just has icons in a narrow column, or can be expanded to include captions alongside these icons.

The menu items are integrated with the Blazor navigation manager so that clicking them navigates to a selected URI, being a component labeled with an `@page` directive at the top.

##Use
The layout is contained in the files `NavStackLayout.razor` and `NavStackLayout.razor.css` to be found in the `Layout` folder. This can either be used as the layout explicitly by placing the following at the top of any page that wishes to use this layout:
```
@using NavComponents.Components.Layout
@layout NavStackLayout
```
or it can be installed as the default layout manager by altering the `RouteView` element in `Routes.razor` to the following:
```
<RouteView RouteData="routeData" DefaultLayout="typeof(Layout.NavStackLayout)" />
```

Menu items consist of `<NavButton/>` elements inside a `<NavStack />` element.

Each `<NavButton/>` has three attributes that can be set:
| Attribute | Value |
| --------- | ----- |
| `Icon`    | The name of the icon to be used alongside the label. This can be one of the bootstrap icons (name starting `bi-`), open icons (name starting `oi-`) glyph icons (name starting `glyphicon-`) or font awesome icons (names starting with `fa-`).   |
| `Label`   |  The textual label to appear alongside the icon if the menu is not collapsed.  |
| `Link`    |  The link to the page to be displayed in the `@Body` part of the page. The link should match one of the labels found after an `@page` directive on one of the Blazor pages of your application.    |