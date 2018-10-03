---
title: Asesor de optimización de memoria | Microsoft Docs
ms.custom: ''
ms.date: 10/26/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
f1_keywords:
- sql12.swb.memoryoptimizationwizard.f1
- swb.memoryoptimizationwizard.f1
ms.assetid: 181989c2-9636-415a-bd1d-d304fc920b8a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d616312ffec682ad7c37da62c23c4ada1eb98f00
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48140995"
---
# <a name="memory-optimization-advisor"></a>Asesor de optimización de memoria
  La herramienta de informes de rendimiento de las transacciones (vea [Determinar si una tabla o un procedimiento almacenado se debe pasar a OLTP en memoria](determining-if-a-table-or-stored-procedure-should-be-ported-to-in-memory-oltp.md)) le informa sobre qué tablas de la base de datos se beneficiarían de una conversión para utilizar OLTP en memoria. Después de identificar la tabla que desea convertir para que utilice OLTP en memoria, puede usar el Asistente de optimización de memoria para que le ayude a migrar la tabla de base de datos basada en disco a OLTP en memoria.  
  
 Para empezar, conéctese a la instancia que contiene la tabla de base de datos basada en disco. Puede conectarse a una instancia de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] o [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] . Sin embargo, si desea realizar una operación de migración con el asistente, debe conectarse a una instancia de [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] que tenga habilitada la funcionalidad de OLTP en memoria. Para obtener más información acerca de los requisitos de OLTP en memoria, vea [Requirements for Using Memory-Optimized Tables](memory-optimized-tables.md).  
  
 Para obtener más información sobre las metodologías de migración, vea [OLTP en memoria: patrones de carga de trabajo comunes y consideraciones sobre la migración](http://msdn.microsoft.com/library/dn673538.aspx).  
  
## <a name="walkthrough-using-the-memory-optimization-advisor"></a>Tutorial del uso del Asistente de optimización de memoria  
 En el **Explorador de objetos**, haga clic con el botón derecho en la tabla que quiere convertir y seleccione **Asistente de optimización de memoria**. Se mostrará la página de bienvenida del **Asistente de optimización de memoria de tablas**.  
  
### <a name="memory-optimization-checklist"></a>Lista de comprobación de la optimización de memoria  
 Al hacer clic en **Siguiente** en la página de bienvenida del **Asistente de optimización de memoria de tablas**, verá la lista de comprobación de la optimización de memoria. Las tablas con optimización para memoria no admiten todas las características de las tablas basadas en disco. La lista de comprobación optimizada para memoria indica si la tabla basada en disco utiliza características incompatibles con una tabla optimizada para memoria. El **Asistente de optimización de memoria de tablas** no modifica la tabla basada en disco, lo que permite migrarla para que use OLTP en memoria. Debe realizar esos cambios antes de continuar con la migración. Para cada incompatibilidad que encuentra, el **Asistente de optimización de memoria de tablas** muestra un vínculo a información que puede ayudarle a modificar las tablas basadas en disco.  
  
 Si desea guardar una lista de dichas incompatibilidades para planear la migración, haga clic en **Generar informe** para generar una lista en HTML.  
  
 Si la tabla no tiene ninguna incompatibilidad y está conectado a una instancia de [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] con OLTP en memoria, haga clic en **Siguiente**.  
  
### <a name="memory-optimization-warnings"></a>Advertencias de la optimización de memoria  
 La siguiente página, Advertencias de la optimización de memoria, contiene una lista de problemas que no impiden que la tabla se migre para utilizar OLTP en memoria, pero que pueden hacer que el comportamiento de otros objetos (como los procedimientos almacenados o las funciones CLR) produzca errores o provoque un comportamiento inesperado.  
  
 Las primeras advertencias de la lista son informativas y pueden o no ser aplicables a la tabla. Los vínculos de la columna derecha de la tabla le permitirán obtener más información.  
  
 La tabla de advertencias también mostrará las posibles condiciones de advertencia que no se encuentran en la tabla.  
  
 Las advertencias que requieren acciones tienen un triángulo amarillo en la columna de la izquierda. Si existen advertencias de ese tipo, debe salir de la migración, resolverlas y después reiniciar el proceso. Si no resuelve las advertencias, la tabla migrada puede producir un error.  
  
 Haga clic en **Generar informe** para generar un informe HTML con dichas advertencias. Haga clic en **Siguiente** para continuar.  
  
### <a name="review-optimization-options"></a>Revisar opciones de optimización  
 La pantalla siguiente permite modificar las opciones para la migración a OLTP en memoria:  
  
 Grupo de archivos con optimización para memoria  
 El nombre del grupo de archivos optimizados para memoria. Para poder crear una tabla optimizada para memoria, una base de datos debe tener un grupo de archivos optimizados para memoria con un archivo como mínimo.  
  
 Si no tiene un grupo de archivos optimizados para memoria, puede cambiar el nombre predeterminado. Los grupos de archivos con optimización para memoria no se pueden eliminar. La existencia de un grupo de archivos optimizados para memoria puede deshabilitar algunas características de base de datos como AUTO CLOSE y la creación de reflejo de la base de datos.  
  
 Si una base de datos tiene un grupo de archivos optimizados para memoria, su nombre aparece en este campo y no podrá cambiar el valor de este campo.  
  
 Nombre y ruta de acceso del archivo lógico  
 El nombre del archivo que contendrá la tabla optimizada para memoria. Para poder crear una tabla optimizada para memoria, una base de datos debe tener un grupo de archivos optimizados para memoria con un archivo como mínimo.  
  
 Si no tiene un grupo de archivos optimizados para memoria existente, puede cambiar el nombre y la ruta de acceso predeterminados del archivo, y este se creará al final del proceso de migración.  
  
 Si tiene un grupo de archivos optimizados para memoria existente, estos campos se rellenan de antemano y no podrá cambiar los valores.  
  
 Cambiar el nombre de la tabla original a  
 Al final del proceso de migración, se creará una nueva tabla optimizada para memoria con el nombre actual de la tabla. Para evitar un conflicto de nombres, se debe cambiar el nombre de la tabla actual. Puede cambiar el nombre en este campo.  
  
 Costo estimado de memoria actual (MB)  
 El Asistente de optimización de memoria calcula la cantidad de memoria que utilizará la nueva tabla optimizada para memoria basándose en los metadatos de la tabla basada en disco. El cálculo del tamaño de la tabla se explica en [Tamaño de tabla y fila de las tablas con optimización para memoria](table-and-row-size-in-memory-optimized-tables.md).  
  
 Si no se asigna suficiente memoria, el proceso de migración puede producir un error.  
  
 También copiar los datos de la tabla en la nueva tabla con optimización para memoria  
 Seleccione esta opción si desea que también se muevan los datos de la tabla actual a la nueva tabla optimizada para memoria. Si no selecciona esta opción, la nueva tabla optimizada para memoria se creará sin filas.  
  
 La tabla se migrará como tabla perdurable de forma predeterminada  
 OLTP en memoria admite tablas no perdurables que tienen un rendimiento superior en comparación con las tablas optimizadas para memoria perdurables. Sin embargo, los datos de una tabla no perdurable se perderán de reiniciar el servidor.  
  
 Si selecciona esta opción, el Asistente de optimización de memoria creará una tabla no perdurable en lugar de una tabla perdurable.  
  
> [!WARNING]  
>  Seleccione esta opción únicamente si entiende el riesgo de pérdida de datos asociado a las tablas no perdurables.  
  
 Para continuar, haga clic en **Siguiente** .  
  
### <a name="review-primary-key-conversion"></a>Revisar la conversión de la clave principal  
 La pantalla siguiente es **Revisar la conversión de la clave principal**. El Asistente de optimización de memoria detectará si hay una o varias claves principales en la tabla y rellenará la lista de columnas basándose en los metadatos de la clave principal. Si no la hay, debe crear una clave principal si desea migrar a una tabla optimizada para memoria perdurable.  
  
 Si no existe una clave principal y la tabla se está migrando a una tabla no perdurable, esta pantalla no aparecerá.  
  
 Para las columnas de texto (columnas de tipo `char`, `nchar`, `varchar` y `nvarchar`) debe seleccionar la intercalación adecuada. OLTP en memoria solo admite las intercalaciones BIN2 para las columnas de una tabla optimizada para memoria y no admite intercalaciones con caracteres adicionales. Vea [Collations and Code Pages](../../database-engine/collations-and-code-pages.md) para obtener información sobre las intercalaciones admitidas y el posible impacto de un cambio de la intercalación.  
  
 Puede configurar los parámetros siguientes para la clave principal:  
  
 Seleccione un nuevo nombre para esta clave principal  
 El nombre de la clave principal de la tabla debe ser único en la base de datos. Puede cambiar el nombre de la clave principal aquí.  
  
 Seleccione el tipo de esta clave principal  
 OLTP en memoria admite dos tipos de índices en una tabla optimizada para memoria:  
  
-   Un índice NONCLUSTERED HASH. Este índice es mejor para los índices con muchas búsquedas de puntos. Puede configurar el número de cubos para este índice en el campo **Número de cubos** .  
  
-   Un índice NONCLUSTERED. Este tipo de índice es mejor para los índices con muchas consultas por rango. Puede configurar el criterio de ordenación para cada columna en la lista **Columna de ordenación y orden** .  
  
 Para conocer cuál es el tipo de índice más adecuado para cada clave principal, vea [Índices hash](../../database-engine/hash-indexes.md).  
  
 Haga clic en **Siguiente** cuando seleccione las opciones de la clave principal.  
  
### <a name="review-index-conversion"></a>Revisar la conversión del índice  
 La página siguiente es **Revisar la conversión del índice**. El Asistente de optimización de memoria detectará si hay uno o varios índices en la tabla y rellenará la lista de columnas y el tipo de datos. Los parámetros que puede configurar en la página **Revisar la conversión del índice** son similares a los de la página anterior, **Revisar la conversión de la clave principal** .  
  
 Esta pantalla no aparecerá si la tabla tiene únicamente una clave principal y se está migrando a una tabla perdurable.  
  
 Cuando haya configurado todos los índices de la tabla, haga clic en **Siguiente**.  
  
### <a name="verify-migration-actions"></a>Comprobar acciones de migración  
 La página siguiente es **Comprobar acciones de migración**. Para crear un script para la operación de migración, haga clic en **Script** para generar un script de [!INCLUDE[tsql](../../includes/tsql-md.md)] . A continuación, puede modificar y ejecutar el script. Haga clic en **Migrar** para comenzar la migración de la tabla.  
  
 Después de que finalice el proceso, actualice el **Explorador de objetos** para ver la nueva tabla optimizada para memoria y la tabla basada en disco antigua. Puede conservar la tabla antigua o eliminarla según le convenga.  
  
## <a name="see-also"></a>Vea también  
 [Migrar a OLTP en memoria](migrating-to-in-memory-oltp.md)  
  
  
