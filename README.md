﻿<h2 align="center">Responsive.Avalonia - Use Breakpoints in AvaloniaUI</h2>

<p align="center">
    <img src="https://img.shields.io/nuget/v/Responsive.Avalonia?color=1f72de" alt="Nuget">
    <img src="https://img.shields.io/badge/-.NET%20Standard%202.0-blueviolet?color=1f72de&label=NET" alt="">
    <img src="https://img.shields.io/github/license/russkyc/responsive-avalonia">
    <img src="https://img.shields.io/github/issues/russkyc/responsive-avalonia">
    <img src="https://img.shields.io/nuget/dt/Responsive.Avalonia">
</p>

## Overview

Responsive.Avalonia is a library that provides responsive breakpoints for AvaloniaUI applications. It allows developers
to create responsive layouts that adapt to different screen sizes using predefined breakpoints.

## Features

> [!NOTE]
> Custom conditions can now be added by using the `Condition` property of the `Show` control. Read more in this section: [Custom Conditions](#custom-conditions).

- **Predefined Breakpoints**: Use predefined breakpoints such as `Xs`, `Sm`, `Md`, `Lg`, `Xl`, and `Xxl`.
- **Customizable Visibility**: Control the visibility of UI elements based on the current screen width.
- **Easy Integration**: Simple to integrate into existing AvaloniaUI projects.

## Installation

You can install the library via NuGet Package Manager:

```sh
dotnet add package Responsive.Avalonia
```

## Usage

Add Namespace

```xaml
xmlns:rc="using:Responsive.Avalonia"
```

There are two controls needed to be used. The `BreakpointProvider` is the root that detects
the width changes, and the `Show` control contains the elements that will be shown when the width
is within the breakpoint.

```xml

<rc:BreakpointProvider>
    <rc:Show Breakpoint="Xs">
        <TextBlock HorizontalAlignment="Center" VerticalAlignment="Center" Foreground="White"
                   FontWeight="Medium" FontSize="14" Text="Visible on Small Screens"/>
    </rc:Show>
    <rc:Show Breakpoint="Sm">
        <TextBlock HorizontalAlignment="Center" VerticalAlignment="Center" Foreground="White"
                   FontWeight="Medium" FontSize="24" Text="Visible on Medium Screens"/>
    </rc:Show>
    <rc:Show Breakpoint="MdAndUp">
        <TextBlock HorizontalAlignment="Center" VerticalAlignment="Center" Foreground="White"
                   FontWeight="Medium" FontSize="38" Text="Visible on Large Screens"/>
    </rc:Show>
</rc:BreakpointProvider>
```

## Show Control Properties

**Breakpoint** - Specifies the breakpoint at which the content should be visible. It is of type `Breakpoint`.

| Breakpoint           | Pixel Equivalent         |
|----------------------|--------------------------|
| Breakpoint.Xs        | width < 600px            |
| Breakpoint.SmAndDown | width < 960px            |
| Breakpoint.Sm        | 600px <= width < 960px   |
| Breakpoint.SmAndUp   | width >= 600px           |
| Breakpoint.MdAndDown | width < 1280px           |
| Breakpoint.Md        | 960px <= width < 1280px  |
| Breakpoint.MdAndUp   | width >= 960px           |
| Breakpoint.LgAndDown | width < 1920px           |
| Breakpoint.Lg        | 1280px <= width < 1920px |
| Breakpoint.LgAndUp   | width >= 1280px          |
| Breakpoint.XlAndDown | width < 2560px           |
| Breakpoint.Xl        | 1920px <= width < 2560px |
| Breakpoint.XlAndUp   | width >= 1920px          |
| Breakpoint.Xxl       | width >= 2560px          |

**Condition** - A custom condition that can be used to determine the visibility of the content. It is a `Func<double,bool>` delegate
that returns true if the content should be visible. see the [Custom Conditions](#custom-conditions) section for more details.

**Invert** - A boolean property that inverts the visibility condition. If set to true, the content will be hidden at the
  specified breakpoint. Not that this property is also respected when using the `Condition` property.

## Custom Conditions
For more granular control, custom conditions can be used instead of the standard breakpoints. As an example, here is a condition to show the element if the width of the breakpoint provider is between 600 and 700 pixels:
```csharp
using System;

namespace SampleApp;

public static class CustomBreakpoints
{
    // Example implementation of a custom breakpoint for demonstration purposes.
    public static Func<double,bool> Width600To700Condition => width => width is >= 600 and < 700;
}
```

To use this, we can set the `Condition` property of the `Show` control:

```xaml
<rc:Show Condition="{x:Static sampleApp:CustomBreakpoints.Width600To700Condition}">
   <TextBlock Text="Visible if width is between 600px and 700px" />
</rc:Show>
```
> [!IMPORTANT]
> When using custom conditions, the `Breakpoint` property will be ignored.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for more details.
