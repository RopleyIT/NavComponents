# NavComponents collapsible menu layout
This project contains an implementation of a simple alternative Blazor layout that has a collapsible left vertical menu bar. The menu bar either just has icons in a narrow column, or can be expanded to include captions alongside these icons.

The menu items are integrated with the Blazor navigation manager so that clicking them navigates to a selected URI, being a component labeled with an `@page` directive at the top.

## Use

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

## Nested menus

Instead of an item in the nav bar being associated with a link to a page, 
it is possible to make it become an expand/collapse button for a set of
grouped link items beneath it, accordion-style.

These expand/collapse buttons are implemented as `<NavContext>` components,
and implement the following set of attributes:
| Attribute | Value |
| --------- | ----- |
| `Icon`    | The name of the icon to be used alongside the label. This can be one of the bootstrap icons (name starting `bi-`), open icons (name starting `oi-`) glyph icons (name starting `glyphicon-`) or font awesome icons (names starting with `fa-`).   |
| `Label`   |  The textual label to appear alongside the icon if the expand/collapse button is not collapsed.  |

## Example of use

The following shows an example of how to layout a two-level nav stack
based on the Microsoft default sample Blazor project. This is an excerpt
from the application's `NavStackLoayout.razor` file. There are other layout
related things that need to be done in that file, so do explore the file
itself to see how to configure the menu in an application. Notice how the
nested menu items are contained between the `<NavContext>` open and closing
tags:

```
    <NavStack Collapsed="@collapsed">
        <NavButton Icon="bi-house-door-fill"
        Label="Home"
        Link="" />
        <NavButton Icon="bi-plus"
        Label="Counter"
        Link="counter" />
        <NavContext Icon="bi-house-fill" Label="Children">
            <NavButton Icon="bi-fast-forward-fill"
            Label="Fast forward"
            Link="weather" />
            <NavButton Icon="bi-rewind-fill"
            Label="Backwards"
            Link="" />
        </NavContext>
        <NavButton Icon="bi-cloud-fill"
        Label="Weather"
        Link="weather" />
    </NavStack>
```

## Layout title bar component

Also included in the `Components` folder is a `TopTitle.razor` component. 
This takes child content between its opening and closing tags, and 
automatically puts a bold title in the title bar of the layout. It also 
populates a `<PageTitle/>` Blazor component so that it copies the title 
into the HTML header.