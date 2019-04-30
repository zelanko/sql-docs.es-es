---
title: Conversión de esquemas de Oracle (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Conversion Results
ms.assetid: e021182d-31da-443d-b110-937f5db27272
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 18da150a435b5d3d61740139309d109a16691da3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63288892"
---
# <a name="converting-oracle-schemas-oracletosql"></a>Conversión de esquemas de Oracle (OracleToSQL)
Después de haberse conectado a Oracle, conectado a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], y establecer el proyecto y las opciones de asignación de datos, puede convertir los objetos de base de datos de Oracle para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] objetos de base de datos.  
  
## <a name="the-conversion-process"></a>El proceso de conversión  
Convertir objetos de base de datos toma las definiciones de objeto de Oracle, convierte a similar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] objetos y, a continuación, se carga esta información en los metadatos SSMA. No se carga la información en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A continuación, puede ver los objetos y sus propiedades mediante el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Explorador de metadatos.  
  
Durante la conversión, SSMA imprime mensajes de salida en el panel salida y mensajes de error en el panel de lista de errores. Use la información de salida y error para determinar si tiene que modificar las bases de datos de Oracle o el proceso de conversión para obtener los resultados de la conversión deseada.  
  
## <a name="setting-conversion-options"></a>Establecer las opciones de conversión  
Antes de convertir los objetos, revise las opciones de conversión de proyecto en el **configuración del proyecto** cuadro de diálogo. Mediante este cuadro de diálogo, puede establecer cómo SSMA convierte las funciones y variables globales. Para obtener más información, consulte [configuración del proyecto &#40;conversión&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-conversion-oracletosql.md).  
  
## <a name="conversion-results"></a>Resultados de la conversión  
La siguiente tabla muestra qué objetos de Oracle se convierten y resultante [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] objetos:  
  
|||  
|-|-|  
|Objetos de Oracle|Objetos de SQL Server resultantes|  
|Funciones|Si la función se puede convertir directamente en [!INCLUDE[tsql](../../includes/tsql-md.md)], SSMA crea una función.<br /><br />En algunos casos, la función debe convertirse a un procedimiento almacenado. En este caso, SSMA crea un procedimiento almacenado o una función que llama al procedimiento almacenado.|  
|Procedimientos|Si el procedimiento se puede convertir directamente en [!INCLUDE[tsql](../../includes/tsql-md.md)], SSMA crea un procedimiento almacenado.<br /><br />En algunos casos, un procedimiento almacenado debe llamarse en una transacción autónoma. En este caso, SSMA crea dos procedimientos almacenados: uno que implementa el procedimiento y otro que se usa para llamar a la que implementa el procedimiento almacenado.|  
|.|SSMA crea un conjunto de procedimientos almacenados y funciones que están unificadas por nombres de objetos similares.|  
|Secuencias|SSMA crea los objetos de secuencia (SQL Server 2012 o SQL Server 2014) o emula las secuencias de Oracle.|  
|Tablas con los objetos dependientes, como índices y desencadenadores|SSMA crea las tablas con los objetos dependientes.|  
|Ver con los objetos dependientes, como los desencadenadores|SSMA crea vistas con los objetos dependientes.|  
|Vistas materializadas|**SSMA crea vistas indizadas en SQL server con algunas excepciones. Se producirá un error en la conversión si la vista materializada incluye una o varias de las siguientes construcciones:**<br /><br />Función definida por el usuario<br /><br />Campo no determinista de función o expresión SELECT, donde o cláusulas GROUP BY<br /><br />Uso de Float de columna en SELECT *, donde o cláusulas GROUP BY (caso especial de problema anterior)<br /><br />Tipo de datos personalizado (incluido anidadas tablas)<br /><br />COUNT (distinct &lt;campo&gt;)<br /><br />FETCH<br /><br />Combinaciones externas (LEFT, RIGHT o FULL)<br /><br />Subconsulta, otra vista<br /><br />OTRA VEZ, RANK, CLIENTE POTENCIAL, INICIE SESIÓN<br /><br />MIN, MAX<br /><br />UNION, EL SIGNO MENOS, FORMAN UNA INTERSECCIÓN<br /><br />HAVING|  
|Desencadenador|**SSMA crea desencadenadores en función de las reglas siguientes:**<br /><br />ANTES de que los desencadenadores se convierten en los desencadenadores INSTEAD OF.<br /><br />Los desencadenadores AFTER se convierten en los desencadenadores AFTER.<br /><br />Los desencadenadores INSTEAD OF se convierten en los desencadenadores INSTEAD OF. Varios desencadenadores INSTEAD OF definidos en la misma operación se combinan en un desencadenador.<br /><br />Los desencadenadores de nivel de fila se emulan con cursores.<br /><br />Los desencadenadores en cascada se convierten en varios desencadenadores individuales.|  
|Sinónimos|**Sinónimos se crean para los tipos de objeto siguientes:**<br /><br />Las tablas y objetos<br /><br />Vistas y objetos<br /><br />Procedimientos almacenados<br /><br />Funciones<br /><br />**Sinónimos de los objetos siguientes están resueltas y reemplazados por referencias a objetos directos:**<br /><br />Secuencias<br /><br />.<br /><br />Objetos de esquema de clase de Java<br /><br />Tipos de objeto definido por el usuario<br /><br />Sinónimos de otro sinónimo no pueden migrarse y se marcará como errores.<br /><br />Sinónimos no se crean para las vistas de Materialized.|  
|Tipos definidos por el usuario|**SSMA no proporciona soporte técnico para la conversión de tipos definidos por el usuario. Tipos definidos por el usuario, incluyendo su uso en programas de PL/SQL se marcan con errores de conversión especial guiados por las reglas siguientes:**<br /><br />Columna de tabla de un tipo definido por el usuario se convierte a varchar (8000).<br /><br />Tipo definido por el argumento de usuario a un procedimiento almacenado o función se convierte a varchar (8000).<br /><br />Variable de tipo definido por el usuario en el bloque de PL/SQL se convierte a varchar (8000).<br /><br />Tabla de objetos se convierte en una tabla estándar.<br /><br />Vista del objeto se convierte en una vista estándar.|  
  
## <a name="converting-oracle-database-objects"></a>Convertir objetos de base de datos de Oracle  
Para convertir los objetos de base de datos de Oracle, seleccione primero los objetos que desea convertir y, a continuación, tener SSMA para realizar la conversión. Para ver los mensajes de salida durante la conversión, en el **vista** menú, seleccione **salida**.  
  
**Para convertir los objetos de Oracle en la sintaxis de SQL Server**  
  
1.  En el Explorador de metadatos de Oracle, expanda el servidor de Oracle y, a continuación, expanda **esquemas**.  
  
2.  Seleccione los objetos que desea convertir:  
  
    -   Para convertir todos los esquemas, seleccione la casilla de verificación junto a **esquemas**.  
  
    -   Para convertir u omitir una base de datos, seleccione la casilla de verificación junto al nombre del esquema.  
  
    -   Para convertir u omitir una categoría de objetos, expanda un esquema y, a continuación, active o desactive la casilla de verificación junto a la categoría.  
  
    -   Para convertir u omitir los objetos individuales, expanda la carpeta de categoría y, a continuación, active o desactive la casilla de verificación situada junto al objeto.  
  
3.  Para convertir todos los objetos seleccionados, haga clic en **esquemas** y seleccione **convertir esquema**.  
  
    También puede convertir los objetos individuales o categorías de objetos haciendo clic en el objeto o su carpeta principal y, a continuación, seleccione **convertir esquema**.  
  
## <a name="viewing-conversion-problems"></a>Ver los problemas de conversión  
No se pueden convertir algunos objetos de Oracle. Puede determinar las tasas de éxito de conversión viendo el informe de resumen de conversión.  
  
**Para ver un informe de resumen**  
  
1.  En el Explorador de metadatos de Oracle, seleccione **esquemas**.  
  
2.  En el panel derecho, seleccione el **informe** ficha.  
  
    Este informe muestra el informe de resumen de evaluación para todos los objetos de base de datos que se han evaluado o convertir. También puede ver un informe de resumen de los objetos individuales:  
  
    -   Para ver el informe para un esquema individual, seleccione el esquema en el Explorador de metadatos de Oracle.  
  
    -   Para ver el informe para un objeto individual, seleccione el objeto en el Explorador de metadatos de Oracle. Los objetos que tienen problemas de conversión tienen un icono rojo de error.  
  
Para los objetos que no se pudo conversión, puede ver la sintaxis que produjo el error de conversión.  
  
**Para ver los problemas de conversión individuales**  
  
1.  En el Explorador de metadatos de Oracle, expanda **esquemas**.  
  
2.  Expanda el esquema que se muestra un icono rojo de error.  
  
3.  En el esquema, expanda una carpeta que tiene un icono rojo de error.  
  
4.  Seleccione el objeto que tiene un icono rojo de error.  
  
5.  En el panel derecho, haga clic en el **informe** ficha.  
  
6.  En la parte superior de la **informe** ficha es una lista desplegable. Si la lista muestra **estadísticas**, cambie la selección a **origen**.  
  
    SSMA mostrará el código fuente y varios botones inmediatamente encima del código.  
  
7.  Haga clic en el **siguiente problema** botón. Se trata de un icono de error rojo con una flecha que señala a la derecha.  
  
    SSMA resaltará el primer código problemático de origen que encuentra en el objeto actual.  
  
Para cada elemento que no se pudo convertir, tendrá que determinar qué desea hacer con ese objeto:  
  
-   Puede modificar el código fuente para procedimientos en el **SQL** ficha.  
  
-   Puede modificar el objeto en la base de datos de Oracle para quitar o revisar código problemático. Para cargar el código actualizado en SSMA, tendrá que actualizar los metadatos. Para obtener más información, consulte [conectarse a Oracle Database &#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-oracle-database-oracletosql.md).  
  
-   El objeto se puede excluir de la migración. En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Explorador de metadatos y el Explorador de metadatos de Oracle, desactive la casilla de verificación situada junto al elemento antes de cargar los objetos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y migrar datos de Oracle.  
  
## <a name="next-step"></a>Paso siguiente  
El siguiente paso del proceso de migración es [cargar los objetos convertidos en SQL Server](loading-converted-database-objects-into-sql-server-oracletosql.md).  
  
## <a name="see-also"></a>Vea también  
[Bases de datos de migración de Oracle a SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
