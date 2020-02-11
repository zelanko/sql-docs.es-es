---
title: Utilizar ADO para ejecutar consultas SQLXML 4.0
ms.custom: ''
ms.date: 12/15/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- query testers [SQLXML]
- test scripts
- ADO [SQLXML]
- queries [SQLXML], ADO
- SQLXML, ADO
ms.assetid: 3d54e3bb-7c5f-427e-82f8-1403a54c4f53
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 436ec564e4cf5de21647eb5cd667741ce246e99d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "75254139"
---
# <a name="using-ado-to-execute-sqlxml-40-queries"></a>Utilizar ADO para ejecutar consultas SQLXML 4.0
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  En versiones anteriores de SQLXML, la ejecución de consultas basadas en HTTP se admitía mediante la utilización de directorios virtuales de SQLXML IIS y el filtro SQLXML ISAPI. En SQLXML 4.0, estos componentes se han quitado ya que se ofrece una funcionalidad similar superpuesta a través de servicios web XML nativos a partir de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
 Como alternativa, puede ejecutar consultas y utilizar SQLXML 4.0 con las aplicaciones basadas en COM si aprovecha las extensiones SQLXML a Objetos de datos ActiveX (ADO) que se introdujeron por primera vez en Microsoft Data Access Components (MDAC) 2.6 y versiones posteriores.  
  
 En este tema se muestra cómo usar SQLXML y ADO como parte de una aplicación Visual Basic Scripting Edition (VBScript) (un script con la extensión de nombre de archivo. vbs). También se proporcionan los procedimientos de configuración iniciales que le ayudarán a volver a crear y probar ejemplos de consulta de la documentación de SQLXML 4.0.  
  
## <a name="creating-the-sqlxml-40-test-script"></a>Crear el script de prueba de SQLXML 4.0  
 En este procedimiento, crea un archivo VBScript (.vbs), Sqlxml4test.vbs, que se puede utilizar para ejecutar consultas SQLXML aprovechando las extensiones ADO de SQLXML en ADO 2.6 y versiones posteriores.  
  
#### <a name="to-create-the-sqlxml-40-query-tester-using-ado-vbscript"></a>Para crear el evaluador de consultas de SQLXML 4.0 mediante ADO (VBScript).  
  
1.  Copie el código siguiente y péguelo en un archivo de texto. Guarde el archivo como Sqlxml4test.vbs.  
  
    ```  
    WScript.Echo "Query process may take a few seconds to complete. Please be patient."  
  
    ' Note that for SQL Server Native Client to be used as the data provider,  
    ' it needs to be installed on the client computer first. Also, SQLXML extensions   
    ' for ADO are used and available in MDAC 2.6 or later.  
  
    'Set script variables.  
    inputFile = "@@FILE_NAME@@"  
    strServer = "@@SERVER_NAME@@"  
    strDatabase = "@@DATABASE_NAME@@"  
    dbGuid = "{5d531cb2-e6ed-11d2-b252-00c04f681b71}"  
  
    ' Establish ADO connection to SQL Server and   
    ' create an instance of the ADO Command object.  
    Set conn = CreateObject("ADODB.Connection")  
    Set cmd = CreateObject("ADODB.Command")  
    conn.Open "Provider=SQLXMLOLEDB.4.0;Data Provider=SQLNCLI11;Server=" & strServer & _  
              ";Database=" & strDatabase & ";Integrated Security=SSPI"  
    Set cmd.ActiveConnection = conn  
  
    ' Create the input stream as an instance of the ADO Stream object.  
    Set inStream = CreateObject("ADODB.Stream")  
    inStream.Open  
    inStream.Charset = "utf-8"  
    inStream.LoadFromFile inputFile  
  
    ' Set ADO Command instance to use input stream.  
    Set cmd.CommandStream = inStream  
  
    ' Set the command dialect.  
    cmd.Dialect = dbGuid  
  
    ' Set a second ADO Stream instance for use as a results stream.   
    Set outStream = CreateObject("ADODB.Stream")  
    outStream.Open  
  
    ' Set dynamic properties used by the SQLXML ADO command instance.   
    cmd.Properties("XML Root").Value = "ROOT"  
    cmd.Properties("Output Encoding").Value = "UTF-8"  
  
    ' Connect the results stream to the command instance and execute the command.  
    cmd.Properties("Output Stream").Value = outStream  
    cmd.Execute , , 1024  
  
    ' Echo cropped/partial results to console.  
    WScript.Echo Left(outStream.ReadText, 1023)  
  
    inStream.Close  
    outStream.Close  
    ```  
  
2.  Actualice los siguientes valores de script para obtener el ejemplo que está intentando probar y su entorno de pruebas.  
  
    -   Busque "`@@FILE_NAME@@`" y reemplácelo con el nombre del archivo de plantilla.  
  
    -   Busque "`@@SERVER_NAME@@`" y reemplácelo con el nombre de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (por ejemplo, "`(local)`" si [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se ejecuta localmente).  
  
    -   Busque "`@@DATABASE_NAME@@`" y reemplácelo con el nombre de la base de datos (por ejemplo, "`AdventureWorks2012`" o "`tempdb`").  
  
     Actualice cualquier otro valor si se menciona en las instrucciones concretas del ejemplo que intenta volver a crear localmente en el equipo.  
  
3.  Guarde el archivo y ciérrelo.  
  
4.  Compruebe que ha creado los archivos adicionales, como esquemas o plantillas XML que forman parte del ejemplo que intenta volver a crear localmente en el equipo. Estos archivos deben estar incluidos en el mismo directorio donde se ha guardado el archivo de script de prueba (Sqlxml4test.vbs).  
  
5.  Siga las instrucciones de la sección siguiente sobre cómo utilizar el script de prueba de SQLXML 4.0.  

## <a name="using-the-sqlxml-40-test-script"></a>Utilizar el script de prueba de SQLXML 4.0  
 El procedimiento siguiente describe cómo utilizar los archivos Sqlxml4test.vbs probar las consultas de ejemplo incluidas en esta documentación.  
  
#### <a name="to-use-the-sqlxml-40-query-tester"></a>Para utilizar el evaluador de consultas de SQLXML 4.0  
  
1.  Compruebe tal como se indica a continuación que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client está instalado:  
  
    1.  En el menú **Inicio** , seleccione **configuración**y, a continuación, haga clic en **Panel de control**.  
  
    2.  En el panel de control, Abra **Agregar o quitar programas** .  
  
    3.  En la lista de programas instalados actualmente, compruebe que **Microsoft SQL Server Native Client** aparece en la lista.  
  
        > [!NOTE]  
        >  Si necesita instalar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, consulte instalación de [SQL Server Native Client](../../relational-databases/native-client/applications/installing-sql-server-native-client.md).  
  
2.  Compruebe que la versión de MDAC instalada en el equipo cliente es la versión 2.6 o posterior. Si necesita comprobar la información de la versión de MDAC, puede usar la herramienta Comprobador de componentes de MDAC, que se proporciona como descarga gratuita en [http://www.microsoft.com](https://www.microsoft.com)el sitio web de Microsoft,. Para obtener más información, busque "MDAC Component Checker" en el sitio web de Microsoft.  
  
3.  Ejecute el script.  
  
     Puede ejecutar el archivo VBScript en la línea de comandos utilizando Cscript.exe o haciendo doble clic en el archivo Sqlxml4test.vbs para invocar Windows Script Host (WScript.exe).  
  
     Al ejecutarlo, el script debe mostrar un mensaje para advertir que puede tardar unos momentos en ejecutarse antes de devolver y mostrar los resultados de consulta como salida del script. Cuando aparezca el resultado, compare su contenido con los resultados esperados del ejemplo.  
  
  
