---
title: Convertir objetos de base de datos de ASE de Sybase (SybaseToSQL) | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Converting Database Objects
ms.assetid: 509cb65d-2f54-427a-83d7-37919cc4e3e3
caps.latest.revision: 8
author: sabotta
ms.author: carlasab
manager: lonnyb
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: dd8fba1682d270251a865675f047e69a66e12479
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="converting-sybase-ase-database-objects-sybasetosql"></a>Convertir objetos de base de datos de ASE de Sybase (SybaseToSQL)
Después de haber conectado para Sybase Adaptive Server Enterprise (ASE), conectado a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure y el proyecto de conjunto y opciones de asignación de datos, puede convertir objetos de base de datos de Sybase Adaptive Server Enterprise (ASE) a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] u objetos de base de datos de SQL Azure.  
  
## <a name="the-conversion-process"></a>El proceso de conversión  
Convertir objetos de base de datos toma las definiciones de objeto de ASE, se convierte en similar [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure objetos y, a continuación, se carga esta información en los metadatos SSMA. No se carga la información en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure. A continuación, puede ver los objetos y sus propiedades mediante el [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o en el Explorador de metadatos de SQL Azure.  
  
Durante la conversión, SSMA imprime mensajes de salida en el panel de resultados y mensajes de error en el panel de lista de errores. Use la información de salida y el error para determinar si tiene que modificar las bases de datos de ASE o el proceso de conversión para obtener los resultados de la conversión deseada.  
  
## <a name="setting-conversion-options"></a>Establecer las opciones de conversión  
Antes de convertir objetos, revise las opciones de conversión de proyecto en el **configuración del proyecto** cuadro de diálogo. Mediante este cuadro de diálogo, puede establecer cómo SSMA convierte las funciones y variables globales. Para obtener más información, vea [configuración del proyecto &#40; Conversión &#41; &#40; SybaseToSQL &#41; ](../../ssma/sybase/project-settings-conversion-sybasetosql.md).  
  
## <a name="converting-ase-database-objects"></a>Convertir objetos de base de datos de ASE  
Para convertir objetos de base de datos de ASE, primero seleccione los objetos que se va a convertir y, a continuación, tener SSMA para realizar la conversión. Para ver los mensajes de salida durante la conversión, en la **vista** menú, seleccione **salida**.  
  
**Para convertir objetos de ASE a sintaxis de SQL Server o SQL Azure**  
  
1.  En el Explorador de metadatos de Sybase, expanda el servidor ASE y, a continuación, expanda **bases de datos**.  
  
2.  Seleccione los objetos que se va a convertir:  
  
    -   Para convertir todas las bases de datos, active la casilla situada junto a **bases de datos**.  
  
    -   Para convertir u omitir una base de datos, active o desactive la casilla de verificación situada junto al nombre de la base de datos.  
  
    -   Para convertir u omitir esquemas individuales, expanda la base de datos, **esquemas**y, a continuación, active o desactive la casilla situada al lado del esquema.  
  
    -   Para convertir u omitir una categoría de objetos, expanda el esquema y, a continuación, active o desactive la casilla situada junto a la categoría.  
  
    -   Para convertir u omitir los objetos individuales, expanda la carpeta de la categoría y, a continuación, active o desactive la casilla de verificación situada junto al objeto.  
  
3.  Para convertir todos los objetos seleccionados, haga clic en **bases de datos** y seleccione **convertir esquema**.  
  
    También puede convertir los objetos individuales o las categorías de objetos con el botón secundario en el objeto o la carpeta que lo contiene y, a continuación, seleccione **convertir esquema**.  
  
> [!NOTE]  
> Algunas de las funciones de sistema de Sybase coincide exactamente con las funciones del sistema de SQL Server equivalente en el comportamiento. Para emular el comportamiento de Sybase ASE, SSMA genera funciones definidas por el usuario en la base de datos de SQL Server convertida en un esquema denominado 's2ss'. Según la configuración del proyecto, algunas de las funciones de sistema de SQL Server se reemplazan con estas funciones emuladas. SSMA crea las siguientes funciones definidas por el usuario:  
  
||||  
|-|-|-|  
|**char_length_nvarchar**|**index_colorder**|**ssma_datepart**|  
|**char_length_varchar**|**inttohex**|**substring_nvarchar**|  
|**charindex_nvarchar**|**ssma_datediff**|**substring_varbinary**|  
|**charindex_varchar**|**hextoint**|**substring_varchar**|  
|**ulowsurr**|**to_unichar**|**ssma_current_time**|  
|**uhighsurr**|||  
  
## <a name="objects-not-supported-in-sql-azure"></a>Objetos no admitidos en SQL Azure  
Las siguientes palabras clave de T-SQL se utilizan de SSMA para Sybase durante la conversión a SQL Server normal pero estas palabras clave no son compatibles con la sintaxis de T-SQL de SQL Azure:  
  
||||  
|-|-|-|  
|CHECKPOINT|CREATE/ALTER/DROP DEFAULT|CREATE/DROP RULE|  
|DBCC TRACEOFF|DBCC TRACEON|GRANT/REVOKE/DENY ALL|  
|KILL|READTEXT|SELECT INTO|  
|SET OFFSETS|SETUSER|SHUTDOWN|  
|WRITETEXT|||  
  
## <a name="viewing-conversion-problems"></a>Ver los problemas de conversión  
No se pueden convertir algunos objetos ASE. Puede determinar las tasas de éxito de conversión visualizando el informe de resumen de conversión.  
  
**Para ver un informe de resumen**  
  
1.  En el Explorador de metadatos de Sybase, seleccione **bases de datos**.  
  
2.  En el panel derecho, seleccione la **informe** ficha.  
  
    Este informe muestra el informe de resumen de evaluación para todos los objetos de base de datos que se han evaluado o convertir. También puede ver un informe de resumen para objetos individuales:  
  
    -   Para ver el informe de una base de datos individual, seleccione la base de datos en el Explorador de metadatos de Sybase.  
  
    -   Para ver el informe de un objeto de base de datos individual, seleccione el objeto en el Explorador de metadatos de Sybase. Objetos que tienen problemas de conversión tienen un icono rojo de error.  
  
Para los objetos que no se pudo conversión, puede ver la sintaxis que produjo el error de conversión.  
  
**Para ver los problemas de conversión individuales**  
  
1.  En el Explorador de metadatos de Sybase, expanda **bases de datos**.  
  
2.  Expanda la base de datos que muestra un icono rojo de error.  
  
3.  Expanda el **esquemas** carpeta y, a continuación, expanda el esquema que muestra un icono rojo de error.  
  
4.  En el esquema, expanda una carpeta que tenga un icono rojo de error.  
  
5.  Seleccione el objeto que tiene un icono rojo de error.  
  
6.  En el panel derecho, haga clic en el **informe** ficha.  
  
7.  En la parte superior de la **informe** ficha es una lista desplegable. Si la lista muestra **estadísticas**, cambie la selección a **origen**.  
  
    SSMA mostrará el código fuente y varios botones inmediatamente encima del código.  
  
8.  Haga clic en el **problema siguiente** botón. Se trata de un icono de error rojo con una flecha que señala a la derecha.  
  
    SSMA para ASE resaltará el primer código de origen problemático que encuentra en el objeto actual.  
  
Para cada elemento que no se pudo convertir, deberá determinar qué desea hacer con ese objeto:  
  
-   Puede editar el código fuente para procedimientos y desencadenadores en el **SQL** ficha.  
  
-   Puede modificar el objeto de ASE para quitar o revisar el código problemático. Para cargar el código actualizado en SSMA, tendrá que actualizar los metadatos. Para obtener más información, vea [conectarse para Sybase ASE &#40; SybaseToSQL &#41; ](../../ssma/sybase/connecting-to-sybase-ase-sybasetosql.md).  
  
-   Puede excluir el objeto de la migración. En [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o el Explorador de metadatos de SQL Azure y el Explorador de metadatos de Sybase, desactive la casilla de verificación situada junto al elemento antes de cargar los objetos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure y migrar datos de ASE.  
  
## <a name="next-step"></a>Paso siguiente  
El siguiente paso del proceso de migración consiste en [cargar objetos de base de datos para convertir a SQL Server o SQL Azure (SybaseToSQL)](http://msdn.microsoft.com/en-us/4c59256f-99a8-4351-9559-a455813dbd06).  
  
## <a name="see-also"></a>Vea también  
[Migrar bases de datos de ASE de Sybase a SQL Server: base de datos de SQL Azure &#40; SybaseToSQL &#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  

