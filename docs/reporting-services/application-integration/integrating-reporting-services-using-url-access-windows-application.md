---
title: "Mediante el acceso URL en una aplicación de Windows | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Windows applications [Reporting Services]
- Web Browser controls [Reporting Services]
- Windows Forms [Reporting Services]
- browser controls [Reporting Services]
- URL access [Reporting Services], Windows applications
ms.assetid: a4b222e5-0cbd-409c-92c4-046a674db8ac
caps.latest.revision: 48
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: 782be214cb491e1fdddf6ff7d45ac377fcfbf8a4
ms.contentlocale: es-es
ms.lasthandoff: 08/12/2017

---
# <a name="integrating-reporting-services-using-url-access---windows-application"></a>Integración de Reporting Services mediante el acceso URL - aplicación de Windows
  Aunque el acceso URL a un servidor de informes se optimiza para un entorno web, también puede utilizar el acceso URL para incrustar informes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en una aplicación para [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows. Sin embargo, el acceso URL que implica formularios Windows Forms todavía requiere que use la tecnología del explorador web. Puede utilizar los escenarios de integración siguientes con el acceso URL y los formularios Windows Forms:  
  
-   Mostrar un informe de una aplicación de formulario Windows Forms iniciando mediante programación un explorador web.  
  
-   Usar el control <xref:System.Windows.Forms.WebBrowser> en un formulario Windows Forms para mostrar un informe.  
  
## <a name="starting-internet-explorer-from-a-windows-form"></a>Iniciar Internet Explorer desde un formulario Windows Forms  
 Puede utilizar la clase <xref:System.Diagnostics.Process> para tener acceso a un proceso que se está ejecutando en un equipo. El <xref:System.Diagnostics.Process> clase es útil [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] construcción para iniciar, detener, controlar y supervisar aplicaciones. Para ver un informe específico en la base de datos del servidor de informes, puede iniciar el **IExplore** proceso, pasando la dirección URL para el informe. El ejemplo de código siguiente se puede utilizar para iniciar [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Explorer y una dirección URL de un informe concreto cuando el usuario hace clic en un botón de un formulario Windows Forms.  
  
```vb  
Private Sub viewReportButton_Click(ByVal sender As Object, ByVal e As System.EventArgs) Handles viewReportButton.Click  
   ' Build the URL access string based on values supplied by a user  
   Dim url As String = serverUrlTextBox.Text + "?" & reportPathTextBox.Text & _  
   "&rs:Command=Render" & "&rs:Format=HTML4.0"  
  
   ' If the user does not select the toolbar check box,  
   ' turn the toolbar off in the HTML Viewer  
   If toolbarCheckBox.Checked = False Then  
      url += "&rc:Toolbar=False"  
   End If  
   ' load report in the Web browser  
   Try  
      System.Diagnostics.Process.Start("IExplore", url)  
   Catch  
      MessageBox.Show("The system could not start the specified report using Internet Explorer.", _  
      "An error has occurred", MessageBoxButtons.OK, MessageBoxIcon.Error)  
   End Try  
End Sub 'viewReportButton_Click  
```  
  
```csharp  
// Sample click event for a Button control on a Windows Form  
private void viewReportButton_Click(object sender, System.EventArgs e)  
{  
   // Build the URL access string based on values supplied by a user  
   string url = serverUrlTextBox.Text + "?" + reportPathTextBox.Text +  
      "&rs:Command=Render" + "&rs:Format=HTML4.0";  
  
   // If the user does not check the toolbar check box,  
   // turn the toolbar off in the HTML Viewer  
   if (toolbarCheckBox.Checked == false)  
      url += "&rc:Toolbar=False";  
  
   // load report in the Web browser  
   try  
   {  
      System.Diagnostics.Process.Start("IExplore", url);  
   }  
  
   catch (Exception)  
   {  
      MessageBox.Show(  
         "The system could not open the specified report using Internet Explorer.",   
         "An error has occurred", MessageBoxButtons.OK, MessageBoxIcon.Error);  
   }  
}  
```  
  
## <a name="embedding-a-browser-control-on-a-windows-form"></a>Incrustar un control de explorador en un formulario Windows Forms  
 Si no desea ver un informe en un explorador web externo, puede incrustar un explorador web fácilmente como parte de un formulario Windows Forms utilizando el control <xref:System.Windows.Forms.WebBrowser>.  
  
###### <a name="to-add-the-webbrowser-control-to-your-windows-form"></a>Para agregar el control WebBrowser al formulario Windows Forms  
  
1.  Cree una nueva aplicación de Windows en la vista [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[csprcs](../../includes/csprcs-md.md)] o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)].  
  
2.  Busque la <xref:System.Windows.Forms.WebBrowser> controlar en el **cuadro de herramientas** cuadro de diálogo.  
  
     Si el **cuadro de herramientas** es no es visible puede obtener acceso a él haciendo clic en el **vista** elemento de menú y seleccionando **cuadro de herramientas**.  
  
3.  Arrastre el <xref:System.Windows.Forms.WebBrowser>control en la superficie de diseño del formulario Windows Forms.  
  
     El <xref:System.Windows.Forms.WebBrowser>control denominado webBrowser1 se agrega al formulario  
  
 Usted nos los <xref:System.Windows.Forms.WebBrowser> control a una dirección URL mediante una llamada a su **Navigate** método. Puede asignar una cadena de acceso URL concreta al control <xref:System.Windows.Forms.WebBrowser> en tiempo de ejecución como se muestra en el ejemplo siguiente.  
  
```vb  
Dim url As String = "http://localhost/reportserver?/" & _  
                    "AdventureWorks2012 Sample Reports/" & _  
                    "Company Sales&rs:Command=Render"  
WebBrowser1.Navigate(url)  
```  
  
```csharp  
string url = "http://localhost/reportserver?/" +  
             "AdventureWorks2012 Sample Reports/" +  
             "Company Sales&rs:Command=Render";  
webBrowser1.Navigate(url);  
```  
  
## <a name="see-also"></a>Vea también  
 [Integración de Reporting Services en aplicaciones](../../reporting-services/application-integration/integrating-reporting-services-into-applications.md)   
 [Integración de Reporting Services mediante el acceso URL](../../reporting-services/application-integration/integrating-reporting-services-using-url-access.md)   
 [Integrar Reporting Services con SOAP](../../reporting-services/application-integration/integrating-reporting-services-using-soap.md)   
 [Integrar Reporting Services con los controles ReportViewer](../../reporting-services/application-integration/integrating-reporting-services-using-reportviewer-controls.md)   
 [Acceso URL &#40; SSRS &#41;](../../reporting-services/url-access-ssrs.md)  
  
  
