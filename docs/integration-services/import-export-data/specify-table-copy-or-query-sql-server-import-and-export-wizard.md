---
title: Especificar copia de tabla o consulta (Asistente para importación y exportación de SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 02/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.impexpwizard.specifytablecopyorquery.f1
ms.assetid: 08aa7158-40e6-4ef3-84d3-1265a8ba194c
author: janinezhang
ms.author: janinez
ms.openlocfilehash: d25caed1ed159ff3cbb63851eb0f9a22487511b1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68025180"
---
# <a name="specify-table-copy-or-query-sql-server-import-and-export-wizard"></a>Especificar copia de tabla o consulta (Asistente para importación y exportación de SQL Server)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Después de proporcionar información sobre el destino de los datos y sobre cómo se conectará a estos, en el Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se mostrará **Especificar copia de tabla o consulta**. En esta página, elija una de las opciones siguientes.
-   **Copiar los datos de una o varias tablas o vistas**. Puede seleccionar una o varias tablas de una lista.
-   **Escribir una consulta para especificar los datos que se van a transferir**. Puede escribir o pegar el texto de una consulta SQL.
    
> [!TIP]
> Si tiene que copiar más de una base de datos, o bien objetos de base de datos que no sean tablas y vistas, use el Asistente para copiar bases de datos en lugar del Asistente para importación y exportación. Para más información, vea [Usar el Asistente para copiar bases de datos](../../relational-databases/databases/use-the-copy-database-wizard.md).     
 
## <a name="screen-shot-of-the-specify-table-copy-or-query-page"></a>Captura de pantalla de la página Especificar copia de tabla o consulta    
 En la captura de pantalla siguiente se muestra la página **Especificar copia de tabla o consulta** del asistente.    
    
 ![Página Especificar copia de tabla o consulta del Asistente para importación y exportación](../../integration-services/import-export-data/media/table-copy-or-query.png "Página Especificar copia de tabla o consulta del Asistente para importación y exportación")    
    
## <a name="specify-whether-to-copy-an-entire-table-or-write-a-query"></a>Especifique si quiere copiar una tabla completa o escribir una consulta 
 **Copiar los datos de una o varias tablas o vistas**    
 Seleccione esta opción si quiere copiar los datos del origen sin tener que filtrar ni ordenar registros.   

Al seleccionar **Copiar los datos de una o varias tablas o vistas**, puede copiar desde una tabla o vista a una tabla de destino, o bien desde varias tablas o vistas a varias tablas de destino.

 Después de hacer clic en **Siguiente**, seleccione las tablas que quiera copiar en la página **Seleccionar tablas y vistas de origen** . Para más información, vea [Seleccionar tablas y vistas de origen](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md).   
    
 **Escribir una consulta para especificar los datos que se van a transferir**    
 Seleccione esta opción si quiere filtrar u ordenar los datos de origen antes de copiarlos en el destino.    
    
Al seleccionar **Escribir una consulta para especificar los datos que se van a transferir**, solo se pueden copiar los resultados a una tabla de destino.  

Después de hacer clic en **Siguiente**, escriba una instrucción SQL para especificar columnas y seleccionar filas en el cuadro de diálogo **Proporcionar una consulta de origen** . Para más información, vea [Proporcionar una consulta de origen](../../integration-services/import-export-data/provide-a-source-query-sql-server-import-and-export-wizard.md).   
    
## <a name="why-isnt-the-copy-option-available"></a>¿Por qué no está disponible la opción Copiar?    
 Es posible que la opción **Copiar los datos de una o varias tablas o vistas** no esté disponible si el asistente usa un proveedor de datos de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] para conectarse al origen de datos. Esto ocurre cuando el asistente no tiene información suficiente sobre el proveedor de datos para pedir una lista de tablas y vistas desde el origen de datos. 
 
Puede seguir usando la opción **Write a query (Escribir una consulta)** , aunque normalmente no escriba consultas SQL, siempre y cuando conozca el nombre de la tabla que quiere exportar. En el cuadro de diálogo **Proporcionar una consulta de origen**, que se muestra después de hacer clic en **Siguiente**, escriba la consulta como `SELECT * FROM <name of table>`. Si el nombre de la tabla contiene espacios u otros caracteres especiales, escriba el nombre entre corchetes (`SELECT * FROM [<name of table>]`).

### <a name="more-info"></a>Más información
 La opción **Copiar los datos de una o varias tablas o vistas** solo está disponible para los proveedores que tienen la sección ProviderDescription en el archivo ProviderDescriptors.xml. (De forma predeterminada, este archivo se encuentra en \<*unidad*>:\Archivos de programa\Microsoft SQL Server\130\DTS\ProviderDescriptors). Cada sección ProviderDescription del archivo contiene la información que necesita para recuperar los metadatos del proveedor correspondiente.    
    
 De forma predeterminada, el archivo ProviderDescriptors.xml contiene la sección ProviderDescription solo para los proveedores siguientes.    
    
-   Proveedor de datos .NET Framework para ODBC SQL Server (System.Data.SqlClient)    
    
-   Proveedor de datos .NET Framework para Oracle (System.Data.OracleClient)    
    
-   Proveedor de datos .NET Framework para ODBC (System.Data.Odbc)    
    
-    System.Data.OleDb (válido para todos los proveedores OLE DB)    
    
-   Proveedor de Microsoft para DB2 instalado por Microsoft Host Integration Server (Microsoft.HostIntegration.MsDb2Client.MsDb2Connection)    
    
 Los desarrolladores independientes pueden permitir que esté disponible la opción **Copiar los datos de una o varias tablas o vistas** para su proveedor si agregan la sección ProviderDescriptor al archivo ProviderDescriptors.xml. Para revisar los requisitos de la sección ProviderDescriptor, vea el archivo de esquema ProviderDescriptors.xsd que, de forma predeterminada, está en la misma carpeta que el archivo ProviderDescriptors.xml.    
    
## <a name="whats-next"></a>¿Qué sigue?    
 Después de especificar si quiere copiar toda una tabla o proporcionar una consulta, la página siguiente depende de la opción que haya elegido en esta página, así como del destino de los datos.    
    
-   Si ha seleccionado **Copiar los datos de una o varias tablas o vistas**, para la mayoría de los destinos, la página siguiente será **Seleccionar tablas y vistas de origen**. En esta página, seleccione las tablas y vistas existentes que quiere copiar del origen de datos al destino. Para más información, vea [Seleccionar tablas y vistas de origen](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md).    
    
-   Si ha seleccionado **Copiar los datos de una o varias tablas o vistas** y el destino es un archivo plano, la página siguiente será **Configurar el destino del archivo plano**. En esta página, especifique las opciones de formato del archivo plano de destino. (Después de configurar el archivo plano, la página siguiente será **Seleccionar tablas y vistas de origen**). Para más información, vea [Configurar el destino del archivo plano](../../integration-services/import-export-data/configure-flat-file-destination-sql-server-import-and-export-wizard.md).    
    
-   Si ha seleccionado **Escribir una consulta para especificar los datos que se van a transferir**, la página siguiente será **Proporcionar una consulta de origen**. En esta página, escriba y pruebe la instrucción SQL que selecciona los datos que se van a copiar del origen de datos al destino. (Después de especificar una consulta, la página siguiente será **Seleccionar tablas y vistas de origen**). Para más información, vea [Proporcionar una consulta de origen](../../integration-services/import-export-data/provide-a-source-query-sql-server-import-and-export-wizard.md).

## <a name="see-also"></a>Vea también
[Comenzar con este sencillo ejemplo del Asistente para importar y exportar](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)


