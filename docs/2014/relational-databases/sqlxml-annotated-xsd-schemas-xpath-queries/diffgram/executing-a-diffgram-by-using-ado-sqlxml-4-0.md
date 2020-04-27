---
title: Ejecutar un DiffGram mediante ADO (SQLXML 4,0) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- providers [SQLXML], SQLOLEDB Provider
- ADO [SQLXML]
- SQLXMLOLEDB Provider, DiffGrams
- data providers [SQLXML], SQLOLEDB Provider
- DiffGrams [SQLXML], ADO
ms.assetid: 741fce82-de83-4923-86eb-30acb5b9a5e6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ac11a4f5f697e2b2cd0c27a56940a7183c6231da
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66012480"
---
# <a name="executing-a-diffgram-by-using-ado-sqlxml-40"></a>Ejecutar un DiffGram utilizando ADO (SQLXML 4.0)
  Esta aplicación de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic utiliza ADO para establecer una conexión a una instancia de Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y después ejecuta un DiffGram. En esta aplicación, el DiffGram y el esquema XSD están almacenados en un archivo. La aplicación carga el DiffGram del archivo especificado. Puede usar cualquiera de los DiffGrams (y el esquema XSD asociado) descrito en los [ejemplos de DiffGram](diffgram-examples-sqlxml-4-0.md).  
  
 Éste es el proceso de la aplicación de ejemplo:  
  
-   Objeto **Conn** (**ADODB. Conexión**) establece una conexión a una instancia en ejecución de SQL Server en un servidor específico.  
  
-   El objeto **cmd** (**ADODB. Command**) se ejecuta en la conexión establecida.  
  
-   El lenguaje de comandos está establecido en DBGUID_MSSQLXML.  
  
-   El DiffGram se copia en el flujo de comandos (**strmIn**) de un archivo.  
  
-   El flujo de salida del comando se establece en el objeto **StrmOut** (**ADODB. Stream**) para recibir los datos devueltos.  
  
-   Si está utilizando el proveedor SQLOLEDB, obtendrá de forma predeterminada la funcionalidad de Microsoft SQLXML que proporciona Sqlxmlx.dll. Para utilizar Sqlxml4. dll con el proveedor SQLOLEDB, la propiedad **versión de SQLXML** debe establecerse en **SQLXML. 4.0** en el objeto de **conexión** del proveedor SQLOLEDB.  
  
-   Se ejecuta el comando (DiffGram).  
  
 El siguiente código es la aplicación de ejemplo.  
  
> [!NOTE]  
>  En el código, debe suministrarse el nombre de la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en la cadena de conexión.  
  
```  
Private Sub Command1_Click()  
  Dim cmd As New ADODB.Command  
  Dim conn As New ADODB.Connection  
  Dim strmOut As New ADODB.Stream  
  Dim strmIn As New ADODB.Stream  
  
  'Open a connection to SQL Server.  
  conn.Provider = "SQLOLEDB"  
  conn.Open "server=SqlServerName; database=tempdb; Integrated Security=SSPI; "  
  conn.Properties("SQLXML Version") = "SQLXML.4.0"  
  Set cmd.ActiveConnection = conn  
  strmIn.Open  
  strmIn.Charset = "UTF-8"  
  strmIn.LoadFromFile "C:\SomeFilePath\SampleDiffGram.xml"  
  strmIn.Position = 0  
  Set cmd.CommandStream = strmIn  
  
  strmOut.Open  
  cmd.Properties("Output Stream").Value = strmOut  
  cmd.Properties("Output Encoding").Value = "UTF-8"  
  
  cmd.Dialect = "{5d531cb2-e6ed-11d2-b252-00c04f681b71}"  
  cmd.Properties("Mapping Schema") = "C:\SomeFilePath\SampleDiffGram.xml"  
  cmd.Execute , , adExecuteStream  
  strmOut.Position = 0  
  Set cmd = Nothing  
  strmOut.Charset = "UTF-8"  
  strmOut.SaveToFile "C:\DropIt.txt", adSaveCreateOverWrite  
  strmOut.Close  
  Set strmOut = Nothing  
  
End Sub  
```  
  
### <a name="to-test-the-diffgram"></a>Para probar el DiffGram:  
  
1.  En una carpeta del equipo, copie cualquiera de los DiffGrams y el esquema XSD correspondiente de uno de los ejemplos de los [ejemplos de DiffGram](diffgram-examples-sqlxml-4-0.md).  
  
2.  Abra Visual Basic y cree un proyecto EXE estándar.  
  
3.  Agregue estas referencias al proyecto:  
  
    ```  
    Microsoft ActiveX Data Objects 2.8 Library  
    ```  
  
4.  En el cuadro de herramientas, haga clic en **CommandButton**y, a continuación, dibuje un botón en el formulario.  
  
5.  Haga doble clic en el botón para modificar el código y agregue el código de aplicación que se proporciona en el tema.  
  
6.  Modifique el código para especificar el DiffGram y los nombres de archivos XSD. Modifique también la cadena de conexión según corresponda.  
  
7.  Ejecute la aplicación. El resultado de la ejecución depende del DiffGram que esté ejecutando.  
  
  
