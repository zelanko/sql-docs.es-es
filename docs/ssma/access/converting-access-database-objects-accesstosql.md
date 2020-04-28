---
title: Conversión de objetos de base de datos de Access (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Access databases
- Access databases, converting schemas
- conversion
- conversion, converting schemas
- indexes, altering
- metadata
- metadata, altering
- metadata, converting
- migrating databases, one-click
- one-click migration
- schemas
- schemas, converting
- SQL
- SQL, converting
- syntax
- syntax, converting
- tables, altering
- translating Access to SQL Azure
- translating Access to SQL Server
ms.assetid: e0ef67bf-80a6-4e6c-a82d-5d46e0623c6c
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 56c55dbc5df61bfdb9013e505335af16fccbeecd
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "68006631"
---
# <a name="converting-access-database-objects-accesstosql"></a>Convertir objetos de base de datos de Access (AccessToSQL)
Una vez agregadas las bases de datos de Access y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conectado a o SQL Azure, SSMA muestra los metadatos para el acceso y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] los objetos de base de datos de SQL Azure. Ahora puede seleccionar objetos de base de datos de Access y, a continuación, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] convertir los esquemas en o SQL Azure esquemas.  
  
## <a name="the-conversion-process"></a>Proceso de conversión  
La conversión de objetos de base de datos toma las definiciones de objeto de los metadatos [!INCLUDE[tsql](../../includes/tsql-md.md)] de acceso, las convierte en una sintaxis equivalente y, a continuación, carga esta información en el proyecto. A continuación, puede ver [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] los objetos o SQL Azure y sus propiedades mediante [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure el explorador de metadatos.  
  
> [!IMPORTANT]  
> La conversión de objetos no crea los objetos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en ni SQL Azure. Solo convierte las definiciones de objeto y almacena la información en el proyecto SSMA.  
  
Durante la conversión, SSMA imprime el estado en el panel de salida, así como los mensajes de error, de advertencia e informativos en el panel Lista de errores. Use esta información para determinar si es necesario modificar las bases de datos de Access o el proceso de conversión para obtener los resultados de la conversión deseada. También puede usar la información del tema [preparación de bases de datos de Access para la migración](preparing-access-databases-for-migration-accesstosql.md) para determinar lo que se convertirá y no.  
  
## <a name="setting-conversion-options"></a>Establecer opciones de conversión  
Antes de convertir objetos, revise las opciones de conversión de proyectos en el cuadro de diálogo **configuración del proyecto** . Mediante este cuadro de diálogo, puede establecer cómo SSMA convierte las columnas de memorando indizadas, las claves principales, las restricciones de clave externa, las marcas de tiempo y las tablas sin índices. Para obtener más información, vea [configuración del proyecto (conversión)](https://msdn.microsoft.com/bcebc635-c638-4ddb-924c-b9ccfef86388) .  
  
## <a name="conversion-results"></a>Resultados de la conversión  
En la tabla siguiente se muestra qué objetos de acceso se convierten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y los objetos SQL Azure o resultantes:  
  
|Objeto de acceso|Objeto SQL Server resultante|  
|-----------------|-------------------------------|  
|table|table|  
|columna|columna|  
|índice|índice|  
|clave externa|clave externa|  
|Query|ver<br /><br />La mayoría de las consultas SELECT se convierten en vistas. Otras consultas, como las consultas de actualización, no se migran.<br /><br />No se convierten las consultas SELECT que toman parámetros y las consultas entre tabulaciones.|  
|informe|no convertido|  
|form|no convertido|  
|macro|no convertido|  
|module|no convertido|  
|valor predeterminado|valor predeterminado|  
|permitir propiedad de columna de longitud cero|restricción check|  
|regla de validación de columna|restricción check|  
|regla de validación de tabla|restricción check|  
|clave principal|clave principal|  
  
## <a name="converting-access-objects"></a>Convertir objetos de acceso  
Para convertir los objetos de base de datos de Access, primero debe seleccionar los objetos que desea convertir y, a continuación, usar SSMA para realizar la conversión. Para ver los mensajes de salida durante la conversión, en el menú **Ver** , seleccione **salida**.  
  
**Para seleccionar y convertir objetos de base de datos de Access en SQL Server o SQL Azure sintaxis**  
  
1.  En el explorador de metadatos de Access, expanda **Access-metabase**y, a continuación, expanda **bases**de datos.  
  
2.  Realice uno o varios de los procedimientos siguientes:  
  
    -   Para convertir todas las bases de datos, active la casilla situada junto a **bases de datos**.  
  
    -   Para convertir u omitir las bases de datos individuales, Active o desactive la casilla situada junto al nombre de la base de datos.  
  
    -   Para convertir u omitir consultas, expanda la base de datos y, a continuación, Active o desactive la casilla **consultas** .  
  
    -   Para convertir u omitir tablas individuales, expanda la base de datos, expanda **tablas**y, a continuación, Active o desactive la casilla situada junto a la tabla.  
  
3.  Realice una de las siguientes acciones:  
  
    -   Para convertir esquemas, haga clic con el botón derecho en **bases de datos** y seleccione **convertir esquema**.  
  
        También puede convertir objetos individuales. Para convertir un objeto, con independencia de los objetos seleccionados, haga clic con el botón secundario en el objeto y seleccione **convertir esquema**.  
  
        Cuando se ha convertido un objeto, aparece en negrita en el explorador de metadatos de Access.  
  
    -   Para convertir, cargar y migrar esquemas y datos en un solo paso, haga clic con el botón derecho en bases de datos y seleccione **convertir, cargar y migrar**.  
  
4.  Revise los mensajes en el panel de **salida** y los errores y advertencias en el panel de **lista de errores** .  
  
## <a name="altering-tables-and-indexes"></a>Modificar tablas e índices  
Después de convertir los metadatos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de acceso en o SQL Azure los metadatos, y antes [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de cargar los objetos en o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL Azure, puede modificar o SQL Azure tablas e índices.  
  
**Para modificar las propiedades de la tabla o el índice**  
  
1.  En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure explorador de metadatos, seleccione la tabla o el índice que desea modificar.  
  
2.  En la pestaña **tabla** , haga clic en la propiedad que desea modificar y, a continuación, escriba o seleccione la nueva configuración. Por ejemplo, puede cambiar nvarchar (15) a nvarchar (20) o activar una casilla para hacer que una columna de tabla admita valores NULL.  
  
    Desplace el cursor fuera de la celda de propiedad cambiada. Para ello, haga clic en otra fila o presione la tecla TAB.  
  
3.  Haga clic en **Aplicar**.  
  
Ahora puede ver los cambios en el código en la pestaña **SQL** .  
  
## <a name="next-step"></a>siguiente paso  
El siguiente paso del proceso de migración es [cargar los objetos de base de datos convertidos en SQL Server](loading-converted-database-objects-into-sql-server-accesstosql.md)  
  
## <a name="see-also"></a>Consulte también  
[Migrar bases de datos de Access a SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
