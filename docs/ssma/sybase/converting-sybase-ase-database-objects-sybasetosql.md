---
title: Convertir objetos de base de datos ASE Sybase (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/01/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Converting Database Objects
ms.assetid: 509cb65d-2f54-427a-83d7-37919cc4e3e3
caps.latest.revision: 8
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 86adf372dfd590f0cac1d8ac872501fb12ab1e7b
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/12/2018
ms.locfileid: "38980667"
---
# <a name="converting-sap-ase-database-objects-sybasetosql"></a>Convertir objetos de base de datos de SAP ASE (SybaseToSQL)
Después de haberse conectado a SAP Adaptive Server Enterprise (ASE), conectado a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure y establecer el proyecto y las opciones de asignación de datos, puede convertir los objetos de base de datos de SAP Adaptive Server Enterprise (ASE) para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o base de datos SQL de Azure objetos.  
  
## <a name="the-conversion-process"></a>El proceso de conversión  
Convertir objetos de base de datos toma las definiciones de objeto de ASE, los convierte similar [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure los objetos y, a continuación, se carga esta información en los metadatos SSMA. No se carga la información en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure. A continuación, puede ver los objetos y sus propiedades mediante el [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o el Explorador de metadatos de SQL Azure.
  
Durante la conversión, SSMA imprime mensajes de salida para los mensajes de error y el panel de salida para el **lista de errores** panel. Use la información de salida y error para determinar si tiene que modificar las bases de datos de ASE o el proceso de conversión para obtener los resultados de la conversión deseada.  
  
## <a name="setting-conversion-options"></a>Establecer las opciones de conversión  
Antes de convertir los objetos, revise las opciones de conversión de proyecto en el **configuración del proyecto** cuadro de diálogo. Mediante este cuadro de diálogo, puede establecer cómo SSMA convierte las funciones y variables globales. Para obtener más información, consulte [configuración del proyecto &#40;conversión&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-conversion-sybasetosql.md).  
  
## <a name="converting-ase-database-objects"></a>Convertir objetos de base de datos de ASE  
Para convertir objetos de base de datos de ASE, primero seleccione los objetos que desea convertir y, a continuación, SSMA realizar la conversión. Para ver los mensajes de salida durante la conversión, en el **vista** menú, seleccione **salida**.  
  
**Para convertir objetos de ASE a sintaxis de SQL Server o SQL Azure**  
  
1.  En el Explorador de metadatos de Sybase, expanda el servidor de ASE y, a continuación, expanda **bases de datos**.  
  
2.  Seleccione los objetos que desea convertir:  
  
    -   Para convertir todas las bases de datos, seleccione la casilla de verificación junto a **bases de datos**.  
  
    -   Para convertir u omitir una base de datos, active o desactive la casilla de verificación situada junto al nombre de la base de datos.  
  
    -   Para convertir u omitir esquemas individuales, expanda la base de datos, **esquemas**y, a continuación, active o desactive la casilla de verificación al lado del esquema.  
  
    -   Para convertir u omitir una categoría de objetos, expanda el esquema y, a continuación, active o desactive la casilla de verificación junto a la categoría.  
  
    -   Para convertir u omitir los objetos individuales, expanda la carpeta de categoría y, a continuación, active o desactive la casilla de verificación situada junto al objeto.  
  
3.  Para convertir todos los objetos seleccionados, haga clic en **bases de datos**y, a continuación, seleccione **convertir esquema**.  
  
    También puede convertir los objetos individuales o categorías de objetos haciendo clic en el objeto o su carpeta contenedora y, a continuación, seleccione **convertir esquema**.  
  
> [!NOTE]  
> Algunas de las funciones de sistema de SAP ASE no coinciden exactamente con las funciones del sistema de SQL Server equivalente en comportamiento. Para emular el comportamiento de SAP ASE, SSMA genera funciones definidas por el usuario en la base de datos de SQL Server convertido en un esquema denominado 's2ss'. Según la configuración del proyecto, algunas de las funciones de sistema de SQL Server se reemplazan con estas funciones emuladas. SSMA crea las siguientes funciones definidas por el usuario:  
  
||||  
|-|-|-|  
|**char_length_nvarchar**|**index_colorder**|**ssma_datepart**|  
|**char_length_varchar**|**inttohex**|**substring_nvarchar**|  
|**charindex_nvarchar**|**ssma_datediff**|**substring_varbinary**|  
|**charindex_varchar**|**hextoint**|**substring_varchar**|  
|**ulowsurr**|**to_unichar**|**ssma_current_time**|  
|**uhighsurr**|||  
  
## <a name="objects-not-supported-in-azure-sql"></a>Objetos no admitidos en SQL Azure  
Las siguientes palabras clave de Transact-SQL se utilizan SSMA para SAP ASE durante la conversión a SQL Server local, pero estas palabras clave no son compatibles con la sintaxis de T-SQL de SQL Azure:  
  
||||  
|-|-|-|  
|CHECKPOINT|CREATE/ALTER/DROP DEFAULT|CREATE/DROP RULE|  
|DBCC TRACEOFF|DBCC TRACEON|GRANT/REVOKE/DENY ALL|  
|KILL|READTEXT|SELECT INTO|  
|SET OFFSETS|SETUSER|SHUTDOWN|  
|WRITETEXT|||  
  
## <a name="viewing-conversion-problems"></a>Ver los problemas de conversión  
No se pueden convertir algunos objetos de SAP ASE. Puede determinar las tasas de éxito de conversión viendo el informe de resumen de conversión.  
  
**Para ver un informe de resumen**  
  
1.  En el Explorador de metadatos de Sybase, seleccione **bases de datos**.  
  
2.  En el panel derecho, seleccione el **informe** ficha.  
  
    Este informe muestra el informe de resumen de evaluación para todos los objetos de base de datos que se han evaluado o convertir. También puede ver un informe de resumen de los objetos individuales:  
  
    -   Para ver el informe para una base de datos, seleccione la base de datos en el Explorador de metadatos de Sybase.  
  
    -   Para ver el informe para un objeto de base de datos individual, seleccione el objeto en el Explorador de metadatos de Sybase. Los objetos que tienen problemas de conversión tienen un icono rojo de error.  
  
Para los objetos que no se pudo conversión, puede ver la sintaxis que produjo el error de conversión.  
  
**Para ver los problemas de conversión individuales**  
  
1.  En el Explorador de metadatos de Sybase, expanda **bases de datos**.  
  
2.  Expanda la base de datos que se muestra un icono rojo de error.  
  
3.  Expanda el **esquemas** carpeta y, a continuación, expanda el esquema que se muestra un icono rojo de error.  
  
4.  En el esquema, expanda una carpeta que tiene un icono rojo de error.  
  
5.  Seleccione el objeto que tiene un icono rojo de error.  
  
6.  En el panel derecho, seleccione el **informe** ficha.  
  
7.  En la parte superior de la **informe** ficha es una lista desplegable. Si la lista muestra **estadísticas**, cambie la selección a **origen**.  
  
    SSMA mostrará el código fuente y varios botones inmediatamente encima del código.  
  
8.  Seleccione **siguiente problema**, un icono de error rojo con una flecha que apunta a la derecha.  
  
    SSMA para SAP ASE, resaltará el primer código problemático de origen que encuentra en el objeto actual.  
  
Para cada elemento que no se pudo convertir, tendrá que determinar qué desea hacer con ese objeto:  
  
-   Puede editar el código fuente para procedimientos y desencadenadores en el **SQL** ficha.  
  
-   Puede modificar el objeto de SAP ASE para quitar o revisar el código problemático. Para cargar el código actualizado en SSMA, tendrá que actualizar los metadatos. Para obtener más información, consulte [conectarse a SAP ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sybase-ase-sybasetosql.md).  
  
-   El objeto se puede excluir de la migración. En [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o explorador de metadatos de SQL Azure y el Explorador de metadatos de Sybase, desactive la casilla de verificación situada junto al elemento antes de cargar los objetos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure y migrar datos de SAP ASE.  
  
## <a name="next-steps"></a>Pasos siguientes  
El siguiente paso del proceso de migración es [cargar objetos de base de datos para convertir a SQL Server o SQL Azure (SybaseToSQL)](http://msdn.microsoft.com/4c59256f-99a8-4351-9559-a455813dbd06).  
  
## <a name="see-also"></a>Vea también  
[Migrar bases de datos de ASE de SAP a SQL Server: base de datos SQL Azure &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
