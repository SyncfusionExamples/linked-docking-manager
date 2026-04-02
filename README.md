# Linked DockingManager
This sample demonstrates linking two DockingManager instances so that child windows can be dragged and dropped from one manager to another. By default, panes cannot cross DockingManager boundaries. With Linked Manager support, you can add target managers so panes move seamlessly between managers without losing layout, headers, or state.

[Documentation](https://help.syncfusion.com/wpf/dockingmanager/linked-manager)

## Concept
- Allow cross-manager drag-and-drop by adding a DockingManager to another manager’s target list.
- Use AddToTargetManagersList to link, and RemoveFromTargetManagersList to unlink.
- For bi-directional movement, both managers must add each other as targets.
- If only one side is linked, panes moved to the target cannot be dragged back.

## Source DockingManager (XAML)
```xml
<syncfusion:DockingManager x:Name="DockingManager1">
  <ContentControl syncfusion:DockingManager.State="Document"
                  syncfusion:DockingManager.Header="Window1" />
  <ContentControl syncfusion:DockingManager.State="Dock"
                  syncfusion:DockingManager.Header="Window2" />
  <ContentControl syncfusion:DockingManager.State="AutoHidden"
                  syncfusion:DockingManager.Header="Window3" />
</syncfusion:DockingManager>
```

## Target DockingManager (XAML)
```xml
<syncfusion:DockingManager x:Name="DockingManager2">
  <ContentControl syncfusion:DockingManager.State="Dock"
                  syncfusion:DockingManager.Header="Window1" />
  <ContentControl syncfusion:DockingManager.State="Dock"
                  syncfusion:DockingManager.Header="Window2" />
  <ContentControl syncfusion:DockingManager.State="AutoHidden"
                  syncfusion:DockingManager.Header="Window3" />
</syncfusion:DockingManager>

```

## Linking managers (C#)
```csharp
public partial class MainWindow : Window
{
    public MainWindow()
    {
        InitializeComponent();

        var other = new MainWindow1 { Title = "Docking Manager 1" };
        other.Show();

        // Enable cross-docking in both directions
        this.DockingManager1.AddToTargetManagersList(other.DockingManager2);
        other.DockingManager2.AddToTargetManagersList(this.DockingManager1);
    }
}
```

## One-way link
```csharp
this.DockingManager1.AddToTargetManagersList(MainWindow.DockingManager2);
```

## Two-way link
```csharp
this.DockingManager1.AddToTargetManagersList(MainWindow.DockingManager2);
MainWindow.DockingManager2.AddToTargetManagersList(this.DockingManager1);
```

## Removing a link
```csharp
MainWindow.DockingManager2.RemoveFromTargetManagersList(this.DockingManager1);
```

## Notes
- Ensure each DockingManager is created and visible before linking.
- Two-way linking provides a symmetric user experience; one-way restricts return drag.
- Keep headers distinct to recognize panes after cross-docking.
- If docking fails, verify target list entries exist and both windows are active at runtime.

