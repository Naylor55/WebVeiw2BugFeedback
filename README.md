# WebVeiw2BugFeedback
WPF中使用WebView2遇到一个问题，猜测是控件的bug，此工程为bug复现和演示的代码


# bug 描述
**Description**
创建一个WPF的应用程序，引入webview2控件来显示网页，当代码放到E盘（E:\code\WPF\WebView2Bug）的时候应用程序启动后webview2控件成功显示了网页信息，但是当将代码文件放到C盘（C:\Program Files (x86)\WebView2Bug）中的时候，此时应用启动之后webview2控件显示空白，调试的时候，webview2.corewebview2对象为null

**Version**
我开发环境用的windows11，VS的版本为Microsoft Visual Studio Community 2022 (64 位) - Current
版本 17.4.1，webview2的版本为1.0.1418.22

**Repro Steps**
核心代码如下 ：
xaml:
`
<Window x:Class="WebView2Bug.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
         xmlns:wv2="clr-namespace:Microsoft.Web.WebView2.Wpf;assembly=Microsoft.Web.WebView2.Wpf"
        xmlns:local="clr-namespace:WebView2Bug"
        mc:Ignorable="d"
        Title="MainWindow" Height="950" Width="1300" ContentRendered="Window_ContentRendered">
    <Grid>
        <Grid.RowDefinitions>
            <RowDefinition Height="60"></RowDefinition>
            <RowDefinition Height="10*"></RowDefinition>
        </Grid.RowDefinitions>
        <Button Grid.Row="0" Name="btn" Width="100" Height="50" Content="查看CoreWebview2" Click="btn_Click"></Button>
        <wv2:WebView2 Grid.Row="1" Name="browser"   Source="http://baidu.com"/>

    </Grid>
</Window>

`
cs:
`
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Data;
using System.Windows.Documents;
using System.Windows.Input;
using System.Windows.Media;
using System.Windows.Media.Imaging;
using System.Windows.Navigation;
using System.Windows.Shapes;

namespace WebView2Bug
{
    /// <summary>
    /// MainWindow.xaml 的交互逻辑
    /// </summary>
    public partial class MainWindow : Window
    {
        public MainWindow()
        {
            InitializeComponent();
        }

        private void Window_ContentRendered(object sender, EventArgs e)
        {
            
        }

        private void btn_Click(object sender, RoutedEventArgs e)
        {
            bool result = this.browser.CoreWebView2 == null ? true : false;
            MessageBox.Show("WebView2控件的CoreWebView2是否为null？" + result);
        }
    }
}

`

<!-- Extra / Helpful -->
**Screenshots**
当代码在E盘（E:\code\WPF\WebView2Bug）中的时候，程序运行起来可以正常显示网页信息：

![图片](https://user-images.githubusercontent.com/13940383/209620616-2c7634df-6fd7-4151-943d-726b6f4d5907.png)

当点击 查看CoreWebView 按钮的时候，获取到其值不为null：
![图片](https://user-images.githubusercontent.com/13940383/209620771-15f09554-5a80-4942-93c7-4283fa7b46e2.png)

当代码在C盘（）中 的时候，程序运行起来不可以显示网页信息：
![图片](https://user-images.githubusercontent.com/13940383/209620928-124d14c9-c386-40b1-9c96-ed5189558137.png)

当点击  查看CoreWebView 按钮的时候，获取到其值为null：
![图片](https://user-images.githubusercontent.com/13940383/209620960-28985018-d86b-4ae5-b592-e801eabf9fe6.png)




**Additional context**



#  官方 issues 地址

