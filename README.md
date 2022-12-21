# Getting Started with .NET MAUI Chart

## Creating an application using the .NET MAUI chart

1. Create a new .NET MAUI application in Visual Studio.
2. Syncfusion .NET MAUI components are available in [nuget.org](https://www.nuget.org/). To add SfFunnelChart to your project, open the NuGet package manager in Visual Studio, search for Syncfusion.Maui.Charts and then install it.
3. To initialize the control, import the Chart namespace.
4. Initialize [SfFunnelChart]().

**[XAML]**
```
<ContentPage   
    . . .
    xmlns:chart="clr-namespace:Syncfusion.Maui.Charts;assembly=Syncfusion.Maui.Charts">

    <chart:SfFunnelChart/>
</ContentPage>
```

**[C#]**
```
using Syncfusion.Maui.Charts;
. . .

public partial class MainWindow : ContentPage
{
    public MainPage()
    {
        this.InitializeComponent();
        SfFunnelChart chart = new SfFunnelChart();
    }
}   
```

## Register the handler

Syncfusion.Maui.Core Nuget is a dependent package for all Syncfusion controls of .NET MAUI. In the MauiProgram.cs file, register the handler for Syncfusion core.

**[C#]**
```
using Microsoft.Maui;
using Microsoft.Maui.Hosting;
using Microsoft.Maui.Controls.Compatibility;
using Microsoft.Maui.Controls.Hosting;
using Microsoft.Maui.Controls.Xaml;
using Syncfusion.Maui.Core.Hosting;

namespace ChartGettingStarted
{
    public static class MauiProgram
    {
        public static MauiApp CreateMauiApp()
        {
            var builder = MauiApp.CreateBuilder();
            builder
            .UseMauiApp<App>()
            .ConfigureSyncfusionCore()
            .ConfigureFonts(fonts =>
            {
                fonts.AddFont("OpenSans-Regular.ttf", "OpenSansRegular");
            });

            return builder.Build();
        }
    }
}
```

## Initialize view model

Now, let us define a simple data model that represents a data point in the chart.

**[C#]**
```
 public class Admission
{
    public string XValue { get; set; }
    public double YValue { get; set; }
}
```

Next, create a view model class and initialize a list of `Model` objects as follows.

**[C#]**
```
public class ChartViewModel
{
    public List<Admission> Data { get; set; }

    public ChartViewModel()
    {
        Data = new List<Admission>()
        {
            new Admission() {XValue = "Enrolled", YValue=175},
            new Admission() {XValue = "Admits", YValue=190},
            new Admission() {XValue = "Applicants", YValue=245},
            new Admission() {XValue = "Inquiries ", YValue=290},
            new Admission() {XValue = "Prospects ", YValue=320},
        };
    }
}
```

Create a `ViewModel` instance and set it as the chart's `BindingContext`. This enables property binding from `ViewModel` class.

> **_Note:_**
Add the namespace of `ViewModel` class to your XAML Page, if you prefer to set `BindingContext` in XAML.

**[XAML]**
```
<ContentPage
    . . .
    xmlns:chart="clr-namespace:Syncfusion.Maui.Charts;assembly=Syncfusion.Maui.Charts"
    xmlns:model="clr-namespace:ChartGettingStarted">

    <chart:SfFunnelChart>
        <chart:SfFunnelChart.BindingContext>
        <model:ChartViewModel/>
        </chart:SfFunnelChart.BindingContext>
    </chart:SfFunnelChart>
</ContentPage>
```

**[C#]**
```
ChartViewModel viewModel = new ChartViewModel();
chart.BindingContext = viewModel;
```

## Populate chart with data

 Binding `Data` to the funnel chart [ItemsSource]() property from its BindingContext to create our own funnel chart.

**[XAML]**
```
<chart:SfFunnelChart ItemsSource="{Binding Data}" 
                     XBindingPath="XValue" 
                     YBindingPath="YValue"/>
. . .            
</chart:SfFunnelChart>
```

**[C#]**
```
SfFunnelChart chart = new SfFunnelChart();
ChartViewModel viewModel = new ChartViewModel();
chart.BindingContext = viewModel;
chart.ItemsSource = viewModel.Data;
chart.XBindingPath = "XValue";
chart.YBindingPath = "YValue";
this.Content = chart;
```

## Add a title

The title of the chart acts as the title to provide quick information to the user about the data being plotted in the chart. You can set the title using the [Title](https://help.syncfusion.com/cr/maui/Syncfusion.Maui.Charts.ChartBase.html#Syncfusion_Maui_Charts_ChartBase_Title) property of the funnel chart as follows.

**[XAML]**
```
<chart:SfFunnelChart>
    <chart:SfFunnelChart.Title>
        <Label Text="School Admission"/>
    </chart:SfFunnelChart.Title>
    . . .
</chart:SfFunnelChart>
```

**[C#]**
```
SfFunnelChart chart = new SfFunnelChart();
chart.Title = new Label
{
    Text = "School Admission"
};
```

## Enable the data labels

The [ShowDataLabels]() property of the chart can be used to enable data labels to improve the readability of the funnel chart. The label visibility is set to `False` by default.

**[XAML]**
```
<chart:SfFunnelChart ShowDataLabels="True">
    . . .
</chart:SfFunnelChart>
```

**[C#]**
```
SfFunnelChart chart = new SfFunnelChart();
. . .
chart.ShowDataLabels = true;
```

## Enable a legend

The legend provides information about the data point displayed in the funnel chart. The [Legend](https://help.syncfusion.com/cr/maui/Syncfusion.Maui.Charts.ChartBase.html#Syncfusion_Maui_Charts_ChartBase_Legend) property of the chart was used to enable it.

**[XAML]**
```
<chart:SfFunnelChart>
    . . .
    <chart:SfFunnelChart.Legend>
    <chart:ChartLegend/>
    </chart:SfFunnelChart.Legend>
</chart:SfFunnelChart>
```

**[C#]**
```
SfFunnelChart chart = new SfFunnelChart();
. . .
chart.Legend = new ChartLegend();
```

## Enable Tooltip

Tooltips are used to show information about the segment, when mouse over on it. Enable tooltip by setting the chart [EnableTooltip]() property as true.

**[XAML]**
```
<chart:SfFunnelChart EnableTooltip="True">
    . . .
</chart:SfFunnelChart>
```

**[C#]**
```
SfFunnelChart chart = new SfFunnelChart();
. . .
chart.EnableTooltip = true;
```

The following code example gives you the complete code of above configurations.

**[XAML]**
```
<chart:SfFunnelChart ItemsSource="{Binding Data}" 
                     ShowDataLabels="True" 
                     XBindingPath="XValue" 
                     YBindingPath="YValue"
                     EnableTooltip="True">
    <chart:SfFunnelChart.Title>
        <Label Text="School Admission"/>
    </chart:SfFunnelChart.Title>
    <chart:SfFunnelChart.BindingContext>
        <model:ChartViewModel/>
    </chart:SfFunnelChart.BindingContext>
    <chart:SfFunnelChart.Legend>
        <chart:ChartLegend/>
    </chart:SfFunnelChart.Legend>
</chart:SfFunnelChart>
```

**[C#]**
```
using Syncfusion.Maui.Charts;
. . .
public partial class MainPage : ContentPage
{   
    public MainWindow()
    {
        SfFunnelChart chart = new SfFunnelChart();
        chart.Title = new Label
        {
            Text = "School Admission"
        };
        chart.Legend = new ChartLegend();
        ChartViewModel viewModel = new ChartViewModel();
        chart.BindingContext = viewModel;

        chart.ItemsSource = viewModel.Data;
        chart.XBindingPath = "XValue";
        chart.YBindingPath = "YValue";
        chart.EnableTooltip = true;
        chart.ShowDataLabels = true;
        this.Content = chart;
    }
}
```

![Funnel chart in .NET MAUI Chart](MAUI_funnel_chart.png)
