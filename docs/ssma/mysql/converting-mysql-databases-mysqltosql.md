---
title: Conversión de bases de datos de MySQL (MySQLToSQL) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssma-mysql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: ac21850b-fb32-4704-9985-5759b7c688c7
caps.latest.revision: 17
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: a1925166a672523f6e4cf5eef7cdc0bc5235c3fd
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="converting-mysql-databases-mysqltosql"></a>Conversión de bases de datos de MySQL (MySQLToSQL)
Después de haber conectado con MySQL, conectado a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure y el proyecto de conjunto y opciones de asignación de datos, puede convertir objetos de base de datos de MySQL a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] u objetos de base de datos de SQL Azure.  
  
## <a name="the-conversion-process"></a>El proceso de conversión  
Convertir objetos de base de datos toma las definiciones de objeto de MySQL, se convierte en similar [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure objetos y, a continuación, se carga esta información en los metadatos SSMA. No se carga la información en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. A continuación, puede ver los objetos y sus propiedades mediante el [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o en el Explorador de metadatos de SQL Azure.  
  
Durante la conversión, SSMA imprime mensajes de salida en el panel de resultados y mensajes de error en el panel de lista de errores. Use la información de salida y el error para determinar si tiene que modificar las bases de datos de MySQL o el proceso de conversión para obtener los resultados de la conversión deseada.  
  
## <a name="setting-conversion-options"></a>Establecer las opciones de conversión  
Antes de convertir objetos, revise las opciones de conversión de proyecto en el **configuración del proyecto** cuadro de diálogo. Mediante este cuadro de diálogo, puede establecer cómo SSMA convierte las tablas e índices. Para obtener más información, vea [configuración del proyecto &#40;conversión&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-conversion-mysqltosql.md)  
  
## <a name="conversion-results"></a>Resultados de la conversión  
La siguiente tabla muestra qué objetos de MySQL se convierten y resultante [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] objetos:  
  
|||  
|-|-|  
|**Objetos de MySQL**|**Objetos SQL Server resultantes**|  
|Tablas con los objetos dependientes, como los índices|SSMA crea tablas con los objetos dependientes. Tabla se convierte con todos los índices y restricciones. Los índices se convierten en diferentes [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] objetos.<br /><br />**Asignación de tipos de datos espaciales** pueden realizarse solo en el nivel del nodo de tabla.<br /><br />Para obtener más información sobre la configuración de conversión de la tabla, vea [la configuración de conversión](http://msdn.microsoft.com/en-us/f551cf6e-1575-4206-9cca-975b5b43a6b8)|  
|Funciones|Si la función se puede convertir directamente a Transact-SQL, SSMA crea una función. En algunos casos, la función debe convertirse en un procedimiento almacenado. Esto puede hacerse mediante el uso de **función conversión** en configuración del proyecto. En este caso, SSMA crea un procedimiento almacenado y una función que llama al procedimiento almacenado.<br /><br />**Opciones que se ofrecen:**<br /><br />Convertir según la configuración de proyecto<br /><br />Convertir a función<br /><br />Convertir en procedimiento almacenado<br /><br />Para obtener más información sobre la configuración de conversión de función, vea [la configuración de conversión](http://msdn.microsoft.com/en-us/f551cf6e-1575-4206-9cca-975b5b43a6b8)|  
|Procedimientos|Si el procedimiento se puede convertir directamente a Transact-SQL, SSMA crea un procedimiento almacenado. En algunos casos, un procedimiento almacenado debe llamarse en una transacción autónoma. En este caso, SSMA crea dos procedimientos almacenados: uno que implementa el procedimiento y otro que se usa para llamar a la implementación de procedimiento almacenado.|  
|Conversión de la base de datos|Las bases de datos como objetos de MySQL no se convierten directamente por SSMA para MySQL. Bases de datos MySQL, se tratan más como nombres de esquema y se pierden todos los parámetros físicos durante la conversión. SSMA para MySQL usa [asignación de bases de datos de MySQL a SQL Server esquemas &#40;MySQLToSQL&#41; ](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md) para asignar objetos de base de datos MySQL a par de esquema y base de datos de SQL Server apropiado.|  
|Conversión de desencadenador|**SSMA crea desencadenadores según las reglas siguientes:**<br /><br />ANTES de que los desencadenadores se convierten en los desencadenadores INSTEAD OF T-SQL<br /><br />Desencadenadores AFTER se convierten en los desencadenadores después de T-SQL con o sin iteraciones por filas.|  
|Conversión de vista|SSMA crea vistas con los objetos dependientes|  
|Conversión de instrucción|-Cada objeto de instrucción SQL puede contener una sola instrucción de MySQL (como DDL, DML y otros tipos de instrucciones) o BEGIN... Bloque final.<br />-   **Conversión de múltiples instrucciones: BEGIN... Conversión de bloque final**instrucción SQL también puede contener un BEGIN... Bloque final como de definición de procedimiento, función o desencadenador. Los bloques se deben convertir la misma manera que se convertirán para los objetos de instrucción únicos de MySQL.|  
  
## <a name="converting-mysql-database-objects"></a>Convertir objetos de base de datos MySQL  
Para convertir objetos de base de datos de MySQL, seleccione primero los objetos que se va a convertir y, a continuación, tener SSMA para realizar la conversión. Para ver los mensajes de salida durante la conversión, en la **vista** menú, seleccione **salida**.  
  
**Para convertir objetos de MySQL a sintaxis de SQL Server o SQL Azure**  
  
1.  En el Explorador de metadatos de MySQL, expanda el servidor MySQL y, a continuación, expanda **bases de datos**.  
  
2.  Seleccione los objetos que se va a convertir:  
  
    -   Para convertir todos los esquemas, active la casilla situada junto a **bases de datos**.  
  
    -   Para convertir u omitir una base de datos, active la casilla de verificación situada junto al nombre de la base de datos.  
  
    -   Para convertir u omitir una categoría de objetos, expanda un esquema y, a continuación, active o desactive la casilla situada junto a la categoría.  
  
    -   Para convertir u omitir los objetos individuales, expanda la carpeta de la categoría y, a continuación, active o desactive la casilla de verificación situada junto al objeto.  
  
3.  Para convertir todos los objetos seleccionados, haga clic en **bases de datos** y seleccione **convertir esquema**.  
  
    También puede convertir los objetos individuales o las categorías de objetos con el botón secundario en el objeto o su carpeta principal y, a continuación, seleccione **convertir esquema**.  
  
## <a name="viewing-conversion-problems"></a>Ver los problemas de conversión  
No se pueden convertir algunos objetos de MySQL. Puede determinar las tasas de éxito de conversión visualizando el informe de resumen de conversión.  
  
**Para ver un informe de resumen**  
  
1.  En el Explorador de metadatos de MySQL, seleccione **bases de datos**.  
  
2.  En el panel derecho, seleccione la **informe** ficha.  
  
    Este informe muestra el informe de resumen de evaluación para todos los objetos de base de datos que se han evaluado o convertir. También puede ver un informe de resumen para objetos individuales:  
  
    -   Para ver el informe de un esquema en particular, seleccione la base de datos en el Explorador de metadatos de MySQL.  
  
    -   Para ver el informe de un objeto individual, seleccione el objeto en el Explorador de metadatos de MySQL. Objetos que tienen problemas de conversión tienen un icono rojo de error.  
  
Para los objetos que no se pudo conversión, puede ver la sintaxis que produjo el error de conversión.  
  
**Para ver los problemas de conversión individuales**  
  
1.  En el Explorador de metadatos de MySQL, expanda **bases de datos**.  
  
2.  Expanda la base de datos que muestra un icono rojo de error.  
  
3.  En la base de datos, expanda una carpeta que tenga un icono rojo de error.  
  
4.  Seleccione el objeto que tiene un icono rojo de error.  
  
5.  En el panel derecho, haga clic en el **informe** ficha.  
  
6.  En la parte superior de la **informe** ficha es una lista desplegable. Si la lista muestra **estadísticas**, cambie la selección a **origen**.  
  
    SSMA mostrará el código fuente y varios botones inmediatamente encima del código.  
  
7.  Haga clic en el **problema siguiente** botón. Se trata de un icono de error rojo con una flecha que apunta a la derecha.  
  
    SSMA resaltará el primer código de origen problemático que encuentra en el objeto actual.  
  
Para cada elemento que no se pudo convertir, deberá determinar qué desea hacer con ese objeto:  
  
-   Puede modificar el objeto en la base de datos de MySQL para quitar o revisar cargue código problemático. Para cargar el código actualizado en SSMA, tendrá que actualizar los metadatos. Para obtener más información, consulte [conectar con MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)  
  
-   Puede excluir el objeto de la migración. En [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o el Explorador de metadatos de SQL Azure y el Explorador de metadatos de MySQL, desactive la casilla de verificación situada junto al elemento antes de cargar los objetos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure y migración de datos de MySQL.  
  
## <a name="next-step"></a>Paso siguiente  
El siguiente paso del proceso de migración es [cargar objetos de base de datos para convertir a SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/loading-converted-database-objects-into-sql-server-mysqltosql.md)  
  
## <a name="see-also"></a>Vea también  
[Bases de datos de migración desde MySQL a SQL Server: base de datos de SQL Azure &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
