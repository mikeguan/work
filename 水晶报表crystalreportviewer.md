# 水晶报表
CrystalReportViewer 成员请参见
CrystalReportViewer 类 | CrystalDecisions.Web 命名空间
公共实例属性
BestFitPage Boolean。获取或设置页面视图是大小合适还是用滚动条进行裁剪。 
BorderStyle BorderStyle。获取或设置控件周围的边框样式。 
ClientTarget String。获取或设置为不同浏览器渲染的目标。有效值有“ie4”、“ie5”、“Uplevel”、“Downlevel”和“Auto”。 
DisplayGroupTree Boolean。获取或设置树视图是可见还是隐藏。 
DisplayPage Boolean。获取或设置页面视图是可见还是隐藏。 
DisplayToolbar Boolean。获取或设置工具栏是可见还是隐藏。 
DrilldownTarget String。获取或设置深化将回发到的框架目标。 
EnableDrillDown Boolean。获取或设置是否启用深化到页面/图表/汇总。 
EnterpriseLogon（从 CrystalReportViewerbase 继承） Object。获取或设置企业报表的登录信息。EnterpriseLogon 属性接受 Crystal Enterprise 登录标记（如“FORTE4@639JVZn'*_}j1E\$k0$”）或 CrystalDecisions.Enterprise.Framework.ISEnterpriseSession 会话对象。 
注意   此属性供将来使用。 
HasDrillUpButton Boolean。获取或设置浅化按钮的可见性。浅化按钮用于在执行一个或多个深化操作后返回上一级视图。 
HasExportButton Boolean。获取或设置工具栏上的导出按钮是可见还是隐藏。 
HasGotoPageButton Boolean。获取或设置工具栏上的转到页按钮是可见还是隐藏。 
HasPageNavigationButtons Boolean。获取或设置工具栏上的页面导航按钮是可见还是隐藏。 
HasPrintButton Boolean。获取或设置工具栏上的打印按钮是可见还是隐藏。 
HasRefreshButton Boolean。获取或设置工具栏上的刷新按钮是可见还是隐藏。 
HasSearchButton Boolean。获取或设置工具栏上的搜索按钮是可见还是隐藏。 
HasToggleGroupTreeButton Boolean。获取或设置工具栏上的显示/隐藏组树按钮是可见还是隐藏。 
HasZoomFactorList Boolean。获取或设置工具栏上的缩放因数列表是可见还是隐藏。 
HyperlinkTarget String。确定是在新的浏览器窗口中还是在现有的浏览器窗口中打开 Web 页。 
除了下列以下划线开头的特殊值外，用于加载 Web 页内容的目标窗口或框架的值必须以 a 到 z 之间的字母开头：

_blank - 在无框架的新窗口中呈现内容。 

_parent - 在上一级框架集父窗口中呈现内容。 

_self - 在具有焦点的框架中呈现内容。 

_top - 在无框架的全窗口中呈现内容。
 
LogOnInfo（从 CrystalReportViewerbase 继承） TableLogOnInfos。获取或设置 TableLogOnInfos 集合。 
PageToTreeRatio Float64。设置组树与报表视图之间的大小比例。  
PageZoomFactor Integer。获取或设置报表的缩放因数。 
ParameterFieldInfo（从 CrystalReportViewerbase 继承） ParameterFields。获取或设置参数字段集合。 
ReportSource（从 CrystalReportViewerbase 继承） Object。获取或设置要绑定到查看器的报表。 
报表的源可以是下列之一： 

*.rpt 文件的绝对路径，例如“c:\myreports\report.rpt”。 
以“ras://”开头的 URI，例如“ras://c:\report.rpt”。这会在报表应用程序服务器 (RAS) 上打开报表，并且它要求 RAS 客户端。将使用的 RAS 服务器取自 HKEY_LOCAL_MACHINE\SOFTWARE\Crystal Decisions\9.0\Report App\Client SDK\DefaultReportAppServerConfigFile 注册表项。 
以“rassdk://”开头的 URI，例如，“rassdk://c:\report.rpt”。这会在客户端上打开报表，然后将文件传送到服务器。此报表源要求 RAS 客户端。所使用的 RAS 服务器取自 DefaultReportAppServerConfigFile 注册表项。 
以“ceis://@cms/#115”开头的 URI。此报表源使用报表的 InfoObject ID 从 Crystal Enterprise CMS 服务器打开报表。需要设置查看器的 EnterpriseLogon 属性以指定 Enterprise 登录信息。 
注意   必须安装了 Crystal Enterprise .NET 客户端才能使用此功能。
指向报表 Web 服务的“http://machinename/directory/webservice.asmx”形式的 URI。若要为 Web 服务指定登录信息，请使用 wsdl.exe 或 VS .NET 生成的 SoapHttpClientProtocol 代理，或者使用 CrystalDecisions.Shared.RemoteReportProxy。 
非类型化 ReportDocument 对象。 
有关更多信息，请参见非类型化报表组件。 

强类型 ReportDocument（已缓存的和未缓存的）。 
有关更多信息，请参见 Web 项目中的强类型报表组件。 

CrystalDecisions.ReportAppServer.ClientDoc.ReportClientDocument 对象。这只是 COM ReportClientDocument 类的 .NET Interop 包装。 
具有类似“http://MyServer/ServerProject/My ReportService.asmx”的 URL 的 SoapHttpClientProtocol 或 CrystalDecisions.Shared.RemoteReportProxy 对象。可以使用 Credentials 属性指定 Web 服务器的身份验证设置。 
有关更多信息，请参见作为 Web 服务的报表。
 
ReportSourceClassFactoryName（从 CrystalReportViewerbase 继承） String。获取或设置创建内部 Reportsource 对象所需的信息。此对象确定查看器如何使用报表源。当前的默认设置为“CrystalDecisions.ReportSource.ReportSourceFactory,CrystalDecisions.ReportSource, Version=9.2.3300.0, Culture=neutral, PublicKeyToken=692fbea5521e1304”。 
注意   此属性供将来使用。 
SelectionFormula（从 CrystalReportViewerbase 继承） String。获取或设置报表的记录选定公式。 
SeparatePages Boolean。获取或设置报表页是分开还是连接。 
ShowAllPageIds Boolean。获取或设置是否在 HTML中给出报表对象 ID。 
TabIndex Short。指定控件的 Tab 键顺序。
