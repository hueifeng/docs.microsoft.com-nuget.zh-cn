- <span data-ttu-id="cfcbf-101">**包管理器 UI** (Visual Studio)：右键单击“解决方案资源管理器”中的解决方案，选择“还原 NuGet 包”。</span><span class="sxs-lookup"><span data-stu-id="cfcbf-101">**Package Manager UI** (Visual Studio): right-click the solution in Solution Explorer and select **Restore NuGet Packages**.</span></span> <span data-ttu-id="cfcbf-102">如果一个或多个独立包仍未正确安装（即“解决方案资源管理器”显示错误图标），请使用包管理器 UI 卸载受影响的包并重新安装。</span><span class="sxs-lookup"><span data-stu-id="cfcbf-102">If one or more individual packages are still not installed properly (meaning that Solution Explorer shows an error icon), then use the Package Manager UI to uninstall the affected packages and reinstall them.</span></span> <span data-ttu-id="cfcbf-103">请参阅[重新安装和更新包](../Consume-Packages/Reinstalling-and-Updating-Packages.md)</span><span class="sxs-lookup"><span data-stu-id="cfcbf-103">See [Reinstalling and updating packages](../Consume-Packages/Reinstalling-and-Updating-Packages.md)</span></span>

- <span data-ttu-id="cfcbf-104">**命令行**：使用 [nuget restore](../tools/cli-ref-restore.md) 命令。</span><span class="sxs-lookup"><span data-stu-id="cfcbf-104">**Command line**: use the [nuget restore](../tools/cli-ref-restore.md) command.</span></span> <span data-ttu-id="cfcbf-105">运行项目文件夹中的 `nuget restore` 即可尝试还原项目的依赖项。</span><span class="sxs-lookup"><span data-stu-id="cfcbf-105">Simply running `nuget restore` in the project folder attempts to restore the project's dependencies.</span></span>