---
title: Migrar de ADO MD a ADOMD.NET | Documentos de Microsoft
ms.custom: 
ms.date: 02/14/2018
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- ADOMD.NET, migrating to
- migrating ADO MD to ADOMD.NET
- ADO MD migration [ADOMD.NET]
ms.assetid: 8c760db3-c475-468e-948d-e5f599d985ad
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 5cfe7226ee90f7333a5a80abcc0590212b15576e
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/15/2018
---
# <a name="migrating-from-ado-md-to-adomdnet"></a>Migrar de ADO MD a ADOMD.NET
  La biblioteca de ADOMD.NET es similar a la biblioteca de ActiveX Data Objects Multidimensional (ADO MD), una extensión de la biblioteca de Objetos de datos ActiveX (ADO) que se utiliza para tener acceso a datos multidimensionales en aplicaciones cliente basadas en el Modelo de objetos componentes (COM). ADO MD proporciona un acceso fácil a los datos multidimensionales de lenguajes no administrados como C++ y [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic. ADOMD.NET proporciona un acceso fácil a los datos analíticos (tanto multidimensionales como de minería de datos) de lenguajes administrados como [!INCLUDE[msCoName](../../includes/msconame-md.md)] C# y [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic .NET. Además, ADOMD.NET proporciona un modelo de objetos de metadatos mejorado.  
  
 Migrar las aplicaciones cliente existentes de ADO MD a ADOMD.NET resulta fácil, pero hay varias diferencias importantes con respecto a la migración:  
  
 **Para proporcionar acceso a datos y conectividad a las aplicaciones cliente**  
 |ADO MD|ADOMD.NET|  
|------------|---------------|  
|Requiere referencias a Adodb.dll y Adomd.dll.|Requiere una única referencia a Microsoft.AnalysisServices.AdomdClient.dll.|  
  
 La clase <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> proporciona compatibilidad de conectividad, además de acceso a metadatos.  
  
 **Para recuperar los metadatos para objetos multidimensionales**  
 |ADO MD|ADOMD.NET|  
|------------|---------------|  
|Utilice la clase de catálogo.|Utilice la propiedad <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.Cubes%2A> de <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>.|  
  
 **Para ejecutar consultas y devolver objetos cellset**  
 |ADO MD|ADOMD.NET|  
|------------|---------------|  
|Utilice la clase de conjunto de celdas.|Utilice la clase <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand>.|  
  
 **Para obtener acceso a los metadatos que se usan para mostrar un conjunto de celdas**  
 |ADO MD|ADOMD.NET|  
|------------|---------------|  
|Utilice la clase de posición.|Utilice los objetos <xref:Microsoft.AnalysisServices.AdomdClient.Set> y <xref:Microsoft.AnalysisServices.AdomdClient.Tuple>.|  
  
> [!NOTE]  
>  La clase <xref:Microsoft.AnalysisServices.AdomdClient.Position> se admite para la compatibilidad con versiones anteriores.  
  
 **Para recuperar metadatos del modelo de minería de datos**  
 En ADO MD no hay ninguna clase disponible. En ADOMD.NET usa una de las colecciones de minería de datos:  
  
-   <xref:Microsoft.AnalysisServices.AdomdClient.MiningModelCollection> contiene una lista de cada modelo de minería de datos del origen de datos.  
  
-   <xref:Microsoft.AnalysisServices.AdomdClient.MiningServiceCollection> proporciona información sobre los algoritmos de minería de datos disponibles.  
  
-   <xref:Microsoft.AnalysisServices.AdomdClient.MiningStructureCollection> expone información sobre las estructuras de minería de datos del servidor.  
  
 Para resaltar estas diferencias, el ejemplo de migración siguiente compara una aplicación existente de ADO MD con una aplicación equivalente de ADOMD.NET.  
  
## <a name="looking-at-a-migration-example"></a>Ejemplo de migración  
 Los ejemplos del código existente de ADO MD y el equivalente de ADOMD.NET que se muestran en esta sección realizan el mismo conjunto de acciones: crear una conexión, ejecutar una instrucción MDX (Expresiones multidimensionales) y recuperar metadatos y datos. Sin embargo, estos dos conjuntos de código no utilizan los mismos objetos para realizar dichas tareas.  
  
### <a name="existing-ado-md-code"></a>Código existente de ADO MD  
 El ejemplo de código siguiente, extraído de la documentación de ADO MD 2.8, está escrito en [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic® 6.0 y utiliza ADO MD para mostrar cómo consultar y conectarse a un [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] origen de datos. En este ejemplo de ADO MD se utiliza los objetos siguientes:  
  
-   Crea una conexión desde un **catálogo** objeto.  
  
-   Ejecuta la instrucción de expresiones multidimensionales (MDX) mediante la **Cellset** objeto.  
  
-   Recupera los metadatos y los datos de la **posición** objeto, recuperado desde el **Cellset** objeto.  
  
```  
Private Sub cmdCellSettoDebugWindow_Click()  
Dim cat As New ADOMD.Catalog  
Dim cst As New ADOMD.Cellset  
Dim i As Integer  
Dim j As Integer  
Dim k As Integer  
Dim strServer As String  
Dim strSource As String  
Dim strColumnHeader As String  
Dim strRowText As String  
  
On Error GoTo Error_cmdCellSettoDebugWindow_Click  
Screen.MousePointer = vbHourglass  
'*-----------------------------------------------------------------------  
'* Set server to local host.  
'*-----------------------------------------------------------------------  
    strServer = "LOCALHOST"  
  
'*-----------------------------------------------------------------------  
'* Set MDX query string source.  
'*-----------------------------------------------------------------------  
    strSource = strSource & "SELECT "  
    strSource = strSource & "{[Measures].members} ON COLUMNS,"  
    strSource = strSource & _  
        "NON EMPTY [Store].[Store City].members ON ROWS"  
    strSource = strSource & " FROM Sales"  
  
'*-----------------------------------------------------------------------  
'* Set active connection.  
'*-----------------------------------------------------------------------  
        cat.ActiveConnection = "Data Source=" & strServer & _  
            ";Provider=msolap;"  
  
'*-----------------------------------------------------------------------  
'* Set cellset source to MDX query string.  
'*-----------------------------------------------------------------------  
        cst.Source = strSource  
  
'*-----------------------------------------------------------------------  
'* Set cellset active connection to current connection  
'*-----------------------------------------------------------------------  
    Set cst.ActiveConnection = cat.ActiveConnection  
  
'*-----------------------------------------------------------------------  
'* Open cellset.  
'*-----------------------------------------------------------------------  
    cst.Open  
  
'*-----------------------------------------------------------------------  
'* Allow space for row header text.  
'*-----------------------------------------------------------------------  
strColumnHeader = vbTab & vbTab & vbTab & vbTab & vbTab & vbTab  
  
'*-----------------------------------------------------------------------  
'* Loop through column headers.  
'*-----------------------------------------------------------------------  
       For i = 0 To cst.Axes(0).Positions.Count - 1  
            strColumnHeader = strColumnHeader & _  
                cst.Axes(0).Positions(i).Members(0).Caption & vbTab & _  
                    vbTab & vbTab & vbTab  
       Next  
       Debug.Print vbTab & strColumnHeader & vbCrLf  
  
'*-----------------------------------------------------------------------  
'* Loop through row headers and provide data for each row.  
'*-----------------------------------------------------------------------  
        strRowText = ""  
        For j = 0 To cst.Axes(1).Positions.Count - 1  
            strRowText = strRowText & _  
                cst.Axes(1).Positions(j).Members(0).Caption & vbTab & _  
                    vbTab & vbTab & vbTab  
            For k = 0 To cst.Axes(0).Positions.Count - 1  
                strRowText = strRowText & cst(k, j).FormattedValue & _  
                    vbTab & vbTab & vbTab & vbTab  
            Next  
            Debug.Print strRowText & vbCrLf  
            strRowText = ""  
        Next  
  
    Screen.MousePointer = vbDefault  
Exit Sub  
  
Error_cmdCellSettoDebugWindow_Click:  
   Beep  
   Screen.MousePointer = vbDefault  
   MsgBox "The following error has occurred:" & vbCrLf & _  
      Err.Description, vbCritical, " Error!"  
   Exit Sub  
End Sub  
```  
  
### <a name="equivalent-adomdnet-code"></a>Código de ADOMD.NET equivalente  
 En el ejemplo siguiente, escrito en Visual Basic .NET y en el que se utiliza ADOMD.NET, se muestra cómo realizar las mismas acciones que en el ejemplo anterior de Visual Basic 6.0. La diferencia principal entre el ejemplo siguiente y el ejemplo de ADO MD mostrado anteriormente son los objetos que se utilizan para realizar las acciones. En el ejemplo del ADOMD.NET se utilizan los objetos siguientes:  
  
-   Crea una conexión con un **AdomdConnection** objeto.  
  
-   Se ejecuta la instrucción MDX mediante un **AdomdCommand** objeto.  
  
-   Recupera los metadatos y los datos de la **establecer** objeto, recuperado desde el **Cellset** objeto.  
  
```  
Private Sub DisplayCellSetInOutputWindow()  
    Dim conn As AdomdConnection  
    Dim cmd As AdomdCommand  
    Dim cst As CellSet  
    Dim i As Integer  
    Dim j As Integer  
    Dim k As Integer  
    Dim strServer As String = "LOCALHOST"  
    Dim strSource As String = "SELECT [Measures].members ON COLUMNS, " & _  
        "NON EMPTY [Store].[Store City].members ON ROWS FROM SALES"  
    Dim strOutput As New System.IO.StringWriter  
  
    '*-----------------------------------------------------------------------  
    '* Open connection.  
    '*-----------------------------------------------------------------------  
    Try  
        ' Create a new AdomdConnection object, providing the connection  
        ' string.  
        conn = New AdomdConnection("Data Source=" & strServer & _  
        ";Provider=msolap;")  
        ' Open the connection.  
        conn.Open()  
    Catch ex As Exception  
        Throw New ApplicationException( _  
            "An error occurred while connecting.")  
    End Try  
  
    Try  
    '*-----------------------------------------------------------------------  
    '* Open cellset.  
    '*-----------------------------------------------------------------------  
        ' Create a new AdomdCommand object, providing the MDX query string.  
        cmd = New AdomdCommand(strSource, conn)  
        ' Run the command and return a CellSet object.  
        cst = cmd.ExecuteCellSet()  
  
    '*-----------------------------------------------------------------------  
    '* Concatenate output.  
    '*-----------------------------------------------------------------------  
  
    ' Include spacing to account for row headers.  
    strOutput.Write(vbTab, 6)  
  
    ' Iterate through the first axis of the CellSet object and  
    ' retrieve column headers.  
    For i = 0 To cst.Axes(0).Set.Tuples.Count - 1  
        strOutput.Write(cst.Axes(0).Set.Tuples(i).Members(0).Caption)  
        strOutput.Write(vbTab, 4)  
    Next  
    strOutput.WriteLine()  
  
    ' Iterate through the second axis of the CellSet object and  
    ' retrieve row headers and cell data.  
    For j = 0 To cst.Axes(1).Set.Tuples.Count - 1  
        ' Append the row header.  
        strOutput.Write(cst.Axes(1).Set.Tuples(j).Members(0).Caption)  
        strOutput.Write(vbTab, 4)  
  
        ' Append the cell data for that row.  
        For k = 0 To cst.Axes(0).Set.Tuples.Count - 1  
            strOutput.Write(cst.Cells(k, j).FormattedValue)  
            strOutput.Write(vbTab, 4)  
        Next  
        strOutput.WriteLine()  
    Next  
  
    ' Display the output.  
    Debug.WriteLine(strOutput.ToString)  
  
    '*-----------------------------------------------------------------------  
    '* Release resources.  
    '*-----------------------------------------------------------------------  
        conn.Close()  
    Catch ex As Exception  
        ' Ignore or handle errors.  
    Finally  
        cst = Nothing  
        cmd = Nothing  
        conn = Nothing  
    End Try  
End Sub  
```  
  
  
