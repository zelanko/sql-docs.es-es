---
title: "Asignación de tipo de datos en el Asistente de exportación y la importación de SQL Server | Documentos de Microsoft"
ms.custom: 
ms.date: 01/11/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 669be403-cb17-4b12-bbbf-e7a74003c4b6
caps.latest.revision: 2
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 4eca10e506087ee5d8106cb05c861c4efa49a65d
ms.contentlocale: es-es
ms.lasthandoff: 09/26/2017

---
# <a name="data-type-mapping-in-the-sql-server-import-and-export-wizard"></a>Asignación de tipos de datos en el Asistente para importación y exportación de SQL Server
 En el Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , puede establecer el nombre, el tipo de datos y las propiedades de tipo de datos de las columnas de las tablas y archivos de destino nuevos, pero no puede especificar conversiones personalizadas para los valores de columna. Como resultado, la asignación integrada de tipos de datos del origen al destino es muy importante.  
  
##  <a name="wizardMapping"></a> ¿Cómo asigna el asistente tipos de datos entre el origen y el destino?
El asistente usa archivos de asignación que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] instala para asignar tipos de datos de un sistema o versión de base de datos a otro. Por ejemplo, puede asignar de tipos de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a tipos de datos de Oracle. De forma predeterminada, los archivos de asignación en formato XML se instalan en las siguientes carpetas.
-   **C:\Program Files\Microsoft SQL Server\130\DTSMappingFiles\**  (para 64 bits)
-   **C:\Program archivos (x86) \Microsoft SQL Server\130\DTSMappingFiles\**  (para 32 bits).  
  
 Si modifica un archivo de asignación existente o agrega un nuevo archivo de asignación a la carpeta, debe cerrar y volver a abrir el Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] para cargar el archivo de asignación nuevo o modificado.  
 
## <a name="you-can-change-an-existing-mapping-file"></a>Puede cambiar un archivo de asignación existente
Si su empresa requiere diferentes asignaciones entre tipos de datos, puede actualizar los archivos de asignación para cambiar las asignaciones que usa el asistente. Por ejemplo, si quiere que el tipo de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **de** se asigne al tipo de datos **GRAPHIC** de DB2 en lugar de al tipo de datos **VARGRAPHIC** de DB2 al transferir datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a DB2, puede cambiar la asignación de **de** en el archivo de asignación **SqlClientToIBMDB2.xml** para que se use **GRAPHIC** en lugar de **VARGRAPHIC**de  
  
## <a name="you-can-add-a-new-mapping-file"></a>Puede agregar un archivo de asignación nuevo
[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] instala asignaciones entre numerosas combinaciones de origen y de destino de uso frecuente. También puede agregar nuevos archivos de asignación en el directorio **MappingFiles** para admitir orígenes y destinos adicionales. Los nuevos archivos de asignación deben ajustarse al esquema XSD publicado y asignar entre una combinación única de origen y destino. El esquema de los archivos de asignación, **DataTypeMapping.xsd**, está publicado [aquí](http://schemas.microsoft.com/sqlserver/2008/07/IntegrationServices/DataTypeMapping/DataTypeMapping.xsd).
 
## <a name="sample-mapping-file"></a>Archivo de asignación de ejemplo
A continuación se muestra una parte del archivo de asignación XML que asigna desde tipos de datos de SQL Server (o, más concretamente, de tipos de datos usados por el proveedor de datos de .NET Framework para SQL Server) a tipos de datos de Oracle. Por ejemplo, puede ver que un tipo de datos **int** de SQL Server se asigna a un tipo de datos **INTEGER** de Oracle.
  
```xml  
  
<dtm:DataTypeMappings  
    xmlns:dtm="http://www.microsoft.com/SqlServer/Dts/DataTypeMapping.xsd"   
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"  
    SourceType="System.Data.SqlClient.SqlConnection"   
    MinSourceVersion="*"   
    MaxSourceVersion="*"   
    DestinationType="MSDAORA;OraOLEDB.Oracle;System.Data.OracleClient.OracleConnection"   
    MinDestinationVersion="08.*"   
    MaxDestinationVersion="*">  
  
    <!-- smallint -->  
    <dtm:DataTypeMapping >  
        <dtm:SourceDataType>  
            <dtm:DataTypeName>smallint</dtm:DataTypeName>  
        </dtm:SourceDataType>  
        <dtm:DestinationDataType>  
            <dtm:SimpleType>  
                <dtm:DataTypeName>INTEGER</dtm:DataTypeName>  
            </dtm:SimpleType>  
        </dtm:DestinationDataType>  
    </dtm:DataTypeMapping>    
  
    <!-- int -->  
    <dtm:DataTypeMapping >  
        <dtm:SourceDataType>  
            <dtm:DataTypeName>int</dtm:DataTypeName>  
        </dtm:SourceDataType>  
        <dtm:DestinationDataType>  
            <dtm:SimpleType>  
                <dtm:DataTypeName>INTEGER</dtm:DataTypeName>  
            </dtm:SimpleType>  
        </dtm:DestinationDataType>  
    </dtm:DataTypeMapping>    
  
        ...  
  
</dtm:DataTypeMappings>  
  
```  


