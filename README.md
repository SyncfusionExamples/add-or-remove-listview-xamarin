# How to add or remove an item from Xamarin.Forms ListView (SfListView)

You can add or remove items from [ItemsSource](https://help.syncfusion.com/cr/cref_files/xamarin/Syncfusion.SfListView.XForms~Syncfusion.ListView.XForms.SfListView~ItemsSource.html?) with a bound collection from ViewModel in Xamarin.Forms [SfListView](https://help.syncfusion.com/xamarin/listview/overview?).

**XAML**

ViewModel [commands](https://docs.microsoft.com/en-us/dotnet/api/system.windows.input.icommand?view=netframework-4.8) bound to view to add or remove item.
``` xml
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:local="clr-namespace:ListViewXamarin"
             xmlns:syncfusion="clr-namespace:Syncfusion.ListView.XForms;assembly=Syncfusion.SfListView.XForms"
             x:Class="ListViewXamarin.MainPage">
    <ContentPage.BindingContext>
        <local:ContactsViewModel/>
    </ContentPage.BindingContext>
 
    <ContentPage.Content>
        <StackLayout>
            <Grid HeightRequest="50" >
                <Button Text="Add item" Grid.Column="0" Command="{Binding AddCommand}"/>
                <Button Text="Delete last item" Grid.Column="1" Command="{Binding DeleteCommand}}"/>
            </Grid>
            <syncfusion:SfListView x:Name="listView" 
                                   ItemSpacing="1" 
                                   ItemSize="50"
                                   ItemsSource="{Binding contactsinfo}">
                <syncfusion:SfListView.ItemTemplate >
                    <DataTemplate>
                        <Grid x:Name="grid" RowSpacing="0">
                            <Grid RowSpacing="0">
                                <Grid.ColumnDefinitions>
                                    <ColumnDefinition Width="70" />
                                    <ColumnDefinition Width="*" />
                                </Grid.ColumnDefinitions>
                                <Image Source="{Binding ContactImage}" VerticalOptions="Center" HorizontalOptions="Center" HeightRequest="50" WidthRequest="50"/>
                                <Grid Grid.Column="1" RowSpacing="1" Padding="10,0,0,0" VerticalOptions="Center">
                                    <Label LineBreakMode="NoWrap" TextColor="#474747" Text="{Binding ContactName}"/>
                                    <Label Grid.Row="1" Grid.Column="0" TextColor="#474747" LineBreakMode="NoWrap" Text="{Binding ContactNumber}"/>
                                </Grid>
                            </Grid>
                        </Grid>
                    </DataTemplate>
                </syncfusion:SfListView.ItemTemplate>
            </syncfusion:SfListView>
        </StackLayout>
    </ContentPage.Content>
</ContentPage>
```
**C#**

Object added to the collection of ViewModel.
``` c#
public class ContactsViewModel
{
  public Command AddCommand { get; set; }
 
    public ContactsViewModel ()
    {
        AddCommand = new Command(OnAddTapped);
    }
 
    private void OnAddTapped(object obj)
  {
      var details = new Contacts()
      {
          ContactNumber = random.Next(100, 400).ToString() + "-" + random.Next(500, 800).ToString() + "-" + random.Next(1000, 2000).ToString(),
          ContactName = CustomerNames[random.Next(1, 50)],
          ContactImage = ImageSource.FromResource("ListViewXamarin.Images.Image" + random.Next(0, 28) + ".png", typeof(MainPage)),
      };
      contactsinfo.Add(details);
  }
}
```
**C#**

Object removed from the collection of ViewModel.
``` c#
public class ContactsViewModel
{
  public Command DeleteCommand { get; set; }
 
    public ContactsViewModel ()
    {
        DeleteCommand = new Command(OnDeleteTapped);
    }
    private void OnDeleteTapped(object obj)
  {
      if (contactsinfo.Count > 0)
          contactsinfo.Remove(contactsinfo[contactsinfo.Count - 1]);
      else
          App.Current.MainPage.DisplayAlert("Alert", "There is no item in the list", "OK");
  }
}
```
