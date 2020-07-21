---
title: 'Lección 1: crear el proyecto de Visual Studio de esquema RDL | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: f420509c-51aa-4170-8c25-64c2954f4bb9
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: c34062acefc2dfd847790a39cea35b03727f49ff
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62678523"
---
# <a name="lesson-1-create-the-rdl-schema-visual-studio-project"></a>Lección 1: Creación del proyecto de Visual Studio Esquema RDL
  Para este tutorial creará una aplicación de consola sencilla. En este tutorial se da por supuesto [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vs_dev10_long](../includes/vs-dev10-long-md.md)]que está desarrollando en.  
  
> [!NOTE]  
>  Al tener acceso al servicio web del servidor de informes que se ejecuta en [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] con Advanced Services, debe agregar "?SQLExpress" a la ruta de acceso de "ReportServer". Por ejemplo:  
>   
>  `http://myserver/reportserver_sqlexpress/reportservice2010.asmx"`  
  
### <a name="to-create-the-web-service-proxy"></a>Crear el proxy del servicio web  
  
1.  En el menú **Inicio** , seleccione **todos los programas**, Microsoft Visual Studio, **Visual Studio Tools**y, por último, **símbolo del sistema de Visual Studio 2010**.  
  
2.  En la ventana del símbolo del sistema, ejecute el siguiente comando si está utilizando C#:  
  
    ```  
    wsdl /language:CS /n:"ReportService2010" http://<Server Name>/reportserver/reportservice2010.asmx?wsdl  
    ```  
  
     Si usa Visual Basic, ejecute el siguiente comando:  
  
    ```  
    wsdl /language:VB /n:"ReportService2010" http://<Server Name>/reportserver/reportservice2010.asmx?wsdl  
    ```  
  
     Este comando genera un archivo .cs o .vb. Agregará este archivo a su aplicación.  
  
### <a name="to-create-a-console-application"></a>Crear una aplicación de consola  
  
1.  En el menú **archivo** , seleccione **nuevo**y, a continuación, haga clic en **proyecto** para abrir el cuadro de diálogo **nuevo proyecto** .  
  
2.  En el panel izquierdo, en **plantillas instaladas**, haga clic en **Visual Basic** o en el nodo **Visual C#** y seleccione una categoría de tipos de proyecto en la lista expandida.  
  
3.  Elija el tipo de proyecto **aplicación de consola** .  
  
4.  En el cuadro **nombre** , escriba un nombre para el proyecto. Escriba el nombre `SampleRDLSchema`.  
  
5.  En el cuadro **Ubicación** , escriba la ruta de acceso donde desea guardar el proyecto o haga clic en **examinar** para navegar hasta la carpeta.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]En Explorador de soluciones se muestra una vista contraída del proyecto.  
  
7.  En el menú **Proyecto** , haga clic en **Agregar elemento existente**.  
  
8.  Navegue hasta la ubicación del archivo. cs o. VB que ha generado, seleccione el archivo y, a continuación, haga clic en **Agregar**.  
  
     También necesitará agregar una referencia al espacio de nombres <xref:System.Web.Services> para que su referencia web funcione.  
  
9. En el menú Proyecto, haga clic en **Agregar referencia**.  
  
     En el cuadro de diálogo **Agregar referencia** , en la pestaña **.net** , seleccione **System. Web. Services**y, a continuación, haga clic en **Aceptar**.  
  
     Para obtener más información sobre cómo conectarse al servicio Web del servidor de informes, vea [compilar aplicaciones con el servicio Web y el .NET Framework](../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md).  
  
10. Expanda el nodo del proyecto en el Explorador de soluciones. Verá que se ha agregado un archivo de código con el nombre predeterminado Program.cs (Module1.vb para [!INCLUDE[vbprvb](../includes/vbprvb-md.md)]) al proyecto.  
  
11. Abra el archivo Program.cs (Module1.vb para [!INCLUDE[vbprvb](../includes/vbprvb-md.md)]) y reemplace el código por lo siguiente:  
  
     El siguiente código proporciona los códigos auxiliares del método que se utilizarán para implementar funcionalidad para cargar, actualizar y guardar.  
  
    ```csharp  
    using System;  
    using System.Collections.Generic;  
    using System.IO;  
    using System.Text;  
    using System.Xml;  
    using System.Xml.Serialization;  
    using ReportService2010;  
  
    namespace SampleRDLSchema  
    {  
        class ReportUpdater  
        {  
            ReportingService2010 _reportService;  
  
            static void Main(string[] args)  
            {  
                ReportUpdater reportUpdater = new ReportUpdater();  
                reportUpdater.UpdateReport();  
            }  
  
            private void UpdateReport()  
            {  
                try  
                {  
                    // Set up the Report Service connection  
                    _reportService = new ReportingService2010();  
                    _reportService.Credentials =  
                        System.Net.CredentialCache.DefaultCredentials;  
                    _reportService.Url =  
                       "http://<Server Name>/reportserver/" +  
                                       "reportservice2010.asmx";  
  
                    // Call the methods to update a report definition  
                    LoadReportDefinition();  
                    UpdateReportDefinition();  
                    PublishReportDefinition();  
                }  
                catch (Exception ex)  
                {  
                    System.Console.WriteLine(ex.Message);  
                }  
            }  
  
            private void LoadReportDefinition()  
            {  
                //Lesson 3: Load a report definition from the report   
                //          catalog  
            }  
  
            private void UpdateReportDefinition()  
            {  
                //Lesson 4: Update the report definition using the    
                //          classes generated from the RDL Schema  
            }  
  
            private void PublishReportDefinition()  
            {  
                //Lesson 5: Publish the updated report definition back   
                //          to the report catalog  
            }  
        }  
    }  
    ```  
  
    ```vb  
    Imports System  
    Imports System.Collections.Generic  
    Imports System.IO  
    Imports System.Text  
    Imports System.Xml  
    Imports System.Xml.Serialization  
    Imports ReportService2010  
  
    Namespace SampleRDLSchema  
  
        Module ReportUpdater  
  
            Private m_reportService As ReportingService2010  
  
            Public Sub Main(ByVal args As String())  
  
                Try  
                    'Set up the Report Service connection  
                    m_reportService = New ReportingService2010  
                    m_reportService.Credentials = _  
                        System.Net.CredentialCache.DefaultCredentials  
                    m_reportService.Url = _  
                        "http:// <Server Name>/reportserver/" & _  
                               "reportservice2010.asmx"  
  
                    'Call the methods to update a report definition  
                    LoadReportDefinition()  
                    UpdateReportDefinition()  
                    PublishReportDefinition()  
                Catch ex As Exception  
                    System.Console.WriteLine(ex.Message)  
                End Try  
  
            End Sub  
  
            Private Sub LoadReportDefinition()  
                'Lesson 3: Load a report definition from the report   
                '          catalog  
            End Sub  
  
            Private Sub UpdateReportDefinition()  
                'Lesson 4: Update the report definition using the   
                '          classes generated from the RDL Schema  
            End Sub  
  
            Private Sub PublishReportDefinition()  
                'Lesson 5: Publish the updated report definition back   
                '          to the report catalog  
            End Sub  
  
        End Module  
  
    End Namespace   
    ```  
  
## <a name="next-lesson"></a>Lección siguiente  
 En la siguiente lección utilizará la herramienta de definición de esquemas XML (Xsd.exe) para generar clases a partir del esquema RDL e incluirlas en el proyecto. Vea [Lección 2: generar clases a partir del esquema RDL con la herramienta XSD](../../2014/tutorials/lesson-2-generate-classes-from-the-rdl-schema-using-the-xsd-tool.md).  
  
## <a name="see-also"></a>Consulte también  
 [Actualizar informes con clases generadas a partir del esquema RDL &#40;tutorial de SSRS&#41;](../../2014/tutorials/updating-reports-using-classes-generated-from-the-rdl-schema-ssrs-tutorial.md)   
 [Lenguaje RDL (Report Definition Language) &#40;SSRS&#41;](../reporting-services/reports/report-definition-language-ssrs.md)  
  
  
