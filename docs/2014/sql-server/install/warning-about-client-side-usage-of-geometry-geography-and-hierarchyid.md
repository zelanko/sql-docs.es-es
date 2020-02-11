---
title: Advertencia sobre el uso del lado cliente de GEOMETRY, Geography y HIERARCHYID | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 500ee6b3-2154-45d2-a3cf-8760166d9413
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 524400e9c9420fb54447220215d4660874ec6d69
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66091088"
---
# <a name="warning-about-client-side-usage-of-geometry-geography-and-hierarchyid"></a>Advertencia sobre el uso del lado cliente de GEOMETRY, GEOGRAPHY y HIERARCHYID
  El ensamblado **Microsoft. SqlServer. types. dll**, que contiene los tipos de datos espaciales, se ha actualizado de la versión 10,0 a la versión 11,0. Cuando se cumplan determinadas condiciones, se puede producir un error en las aplicaciones personalizadas que hacen referencia a este ensamblado.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descripción  
 El ensamblado **Microsoft. SqlServer. types. dll**, que contiene los tipos de datos espaciales, se ha actualizado de la versión 10,0 a la versión 11,0. Cuando se cumplan las siguientes condiciones, se puede producir un error en las aplicaciones personalizadas que hacen referencia a este ensamblado.  
  
-   Cuando se mueve una aplicación personalizada desde un equipo en el [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] que se instaló en un equipo en el [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] que solo está instalado, se producirá un error en la aplicación porque la versión 10,0 a la que se hace referencia del ensamblado **SqlTypes** no está presente. Puede aparecer este mensaje de error: `"Could not load file or assembly 'Microsoft.SqlServer.Types, Version=10.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91' or one of its dependencies. The system cannot find the file specified."`  
  
-   Cuando se hace referencia a la versión 11,0 del ensamblado **SqlTypes** y también se instala la versión 10,0, puede aparecer este mensaje de error:`"System.InvalidCastException: Unable to cast object of type 'Microsoft.SqlServer.Types.SqlGeometry' to type 'Microsoft.SqlServer.Types.SqlGeometry'."`  
  
-   Cuando se hace referencia a la versión 11,0 del ensamblado **SqlTypes** desde una aplicación personalizada que tiene como destino .net 3,5, 4 o 4,5, se producirá un error en la aplicación porque SqlClient by Design carga la versión 10,0 del ensamblado. Este error se produce cuando la aplicación llama a uno de los siguientes métodos:  
  
    -   método `GetValue` de la clase `SqlDataReader`  
  
    -   método `GetValues` de la clase `SqlDataReader`  
  
    -   operador de índice de corchete [] de la clase `SqlDataReader`  
  
    -   método `ExecuteScalar` de la clase `SqlCommand`  
  
## <a name="corrective-action"></a>Acción correctora  
 Puede solucionar este problema si usa uno de los métodos siguientes:  
  
-   Puede solucionar este problema en el código si llama al método `GetSqlBytes`, en lugar de los métodos Get enumerados anteriormente, para recuperar los tipos de sistema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de CLR, tal como se muestra en el siguiente ejemplo:  
  
    ```csharp  
    string query = "SELECT [SpatialColumn] FROM [SpatialTable]";  
          using (SqlConnection conn = new SqlConnection("..."))  
          {  
                SqlCommand cmd = new SqlCommand(query, conn);  
  
                conn.Open();  
                SqlDataReader reader = cmd.ExecuteReader();  
  
                while (reader.Read())  
                {  
                      // In version 11.0 only  
                      SqlGeometry g =   
    SqlGeometry.Deserialize(reader.GetSqlBytes(0));  
  
                      // In version 10.0 or 11.0  
                      SqlGeometry g2 = new SqlGeometry();  
                      g.Read(new BinaryReader(reader.GetSqlBytes(0).Stream));  
                }  
          }  
    ```  
  
-   Puede solucionar este problema mediante el redireccionamiento de ensamblado en el archivo de configuración de la aplicación, tal como se muestra en el siguiente ejemplo:  
  
    ```xml  
    <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">  
        ...  
        <dependentAssembly>  
            <assemblyIdentity name="Microsoft.SqlServer.Types" publicKeyToken="89845dcd8080cc91" culture="neutral" />  
            <bindingRedirect oldVersion="10.0.0.0" newVersion="11.0.0.0" />  
        </dependentAssembly>  
        ...  
    </assemblyBinding>  
    ```  
  
-   Puede solucionar esta problema en la cadena de conexión si especifica el valor "SQL Server 2012" para el atributo "Type System Version" para forzar que SqlClient cargue la versión 11.0 del ensamblado. Este atributo de cadena de conexión solo está disponible en .NET 4.5 y posterior.  
  
## <a name="see-also"></a>Consulte también  
 [Problemas de actualización Motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server el asesor de actualizaciones de 2014 &#91;nuevo&#93;](sql-server-2014-upgrade-advisor.md
)  
  
  
