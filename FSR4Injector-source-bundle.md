# FSR 4 Injector — generated WinUI 3 project source

Every file of the generated project, in order. Paste each block into a file with the path shown above it.
## FSR4Injector.sln

```text
Microsoft Visual Studio Solution File, Format Version 12.00
# Visual Studio Version 17
VisualStudioVersion = 17.8.34309.116
MinimumVisualStudioVersion = 10.0.40219.1
Project("{9A19103F-16F7-4668-BE54-9A1E7A4F7556}") = "FSR4Injector", "FSR4Injector\FSR4Injector.csproj", "{8B4E1F2C-3A7D-4C61-9E2B-5D6A7C8E9F01}"
EndProject
Global
	GlobalSection(SolutionConfigurationPlatforms) = preSolution
		Debug|x64 = Debug|x64
		Release|x64 = Release|x64
	EndGlobalSection
	GlobalSection(ProjectConfigurationPlatforms) = postSolution
		{8B4E1F2C-3A7D-4C61-9E2B-5D6A7C8E9F01}.Debug|x64.ActiveCfg = Debug|x64
		{8B4E1F2C-3A7D-4C61-9E2B-5D6A7C8E9F01}.Debug|x64.Build.0 = Debug|x64
		{8B4E1F2C-3A7D-4C61-9E2B-5D6A7C8E9F01}.Release|x64.ActiveCfg = Release|x64
		{8B4E1F2C-3A7D-4C61-9E2B-5D6A7C8E9F01}.Release|x64.Build.0 = Release|x64
	EndGlobalSection
	GlobalSection(SolutionProperties) = preSolution
		HideSolutionNode = FALSE
	EndGlobalSection
EndGlobal
```

## FSR4Injector/FSR4Injector.csproj

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <OutputType>WinExe</OutputType>
    <TargetFramework>net8.0-windows10.0.19041.0</TargetFramework>
    <TargetPlatformMinVersion>10.0.17763.0</TargetPlatformMinVersion>
    <RootNamespace>FSR4Injector</RootNamespace>
    <AssemblyName>FSR4Injector</AssemblyName>
    <ApplicationManifest>app.manifest</ApplicationManifest>
    <Platforms>x64;ARM64</Platforms>
    <RuntimeIdentifiers>win-x64;win-arm64</RuntimeIdentifiers>
    <UseWinUI>true</UseWinUI>
    <Nullable>enable</Nullable>
    <ImplicitUsings>disable</ImplicitUsings>

    <!-- Unpackaged: the app runs as a plain .exe, no MSIX install step. -->
    <WindowsPackageType>None</WindowsPackageType>
  </PropertyGroup>

  <ItemGroup>
    <PackageReference Include="Microsoft.WindowsAppSDK" Version="1.5.240802000" />
    <PackageReference Include="Microsoft.Windows.SDK.BuildTools" Version="10.0.22621.3233" />
    <!-- Only needed if your SDK does not already expose the Microsoft.Win32.Registry APIs. -->
    <PackageReference Include="Microsoft.Win32.Registry" Version="5.0.0" />
  </ItemGroup>

  <!-- Ship the wrapper DLLs and config next to the executable. -->
  <ItemGroup>
    <None Update="Assets\FSR4_Files\**\*" CopyToOutputDirectory="PreserveNewest" />
  </ItemGroup>

</Project>
```

## FSR4Injector/app.manifest

```xml
<?xml version="1.0" encoding="utf-8"?>
<assembly manifestVersion="1.0" xmlns="urn:schemas-microsoft-com:asm.v1">
  <assemblyIdentity version="1.0.0.0" name="FSR4Injector.app" />

  <compatibility xmlns="urn:schemas-microsoft-com:compatibility.v1">
    <application>
      <!-- Windows 10 and Windows 11 -->
      <supportedOS Id="{8e0f7a12-bfb3-4fe8-b9a5-48fd50a15a9a}" />
    </application>
  </compatibility>

  <application xmlns="urn:schemas-microsoft-com:asm.v3">
    <windowsSettings>
      <dpiAwareness xmlns="http://schemas.microsoft.com/SMI/2016/WindowsSettings">PerMonitorV2</dpiAwareness>
    </windowsSettings>
  </application>
</assembly>
```

## FSR4Injector/App.xaml

```xml
<?xml version="1.0" encoding="utf-8"?>
<Application
    x:Class="FSR4Injector.App"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml">
    <Application.Resources>
        <ResourceDictionary>
            <ResourceDictionary.MergedDictionaries>
                <XamlControlsResources xmlns="using:Microsoft.UI.Xaml.Controls" />
            </ResourceDictionary.MergedDictionaries>
        </ResourceDictionary>
    </Application.Resources>
</Application>
```

## FSR4Injector/App.xaml.cs

```csharp
using Microsoft.UI.Xaml;

namespace FSR4Injector;

public partial class App : Application
{
    private Window? _window;

    public App()
    {
        InitializeComponent();
    }

    protected override void OnLaunched(LaunchActivatedEventArgs args)
    {
        _window = new MainWindow();
        _window.Activate();
    }
}
```

## FSR4Injector/MainWindow.xaml

```xml
<?xml version="1.0" encoding="utf-8"?>
<Window
    x:Class="FSR4Injector.MainWindow"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:models="using:FSR4Injector.Models"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    mc:Ignorable="d"
    Title="FSR 4 Injector">

    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <Grid.RowDefinitions>
            <RowDefinition Height="Auto" />
            <RowDefinition Height="*" />
            <RowDefinition Height="Auto" />
        </Grid.RowDefinitions>

        <!-- Header -->
        <StackPanel Grid.Row="0" Padding="28,24,28,12" Spacing="4">
            <TextBlock Text="FSR 4 + frame generation injector"
                       Style="{StaticResource TitleTextBlockStyle}" />
            <TextBlock Text="Single-player games only. Multiplayer and kernel-level anti-cheat titles are blocked automatically."
                       Style="{StaticResource CaptionTextBlockStyle}"
                       Foreground="{ThemeResource TextFillColorSecondaryBrush}"
                       TextWrapping="Wrap" />
        </StackPanel>

        <ScrollViewer Grid.Row="1" Padding="28,0,28,16" VerticalScrollBarVisibility="Auto">
            <StackPanel Spacing="16" MaxWidth="840" HorizontalAlignment="Stretch">

                <!-- Safety guard banner: becomes the error report when a title is blocked -->
                <InfoBar x:Name="SafetyInfoBar"
                         IsOpen="True"
                         IsClosable="False"
                         Severity="Informational"
                         Title="Safety guard active"
                         Message="Injection is restricted to single-player, offline games. Known multiplayer executables and game folders that contain an anti-cheat component are refused." />

                <!-- 1: choose the game -->
                <Border Background="{ThemeResource CardBackgroundFillColorDefaultBrush}"
                        BorderBrush="{ThemeResource CardStrokeColorDefaultBrush}"
                        BorderThickness="1"
                        CornerRadius="8"
                        Padding="20">
                    <StackPanel Spacing="12">
                        <TextBlock Text="1 — Choose a single-player game" Style="{StaticResource BodyStrongTextBlockStyle}" />
                        <StackPanel Orientation="Horizontal" Spacing="10">
                            <Button x:Name="SelectGameButton" Content="Select game executable…" Click="OnSelectGameClicked" />
                            <Button x:Name="ScanButton" Content="Scan Steam, Epic Games, GOG" Click="OnScanClicked" />
                            <ProgressRing x:Name="ScanProgress" IsActive="False" Width="20" Height="20" VerticalAlignment="Center" />
                        </StackPanel>
                        <TextBlock x:Name="SelectedGameText" Text="No game selected" Style="{StaticResource BodyTextBlockStyle}" />
                        <TextBlock x:Name="InstallPathText"
                                   Style="{StaticResource CaptionTextBlockStyle}"
                                   Foreground="{ThemeResource TextFillColorSecondaryBrush}"
                                   TextWrapping="Wrap"
                                   IsTextSelectionEnabled="True" />
                    </StackPanel>
                </Border>

                <!-- 2: the one-button toggle -->
                <Border Background="{ThemeResource CardBackgroundFillColorDefaultBrush}"
                        BorderBrush="{ThemeResource CardStrokeColorDefaultBrush}"
                        BorderThickness="1"
                        CornerRadius="8"
                        Padding="20">
                    <StackPanel Spacing="12">
                        <TextBlock Text="2 — Injector toggle" Style="{StaticResource BodyStrongTextBlockStyle}" />
                        <ToggleSwitch x:Name="InjectToggle"
                                      Header="FSR 4 upscaling + frame generation"
                                      OnContent="ON"
                                      OffContent="OFF"
                                      IsEnabled="False"
                                      Toggled="OnToggleToggled" />
                        <TextBlock x:Name="StatusText"
                                   Text="Status: waiting for a game"
                                   Style="{StaticResource CaptionTextBlockStyle}"
                                   Foreground="{ThemeResource TextFillColorSecondaryBrush}" />
                        <Button x:Name="OpenFolderButton" Content="Open game folder" Click="OnOpenFolderClicked" IsEnabled="False" />
                    </StackPanel>
                </Border>

                <!-- 3: scanned single-player titles -->
                <Border Background="{ThemeResource CardBackgroundFillColorDefaultBrush}"
                        BorderBrush="{ThemeResource CardStrokeColorDefaultBrush}"
                        BorderThickness="1"
                        CornerRadius="8"
                        Padding="20">
                    <StackPanel Spacing="12">
                        <TextBlock Text="3 — Detected single-player games" Style="{StaticResource BodyStrongTextBlockStyle}" />
                        <TextBlock Text="Read from the installed Steam, Epic Games, GOG libraries. Titles on the anti-cheat block list are filtered out before this list is built."
                                   Style="{StaticResource CaptionTextBlockStyle}"
                                   Foreground="{ThemeResource TextFillColorSecondaryBrush}"
                                   TextWrapping="Wrap" />
                        <ListView x:Name="GamesList"
                                  MaxHeight="280"
                                  SelectionMode="None"
                                  IsItemClickEnabled="True"
                                  ItemClick="OnGameItemClick"
                                  BorderThickness="0">
                            <ListView.ItemTemplate>
                                <DataTemplate x:DataType="models:GameInfo">
                                    <Grid ColumnSpacing="12" Padding="0,8">
                                        <Grid.ColumnDefinitions>
                                            <ColumnDefinition Width="*" />
                                            <ColumnDefinition Width="Auto" />
                                        </Grid.ColumnDefinitions>
                                        <StackPanel Grid.Column="0" Spacing="2">
                                            <TextBlock Text="{x:Bind Name}" Style="{StaticResource BodyTextBlockStyle}" TextTrimming="CharacterEllipsis" />
                                            <TextBlock Text="{x:Bind InstallDirectory}" Style="{StaticResource CaptionTextBlockStyle}" Foreground="{ThemeResource TextFillColorSecondaryBrush}" TextTrimming="CharacterEllipsis" />
                                        </StackPanel>
                                        <TextBlock Grid.Column="1" Text="{x:Bind Launcher}" Style="{StaticResource CaptionTextBlockStyle}" Foreground="{ThemeResource TextFillColorSecondaryBrush}" VerticalAlignment="Center" />
                                    </Grid>
                                </DataTemplate>
                            </ListView.ItemTemplate>
                        </ListView>
                    </StackPanel>
                </Border>
            </StackPanel>
        </ScrollViewer>

        <!-- Footer -->
        <Border Grid.Row="2" Padding="28,12,28,20">
            <TextBlock Style="{StaticResource CaptionTextBlockStyle}"
                       Foreground="{ThemeResource TextFillColorSecondaryBrush}"
                       TextWrapping="Wrap"
                       Text="Wrapper files are read from Assets\FSR4_Files next to the executable. Switching the toggle off restores every original file that was replaced." />
        </Border>
    </Grid>
</Window>
```

## FSR4Injector/MainWindow.xaml.cs

```csharp
using System;
using System.Collections.ObjectModel;
using System.Diagnostics;
using System.IO;
using System.Threading.Tasks;
using FSR4Injector.Models;
using FSR4Injector.Safety;
using FSR4Injector.Services;
using Microsoft.UI.Xaml;
using Microsoft.UI.Xaml.Controls;
using Windows.Storage.Pickers;
using WinRT.Interop;

namespace FSR4Injector;

public sealed partial class MainWindow : Window
{
    private readonly ObservableCollection<GameInfo> _detectedGames = new ObservableCollection<GameInfo>();

    private string _selectedGameDirectory = string.Empty;
    private string _selectedGameExe = string.Empty;
    private bool _suppressToggleEvent;

    // Wrapper assets that ship next to the executable.
    private static readonly string WrapperAssetFolder =
        Path.Combine(AppContext.BaseDirectory, "Assets", "FSR4_Files");

    public MainWindow()
    {
        InitializeComponent();
        GamesList.ItemsSource = _detectedGames;
    }

    // 1 — the user picks an executable by hand.
    private async void OnSelectGameClicked(object sender, RoutedEventArgs e)
    {
        var picker = new FileOpenPicker();
        picker.FileTypeFilter.Add(".exe");
        picker.SuggestedStartLocation = PickerLocationId.ComputerFolder;

        // Unpackaged apps must hand the picker the window handle.
        InitializeWithWindow.Initialize(picker, WindowNative.GetWindowHandle(this));

        var file = await picker.PickSingleFileAsync();
        if (file is null)
        {
            return;
        }

        ApplySelection(file.Path, file.Name);
    }

    // 3 — scan the installed libraries, keeping single-player candidates only.
    private async void OnScanClicked(object sender, RoutedEventArgs e)
    {
        ScanProgress.IsActive = true;
        ScanButton.IsEnabled = false;
        SelectGameButton.IsEnabled = false;

        try
        {
            var detected = await Task.Run(GameScanner.ScanAll);

            _detectedGames.Clear();
            foreach (var game in detected)
            {
                _detectedGames.Add(game);
            }

            StatusText.Text = _detectedGames.Count == 0
                ? "Status: no single-player titles detected — use Select game executable…"
                : $"Status: {_detectedGames.Count} single-player title(s) detected";
        }
        catch (Exception ex)
        {
            ShowMessage(InfoBarSeverity.Error, "Scan failed", ex.Message);
        }
        finally
        {
            ScanProgress.IsActive = false;
            ScanButton.IsEnabled = true;
            SelectGameButton.IsEnabled = true;
        }
    }

    private void OnGameItemClick(object sender, ItemClickEventArgs e)
    {
        if (e.ClickedItem is GameInfo game)
        {
            ApplySelection(game.ExecutablePath, Path.GetFileName(game.ExecutablePath));
        }
    }

    // 2 — the master one-button toggle.
    private void OnToggleToggled(object sender, RoutedEventArgs e)
    {
        if (_suppressToggleEvent)
        {
            return;
        }

        if (string.IsNullOrEmpty(_selectedGameDirectory))
        {
            SetToggleSilently(false);
            ShowMessage(InfoBarSeverity.Warning, "No game selected", "Choose a single-player executable first.");
            return;
        }

        try
        {
            if (InjectToggle.IsChecked == true)
            {
                InjectorService.Enable(_selectedGameDirectory, WrapperAssetFolder);
                StatusText.Text = "Status: FSR 4 active (injected)";
                ShowMessage(InfoBarSeverity.Success, "Injected", "Proxy files are now active for " + _selectedGameExe + ".");
            }
            else
            {
                InjectorService.Disable(_selectedGameDirectory);
                StatusText.Text = "Status: disabled — " + _selectedGameExe + " restored to a clean state";
                ShowMessage(InfoBarSeverity.Informational, "Removed", "The game folder is back to its original state.");
            }
        }
        catch (Exception ex)
        {
            SetToggleSilently(false);
            ShowMessage(InfoBarSeverity.Error, "File operation failed", ex.Message);
        }
    }

    private void OnOpenFolderClicked(object sender, RoutedEventArgs e)
    {
        if (string.IsNullOrEmpty(_selectedGameDirectory))
        {
            return;
        }

        Process.Start(new ProcessStartInfo
        {
            FileName = _selectedGameDirectory,
            UseShellExecute = true
        });
    }

    /// <summary>
    /// The safety guard runs here, before a single byte is written.
    /// </summary>
    private void ApplySelection(string executablePath, string executableName)
    {
        var verdict = AntiCheatBlacklist.Inspect(executablePath);
        if (verdict.Blocked)
        {
            ClearSelection();
            ShowMessage(
                InfoBarSeverity.Error,
                "Blocked — multiplayer or anti-cheat detected",
                verdict.Reason + " Injection is limited to single-player, offline games so no account can ever be put at risk.");
            return;
        }

        _selectedGameDirectory = Path.GetDirectoryName(executablePath) ?? string.Empty;
        _selectedGameExe = executableName;

        var alreadyActive = InjectorService.IsActive(_selectedGameDirectory);

        SelectedGameText.Text = executableName;
        InstallPathText.Text = _selectedGameDirectory;
        InjectToggle.IsEnabled = true;
        OpenFolderButton.IsEnabled = true;
        SetToggleSilently(alreadyActive);
        StatusText.Text = alreadyActive
            ? "Status: FSR 4 already active for " + executableName
            : "Status: ready — " + executableName;
        ShowMessage(InfoBarSeverity.Informational, "Safety guard passed", executableName + " is not on the anti-cheat block list.");
    }

    private void ClearSelection()
    {
        _selectedGameDirectory = string.Empty;
        _selectedGameExe = string.Empty;
        SelectedGameText.Text = "No game selected";
        InstallPathText.Text = string.Empty;
        InjectToggle.IsEnabled = false;
        OpenFolderButton.IsEnabled = false;
        SetToggleSilently(false);
        StatusText.Text = "Status: blocked";
    }

    private void SetToggleSilently(bool isActive)
    {
        _suppressToggleEvent = true;
        InjectToggle.IsChecked = isActive;
        _suppressToggleEvent = false;
    }

    private void ShowMessage(InfoBarSeverity severity, string title, string message)
    {
        SafetyInfoBar.Severity = severity;
        SafetyInfoBar.Title = title;
        SafetyInfoBar.Message = message;
        SafetyInfoBar.IsOpen = true;
    }
}
```

## FSR4Injector/Models/GameInfo.cs

```csharp
using System.IO;

namespace FSR4Injector.Models;

/// <summary>
/// A single-player candidate found on disk.
/// </summary>
public sealed class GameInfo
{
    public string Name { get; set; } = string.Empty;

    public string ExecutablePath { get; set; } = string.Empty;

    public string Launcher { get; set; } = string.Empty;

    public string InstallDirectory => Path.GetDirectoryName(ExecutablePath) ?? string.Empty;
}
```

## FSR4Injector/Safety/AntiCheatBlacklist.cs

```csharp
using System;
using System.Collections.Generic;
using System.IO;

namespace FSR4Injector.Safety;

/// <summary>
/// Result of the check that runs before any file is touched.
/// </summary>
public sealed class GuardVerdict
{
    public GuardVerdict(bool blocked, string reason)
    {
        Blocked = blocked;
        Reason = reason;
    }

    public bool Blocked { get; }

    public string Reason { get; }

    public static GuardVerdict Allow() => new GuardVerdict(false, string.Empty);
}

/// <summary>
/// Hard block list of multiplayer titles and anti-cheat components.
/// Every path through this class can only ever refuse an injection — never allow one.
/// </summary>
public static class AntiCheatBlacklist
{
    /// <summary>Layer 1: exact executable names that are never injected.</summary>
    private static readonly HashSet<string> BlockedExecutables = new HashSet<string>(StringComparer.OrdinalIgnoreCase)
    {
        "valorant.exe",
        "valorant-win64-shipping.exe",
        "leagueclient.exe",
        "league of legends.exe",
        "riotclientservices.exe",
        "vgc.exe",
        "vgtray.exe",
        "cs2.exe",
        "csgo.exe",
        "dota2.exe",
        "cod.exe",
        "codhq.exe",
        "modernwarfare.exe",
        "modernwarfare2.exe",
        "modernwarfare3.exe",
        "mw2.exe",
        "mw3.exe",
        "warzone.exe",
        "blackops6.exe",
        "apexlegends.exe",
        "r5apex.exe",
        "r5apex_dx12.exe",
        "fortniteclient-win64-shipping.exe",
        "fortniteclient-win64-shipping-eac.exe",
        "pubg.exe",
        "tslgame.exe",
        "eft.exe",
        "escapefromtarkov.exe",
        "hunt.exe",
        "overwatch.exe",
        "destiny2.exe",
        "haloinfinite.exe",
        "titanfall2.exe",
        "battlefield2042.exe",
        "bf2042.exe",
        "bf1.exe",
        "bf4.exe",
        "deadbydaylight-win64-shipping.exe",
        "insurgencyclient-win64-shipping.exe",
        "paladins.exe",
        "squad.exe",
        "dayz_x64.exe",
        "arma3_x64.exe",
        "crossout.exe",
        "warthunder.exe",
        "fallguys_client_game.exe",
        "thefinals.exe",
        "newworld.exe",
        "lostark.exe",
        "warframe.x64.exe",
        "genshinimpact.exe",
        "starrail.exe",
        "zenlesszonezero.exe",
        "robloxplayerbeta.exe",
        "gta5.exe",
        "gta5_enhanced.exe",
        "rdr2.exe",
        "fivem.exe",
        "multitheftauto.exe",
        "faceitclient.exe",
        "faceitac.exe",
        "easyanticheat.exe",
        "easyanticheat_x64.exe",
        "easyanticheat_eos.exe",
        "easyanticheat_setup.exe",
        "battleye.exe",
        "beservice.exe",
        "beservice_x64.exe",
    };

    /// <summary>Layer 2: name fragments that always mean "online game with anti-cheat".</summary>
    private static readonly string[] BlockedNameTokens =
    {
        "anticheat",
        "anti-cheat",
        "easyanticheat",
        "battleye",
        "punkbuster",
        "xigncode",
        "nprotect",
        "gameguard",
        "faceitac",
        "byfron",
        "hyperion",
        "sguard",
    };

    /// <summary>Layer 3: files and folders that prove an anti-cheat is installed next to the game.</summary>
    private static readonly string[] AntiCheatMarkers =
    {
        "EasyAntiCheat",
        "EasyAntiCheat_EOS",
        "EasyAntiCheat_x64.dll",
        "EasyAntiCheat_x86.dll",
        "BattlEye",
        "BEService_x64.exe",
        "BEClient_x64.dll",
        "vgk.sys",
        "Vanguard",
        "faceitac.sys",
        "PunkBuster",
        "pbsvc.exe",
        "pbcl.dll",
        "ACE-BASE.sys",
        "ACE-GAME.dll",
        "GameGuard",
        "nProtect",
        "Xigncode",
        "xhunter1.sys",
        "Byfron",
        "Hyperion",
        "sguard64.exe",
        "EQU8.dll",
        "DenuvoAntiCheat",
    };

    public static GuardVerdict Inspect(string executablePath)
    {
        if (string.IsNullOrWhiteSpace(executablePath))
        {
            return new GuardVerdict(true, "No executable was supplied.");
        }

        var fileName = Path.GetFileName(executablePath);

        if (BlockedExecutables.Contains(fileName))
        {
            return new GuardVerdict(true, fileName + " is on the multiplayer / anti-cheat block list.");
        }

        foreach (var token in BlockedNameTokens)
        {
            if (fileName.Contains(token, StringComparison.OrdinalIgnoreCase))
            {
                return new GuardVerdict(true, fileName + " matches the anti-cheat name pattern " + token + ".");
            }
        }

        var directory = Path.GetDirectoryName(executablePath);
        if (!string.IsNullOrWhiteSpace(directory) && Directory.Exists(directory))
        {
            foreach (var marker in AntiCheatMarkers)
            {
                if (Directory.Exists(Path.Combine(directory, marker)) || File.Exists(Path.Combine(directory, marker)))
                {
                    return new GuardVerdict(true, "An anti-cheat component (" + marker + ") is installed in that game folder.");
                }
            }
        }

        return GuardVerdict.Allow();
    }
}
```

## FSR4Injector/Services/InjectorService.cs

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using System.Text.Json;

namespace FSR4Injector.Services;

/// <summary>What the toggle wrote into a game folder, so it can be undone exactly.</summary>
public sealed class InjectionState
{
    public List<InjectedFile> Files { get; set; } = new List<InjectedFile>();
}

public sealed class InjectedFile
{
    public string Name { get; set; } = string.Empty;

    /// <summary>True when an original file was renamed instead of being created fresh.</summary>
    public bool HadBackup { get; set; }
}

/// <summary>
/// The file half of the one-button toggle: copy the wrapper in, or put the folder back exactly as it was.
/// </summary>
public static class InjectorService
{
    private const string StateFileName = "fp_injector_state.json";
    private const string BackupSuffix = ".fsr4backup";

    /// <summary>Files copied into the game folder when the toggle is switched on.</summary>
    public static readonly string[] WrapperFiles =
    {
        "dxgi.dll",
        "nvngx.dll",
        "OptiScaler.ini",
    };

    public static bool IsActive(string gameDirectory)
    {
        return !string.IsNullOrEmpty(gameDirectory)
            && File.Exists(Path.Combine(gameDirectory, StateFileName));
    }

    public static void Enable(string gameDirectory, string assetDirectory)
    {
        var missing = WrapperFiles
            .Where(fileName => !File.Exists(Path.Combine(assetDirectory, fileName)))
            .ToList();

        if (missing.Count > 0)
        {
            throw new InvalidOperationException(
                "Wrapper assets are missing from " + assetDirectory + Environment.NewLine +
                "Expected: " + string.Join(", ", missing) + Environment.NewLine +
                "Copy your OptiScaler build into the app's Assets folder first.");
        }

        var state = new InjectionState();

        foreach (var fileName in WrapperFiles)
        {
            var target = Path.Combine(gameDirectory, fileName);
            var backup = target + BackupSuffix;
            var hadBackup = false;

            if (File.Exists(target) && !File.Exists(backup))
            {
                File.Move(target, backup);
                hadBackup = true;
            }

            File.Copy(Path.Combine(assetDirectory, fileName), target, true);
            state.Files.Add(new InjectedFile { Name = fileName, HadBackup = hadBackup });
        }

        var options = new JsonSerializerOptions { WriteIndented = true };
        File.WriteAllText(Path.Combine(gameDirectory, StateFileName), JsonSerializer.Serialize(state, options));
    }

    public static void Disable(string gameDirectory)
    {
        var statePath = Path.Combine(gameDirectory, StateFileName);

        InjectionState? state = null;
        if (File.Exists(statePath))
        {
            try
            {
                state = JsonSerializer.Deserialize<InjectionState>(File.ReadAllText(statePath));
            }
            catch (JsonException)
            {
                state = null;
            }
        }

        var files = state?.Files ?? WrapperFiles.Select(name => new InjectedFile { Name = name }).ToList();

        foreach (var entry in files)
        {
            var target = Path.Combine(gameDirectory, entry.Name);
            var backup = target + BackupSuffix;

            if (entry.HadBackup && File.Exists(backup))
            {
                if (File.Exists(target))
                {
                    File.Delete(target);
                }

                File.Move(backup, target);
            }
            else if (File.Exists(target))
            {
                File.Delete(target);
            }
        }

        if (File.Exists(statePath))
        {
            File.Delete(statePath);
        }
    }
}
```

## FSR4Injector/Services/GameScanner.cs

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using System.Text.Json;
using System.Text.RegularExpressions;
using FSR4Injector.Models;
using FSR4Injector.Safety;
using Microsoft.Win32;

namespace FSR4Injector.Services;

/// <summary>
/// Walks the installed game libraries and returns single-player candidates only.
/// Anything the safety guard flags is dropped before the list reaches the UI.
/// </summary>
public static class GameScanner
{
    /// <summary>Executables that are never the game itself.</summary>
    private static readonly string[] IgnoredExeTokens =
    {
        "unins", "vcredist", "dxsetup", "directx", "dotnet", "setup", "install",
        "updater", "launcher", "redist", "prereq", "crashreport", "crashhandler", "report"
    };

    public static List<GameInfo> ScanAll()
    {
        var found = new List<GameInfo>();

        ScanSteam(found);
        ScanEpic(found);
        ScanGog(found);

        return found
            .Where(game => !AntiCheatBlacklist.Inspect(game.ExecutablePath).Blocked)
            .GroupBy(game => game.ExecutablePath, StringComparer.OrdinalIgnoreCase)
            .Select(group => group.First())
            .OrderBy(game => game.Name, StringComparer.OrdinalIgnoreCase)
            .ToList();
    }

    /// <summary>Steam libraries, read from the launcher's own library index.</summary>
    private static void ScanSteam(List<GameInfo> found)
    {
        try
        {
            var steamRoot = ReadRegistryString(RegistryHive.CurrentUser, @"Software\Valve\Steam", "SteamPath")
                ?? ReadRegistryString(RegistryHive.LocalMachine, @"SOFTWARE\WOW6432Node\Valve\Steam", "InstallPath");

            if (string.IsNullOrEmpty(steamRoot) || !Directory.Exists(steamRoot))
            {
                return;
            }

            foreach (var library in SteamLibraries(steamRoot))
            {
                var common = Path.Combine(library, "steamapps", "common");
                if (!Directory.Exists(common))
                {
                    continue;
                }

                foreach (var folder in Directory.GetDirectories(common))
                {
                    AddGameFromFolder(found, folder, "Steam");
                }
            }
        }
        catch (Exception)
        {
            // A locked or missing registry key must never stop the whole scan.
        }
    }

    private static IEnumerable<string> SteamLibraries(string steamRoot)
    {
        var libraries = new List<string> { steamRoot };
        var index = Path.Combine(steamRoot, "steamapps", "libraryfolders.vdf");

        if (!File.Exists(index))
        {
            return libraries;
        }

        foreach (var line in File.ReadAllLines(index))
        {
            var match = Regex.Match(line.Trim(), "^\s*\"path\"\s+\"(.+)\"$");
            if (match.Success)
            {
                libraries.Add(match.Groups[1].Value.Replace("\\\\", "\\"));
            }
        }

        return libraries;
    }


    /// <summary>Epic Games titles, read from the launcher's manifest files.</summary>
    private static void ScanEpic(List<GameInfo> found)
    {
        try
        {
            var manifests = Path.Combine(
                Environment.GetFolderPath(Environment.SpecialFolder.CommonApplicationData),
                "Epic", "EpicGamesLauncher", "Data", "Manifests");

            if (!Directory.Exists(manifests))
            {
                return;
            }

            foreach (var manifest in Directory.GetFiles(manifests, "*.item"))
            {
                using var document = JsonDocument.Parse(File.ReadAllText(manifest));
                var root = document.RootElement;

                var location = root.TryGetProperty("InstallLocation", out var locationValue) ? locationValue.GetString() : null;
                var name = root.TryGetProperty("DisplayName", out var nameValue) ? nameValue.GetString() : null;

                if (string.IsNullOrEmpty(location) || !Directory.Exists(location))
                {
                    continue;
                }

                AddGameFromFolder(found, location, "Epic", name);
            }
        }
        catch (Exception)
        {
        }
    }


    /// <summary>GOG installs, read from the launcher's registry entries.</summary>
    private static void ScanGog(List<GameInfo> found)
    {
        try
        {
            using var games = Registry.LocalMachine.OpenSubKey(@"SOFTWARE\WOW6432Node\GOG.com\Games");
            if (games is null)
            {
                return;
            }

            foreach (var keyName in games.GetSubKeyNames())
            {
                using var key = games.OpenSubKey(keyName);
                var path = key?.GetValue("path") as string;
                var name = key?.GetValue("gameName") as string;

                if (string.IsNullOrEmpty(path) || !Directory.Exists(path))
                {
                    continue;
                }

                AddGameFromFolder(found, path, "GOG", name);
            }
        }
        catch (Exception)
        {
        }
    }

    private static void AddGameFromFolder(List<GameInfo> found, string folder, string launcher, string? displayName = null)
    {
        var executable = FindMainExecutable(folder);
        if (executable is null)
        {
            return;
        }

        found.Add(new GameInfo
        {
            Name = string.IsNullOrWhiteSpace(displayName)
                ? Path.GetFileNameWithoutExtension(executable)
                : displayName!,
            ExecutablePath = executable,
            Launcher = launcher
        });
    }

    /// <summary>
    /// Looks in the install root and one level below, then keeps the largest candidate —
    /// in almost every shipped game that is the real executable.
    /// </summary>
    private static string? FindMainExecutable(string folder)
    {
        var candidates = new List<string>();

        try
        {
            candidates.AddRange(Directory.GetFiles(folder, "*.exe", SearchOption.TopDirectoryOnly));

            foreach (var subfolder in Directory.GetDirectories(folder))
            {
                try
                {
                    candidates.AddRange(Directory.GetFiles(subfolder, "*.exe", SearchOption.TopDirectoryOnly));
                }
                catch (UnauthorizedAccessException)
                {
                }
            }
        }
        catch (Exception)
        {
            return null;
        }

        return candidates
            .Where(path => !IgnoredExeTokens.Any(token => Path.GetFileName(path).Contains(token, StringComparison.OrdinalIgnoreCase)))
            .OrderByDescending(path => new FileInfo(path).Length)
            .FirstOrDefault();
    }

    private static string? ReadRegistryString(RegistryHive hive, string subKey, string valueName)
    {
        try
        {
            var view = Environment.Is64BitOperatingSystem ? RegistryView.Registry64 : RegistryView.Registry32;
            using var baseKey = RegistryKey.OpenBaseKey(hive, view);
            using var key = baseKey.OpenSubKey(subKey);
            return key?.GetValue(valueName) as string;
        }
        catch (Exception)
        {
            return null;
        }
    }
}
```

## README.md

```markdown
# FSR 4 Injector

A standalone **Windows desktop app (C# / WinUI 3)** that gives you one toggle to inject or remove an FSR 4
upscaling and frame-generation proxy wrapper in a game folder — with a hard safety guard so it can only be
pointed at **single-player, offline games**.

## Strict safety rule

The app refuses to inject into anything it recognises as a multiplayer or anti-cheat protected title. Three
independent checks run before a single byte is written:

1. **Exact executable block list** — `68` known multiplayer executables (`valorant.exe`, `cod.exe`, `apexlegends.exe`, …).
2. **Name-pattern block list** — `12` fragments such as `anticheat`, `battleye`, `faceitac`.
3. **Folder inspection** — `24` anti-cheat files and folders (EasyAntiCheat, BattlEye, `vgk.sys`, …). If one is installed next to the game, the game is blocked.

If a check fires, the toggle is disabled and an error banner explains why. There is no override.

## What the app does

- **One-button toggle.** On: copies your wrapper files (`dxgi.dll`, `nvngx.dll`, `OptiScaler.ini`) into the game folder.
  Off: restores every file it replaced and removes everything it added. Nothing is left behind.
- **Backups.** If the game already shipped a file with the same name, it is renamed to `*.fsr4backup` first and put back on the way out.
- **Single-player scanner.** Reads the installed Steam, Epic Games, GOG libraries, finds the main executable of each game, filters out everything the guard blocks and lists what is left.
- **Low overhead.** The app only manages files. All upscaling work runs inside the game process through the wrapper’s own GPU compute path — the injector itself idles when it is not toggling.

## Requirements

- Windows 10 1809 or newer (Windows 11 recommended).
- A 64-bit game running DirectX 12 for the wrapper to take effect.
- Your own legally obtained OptiScaler build in `Assets\FSR4_Files`.
- Visual Studio 2022 + .NET 8 SDK to build from source.

## Project files

- `FSR4Injector.csproj`
- `app.manifest`
- `App.xaml`
- `App.xaml.cs`
- `MainWindow.xaml`
- `MainWindow.xaml.cs`
- `Models/GameInfo.cs`
- `Safety/AntiCheatBlacklist.cs`
- `Services/InjectorService.cs`
- `Services/GameScanner.cs`
- `Assets/FSR4_Files/README.txt`

## Building

See `BUILD_WITH_VISUAL_STUDIO.md` for the full step-by-step, from installing Visual Studio to a
standalone `FSR4Injector.exe`.

## Honest limits

- This project ships **no** DLLs, no AMD code and no OptiScaler binaries — you supply them, and you are
  responsible for their licence.
- FSR 4 availability depends on your GPU, driver and the wrapper build you drop in. The app cannot make an
  unsupported GPU render FSR 4.
- Some publishers do not permit modifying game files at all. Single-player, offline only — check the EULA of
  the game you are modding.
- The published .exe is unsigned, so Windows SmartScreen will warn on first run until you sign it.
```

## BUILD_WITH_VISUAL_STUDIO.md

````markdown
# Build the .exe in Visual Studio

This project is **WinUI 3 (Windows App SDK) on .NET 8**, configured as an **unpackaged** app so it runs as a
plain .exe you can double-click — no MSIX install, no Store account.

## 1 · Install the tools

1. Download **Visual Studio 2022** (Community edition is free): https://visualstudio.microsoft.com/downloads/
2. In the installer, open the **Workloads** tab and tick **.NET Desktop Development**.
3. In the right-hand panel open **Installation details** and tick:
   - **Windows App SDK C# Templates**
   - **Windows 11 SDK (10.0.22621.0)** — or the newest Windows SDK offered
4. Install the **.NET 8 SDK** as well: https://dotnet.microsoft.com/download/dotnet/8.0
5. Restart Visual Studio after the installer finishes.

> The Windows App SDK workload is what gives you the WinUI 3 project templates and the build targets. Without
> the Windows App SDK C# Templates component you will not find the WinUI project type.

## 2 · Put the project on disk

**Option A — the bootstrap script (fastest).** The generator gives you `FSR4Injector-bootstrap.ps1`. Save it in an empty
folder, open PowerShell in that folder and run:

```powershell
powershell -ExecutionPolicy Bypass -File .\FSR4Injector-bootstrap.ps1
```

It writes every file — solution, project, XAML, C# sources and docs — into that folder. Then double-click
`FSR4Injector.sln`.

**Option B — start from the Visual Studio template.**

1. File → New → Project → search for `WinUI` → **Blank App, Packaged (WinUI 3 in Desktop)**.
2. Name it `FSR4Injector` and click Create.
3. Replace the template’s `App.xaml`, `App.xaml.cs`, `MainWindow.xaml` and
   `MainWindow.xaml.cs` with the versions from this generator.
4. Add the folders `Models`, `Safety`, `Services` and drop in
   `GameInfo.cs`, `AntiCheatBlacklist.cs`, `InjectorService.cs`, `GameScanner.cs`.
5. Add the `app.manifest` that ships with this generator next to the `.csproj`.
6. Open `FSR4Injector\FSR4Injector.csproj` and make two edits:
   - inside the first `<PropertyGroup>` add `<WindowsPackageType>None</WindowsPackageType>`
     so the app runs unpackaged as a normal .exe instead of an installed MSIX app;
   - add the `<None Update="Assets\…" CopyToOutputDirectory="PreserveNewest" />` item group so your
     wrapper files travel to the build output.

## 3 · Drop in the wrapper files

Create `Assets\FSR4_Files` in the project and copy your own OptiScaler build into it:

- `dxgi.dll`
- `nvngx.dll`
- `OptiScaler.ini`

The generator already ships a `README.txt` in that folder and a project item group that copies
everything inside it to the build output, so nothing else is needed. Keep the names exactly as they are in your
wrapper build — the app copies these exact file names.

> The project ships no binaries. Get the wrapper files from their official release page and respect their
> licence. Do not redistribute a wrapper build you are not allowed to share.

## 4 · Run it from Visual Studio

1. Set the toolbar platform to **x64** and the configuration to **Debug**.
2. Press **F5**. The first build takes a minute while NuGet restores the Windows App SDK.
3. Use it: **Select game executable…** (or **Scan** your libraries), watch the banner confirm the safety check,
   then flip the toggle. The status line under the toggle always tells you whether the game folder is currently
   injected or clean.

## 5 · Publish a standalone .exe

**From Visual Studio:** right-click the project → **Publish…** → target **Folder** → Configuration **Release**,
Target framework `net8.0-windows10.0.19041.0`, Target runtime **win-x64**, Deployment mode
**Self-contained** → **Publish**. The output lands in
`FSR4Injector\bin\x64\Release\net8.0-windows10.0.19041.0\win-x64\publish\FSR4Injector.exe` together with the wrapper assets.

**From the command line** — open **Tools → Terminal** in Visual Studio and run:

```powershell
dotnet publish FSR4Injector\FSR4Injector.csproj `
    -c Release -r win-x64 --self-contained true `
    -p:WindowsAppSDKSelfContained=true `
    -o .\publish
```

Both flags matter: `--self-contained true` bundles the .NET runtime and
`-p:WindowsAppSDKSelfContained=true` bundles the Windows App SDK, so the published folder runs on a machine
that has neither installed.

Keep the whole `publish` folder together — `FSR4Injector.exe` needs the DLLs and the
`Assets\FSR4_Files` folder beside it. If you want one physical file, copy the folder into a
self-extracting archive; single-file publishing with WinUI 3 is fragile and not worth the trouble here.

## 6 · Signing and SmartScreen

A freshly built .exe has no signature, so Windows shows "Windows protected your PC" the first time it runs.
Choose **More info → Run anyway**, or sign the executable with your own code-signing certificate:

```powershell
signtool sign /fd SHA256 /a /f mycert.pfx /p PASSWORD .\publish\FSR4Injector.exe
```

## 7 · Troubleshooting

- **"NETSDK1031: It is not supported to build or publish a self-contained application without specifying a RuntimeIdentifier."**
  The publish command needs `-r win-x64` (it is in the command above), or untick *self-contained* in the
  publish wizard.
- **The app closes immediately with a Windows App SDK dialog.** The Windows App SDK runtime is missing. Either
  install it, or publish with `-p:WindowsAppSDKSelfContained=true`.
- **"Wrapper assets are missing from …"** — the files are not in `Assets\FSR4_Files` or were
  not copied to the output. Check the folder next to the built .exe.
- **"Access to the path … is denied" when toggling.** The game folder needs write permission. Right-click the app
  and choose **Run as administrator**, or move the game out of `C:\Program Files`.
- **The file picker does nothing.** Unpackaged WinUI apps must hand the picker a window handle; the shipped
  `OnSelectGameClicked` already does this with `InitializeWithWindow`. If you rewrote it, put
  that call back.
- **The game still looks the same after injecting.** Only 64-bit DirectX 12 titles with a supported wrapper build
  react. Confirm your GPU and driver support the upscaler you are injecting, and check the wrapper’s own log file
  in the game folder.
- **"The project needs to be restored" / missing `Microsoft.UI.Xaml`.** Right-click the solution →
  **Restore NuGet Packages**, then rebuild.

## 8 · What the generated code does

- `MainWindow.xaml` — the window: guard banner, game picker, scanner, toggle and status line.
- `MainWindow.xaml.cs` — the event handlers, including the guard check that runs on every selection.
- `Safety/AntiCheatBlacklist.cs` — the three-layer block list and the `Inspect()` method.
- `Services/InjectorService.cs` — copy, back up, restore. The whole one-button toggle lives here.
- `Services/GameScanner.cs` — reads the Steam, Epic Games, GOG libraries and filters the results through the guard.
- `Models/GameInfo.cs` — one row in the detected-games list.

## 9 · Safety and legal notes

- The guard is intentionally not overridable. If you widen it, you take the ban risk yourself.
- Use it on single-player, offline titles only. Never on a game with an online mode you intend to play.
- Back up your saves and game configuration before injecting anything.
- The injector only manages files. All upscaling runs in the game process through your wrapper build, which
  stays responsible for any effect on performance or stability.
````

## FSR4Injector/Assets/FSR4_Files/README.txt

```text
FSR 4 Injector — wrapper assets

Put your own wrapper files in this folder:

  dxgi.dll
  nvngx.dll
  OptiScaler.ini

These exact file names are copied into the chosen game folder when the toggle is switched on, and removed
(or restored from their .fsr4backup copies) when it is switched off.

The project ships no binaries. Take the files from the official release page of the wrapper you use, keep the
licence terms that come with them, and do not redistribute a build you are not allowed to share.

Injected game folders are only ever touched by the app you built from this source.
```
