---
title: Configuración (conversión) (MySQLToSQL) del proyecto | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 7ad5fe44-6445-4ba8-a457-5af792631f11
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 12e2e61c6b55bf3c549c08f2b090059d674ed83d
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/27/2018
ms.locfileid: "52411272"
---
# <a name="project-settings-conversion-mysqltosql"></a>Configuración del proyecto (conversión) (MySQLToSQL)
La página de conversión de la **configuración del proyecto** cuadro de diálogo contiene la configuración que permiten personalizar cómo SSMA convierte la sintaxis de MySQL a la sintaxis de SQL Server o SQL Azure.  
  
El panel de conversión está disponible en el **configuración del proyecto** y **configuración de proyecto predeterminada** cuadros de diálogo.  
  
-   Use la **configuración de proyecto predeterminada** cuadro de diálogo para establecer las opciones de configuración para todos los proyectos. Para obtener acceso a la configuración de conversión, en el **herramientas** menú, seleccione **la configuración predeterminada del proyecto**, seleccione el tipo de proyecto de migración para los que es necesaria para ver o cambiar de configuración  **Versión de destino de migración** lista desplegable, haga clic en **General** en la parte inferior del panel izquierdo y a continuación, seleccione **conversión**.  
  
-   Para especificar la configuración para el proyecto actual, en el **herramientas** menú haga clic en **configuración del proyecto**, a continuación, haga clic en **General** en la parte inferior del panel izquierdo y, a continuación, haga clic en **Conversión**.  
  
## <a name="options"></a>Opciones  
  
### <a name="collate-clause"></a>Cláusula de intercalación  
  
|||  
|-|-|  
|**Término**|**Definición**|  
|**Conversión explícita de cláusula COLLATE**|Opción de conversión de cláusula COLLATE explícita especifica cómo convertir las cláusulas COLLATE explícitas en el código de MySQL. Opciones posibles: Omitir y marcar con una advertencia o generar un Error<br /><br />**Modo predeterminado**:  Omitir y se marca con una advertencia<br /><br />**Modo optimista**:  Omitir y se marca con una advertencia<br /><br />**Modo completo**:  Omitir y se marca con una advertencia|  
  
### <a name="column-constraints"></a>Restricciones de columna  
  
|||  
|-|-|  
|**Término**|**Definición**|  
|**Generar la restricción de las columnas de tipo de datos de enumeración**|Genera la restricción de las columnas de tipo de datos de enumeración en la tabla de SQL Server o SQL Azure, si no está presente en la tabla de MySQL. En caso afirmativo, todas las columnas convertidas de tipo de datos de enumeración irá acompañadas de controlar el valor de restricción de comprobación.<br /><br />**Modo predeterminado**:   No<br /><br />**Modo optimista**:  No<br /><br />**Modo completo**:   Sí|  
|**Generar la restricción de las columnas de tipo de conjunto de datos**|Genera la restricción de las columnas de tipo de conjunto de datos en la tabla de SQL Server o SQL Azure, si no está presente en la tabla de MySQL. En caso afirmativo, todas las columnas convertidas de tipo de conjunto de datos irá acompañadas de controlar el valor de restricción de comprobación.<br /><br />**Modo predeterminado**:   No<br /><br />**Modo optimista**:  No<br /><br />**Modo completo**:   Sí|  
|**Generar la restricción de las columnas de las columnas de tipo de datos numérico sin signo**|Agregar comprobación para un valor no negativo a las columnas de tipos de datos numérico sin signo.<br /><br />**Modo predeterminado**:   No<br /><br />**Modo optimista**:  No<br /><br />**Modo completo**:   Sí|  
|**Generar la restricción de las columnas de tipo de datos de año**|Genera la restricción de las columnas de tipo de datos de año en la tabla de SQL Server o SQL Azure, si no está presente en la tabla de MySQL. En caso afirmativo, se han convertido las columnas de datos del año tipo irá acompañado de controlar el valor de restricción de comprobación.<br /><br />**Modo predeterminado**:   No<br /><br />**Modo optimista**:  No<br /><br />**Modo completo**:   Sí|  
  
### <a name="data-types"></a>Tipos de datos  
  
|||  
|-|-|  
|**Término**|**Definición**|  
|**Conversión de tipos de datos de enumeración**|Especifica cómo se debe convertir tipo de datos MySQL ENUM como convertir a NVARCHAR o convertir a numérico<br /><br />**Modo predeterminado**:  Convertir a NVARCHAR<br /><br />**Modo optimista**:  Convertir a NVARCHAR<br /><br />**Modo completo**:  Convertir a NVARCHAR|  
|**Conversión de tipos de conjunto de datos**|Especifica cómo MySQL establecer tipo de datos debe convertir, convertir a NVARCHAR (L) / convertir en BINARY(L)<br /><br />**Modo predeterminado**: Convertir en NVARCHAR(L)<br /><br />**Modo optimista**: Convertir en NVARCHAR(L)<br /><br />**Modo completo**: Convertir en NVARCHAR(L)|  
  
### <a name="generic"></a>Genérico  
  
|||  
|-|-|  
|**Término**|**Definición**|  
|**Columnas sin valor predeterminado de insertar y reemplazar**|Si todas las instrucciones que hacen referencia a tablas mediante motores almacenados que no sean MyISAM y InnoDb, 'Sí' debe marcarse con mensajes de advertencia de conversión.<br /><br />**Modo predeterminado**:  Agregar a lista de columnas<br /><br />**Modo optimista**:  Agregar a lista de columnas<br /><br />**Modo completo**:   Agregar a lista de columnas|  
|**División por cero conversión genera**|Especifica si desea emular MySQL sin comportamiento ERROR_FOR_DIVISION_BY_ZERO o no.<br /><br />**Modo predeterminado**:   Error<br /><br />**Modo optimista**:  Error<br /><br />**Modo completo**:   NULL|  
|**IN (operador)**|Especifica cómo convertir el operador IN de MySQL.<br /><br />**Modo predeterminado**:   Convertir siempre a IN<br /><br />**Modo optimista**:  Convertir siempre a IN<br /><br />**Modo completo**:   Expanda si es necesario|  
|**Conversión de la función de MySQL**|Especifica cómo convertir las funciones estándares de MySQL.<br /><br />**Modo predeterminado**:   Optimistic<br /><br />**Modo optimista**:  Optimistic<br /><br />**Modo completo**:   Preciso|  
|**No se admiten los motores de almacenamiento**|Si todas las instrucciones que hacen referencia a tablas mediante motores almacenados que no sean MyISAM y InnoDb, 'Sí' debe marcarse con mensajes de advertencia de conversión.<br /><br />**Modo predeterminado**:   No<br /><br />**Modo optimista**:  No<br /><br />**Modo completo**:   Sí|  
|**Suprimir la generación de una columna auxiliar ROWID**|En caso afirmativo, prohíbe la creación de la creación de una columna auxiliar ROWD en tablas de destino. Es posible que afectan a la migración de algunas estructuras.<br /><br />**Modo predeterminado**:   No<br /><br />**Modo optimista**:  No<br /><br />**Modo completo**:   No|  
|**Conversión de la instrucción TRUNCATE**|Especifica cómo convertir instrucciones TRUNCADAS.<br /><br />**Modo predeterminado**:   TRUNCATE<br /><br />**Modo optimista**:  TRUNCATE<br /><br />**Modo completo**:   TRUNCATE|  
  
### <a name="misc"></a>Varios  
  
|||  
|-|-|  
|**Término**|**Definición**|  
|**Asignación de esquema predeterminada**|Especifica cómo asignar las bases de datos MySQL a esquemas de SQL Server.<br /><br />**Modo predeterminado**:  Base de datos a la base de datos<br /><br />**Modo optimista**:  Base de datos a la base de datos<br /><br />**Modo completo**:  Base de datos a la base de datos|  
  
### <a name="procedures-and-functions"></a>Procedimientos y funciones  
  
|||  
|-|-|  
|**Término**|**Definición**|  
|**Conversión de función predeterminada**|Especifica si las funciones se de forma predeterminada se deben convertir a las funciones de Transact-SQL o procedimientos almacenados.<br /><br />**Modo predeterminado**:  Convertir a función<br /><br />**Modo optimista**:  Convertir a función<br /><br />**Modo completo**:  Convertir a función|  
|**Generar conjunto XACT_ABORT en**|Especifica si debe agregarse al principio del desencadenador o procedimiento convertido SET XACT_ABORT ON.<br /><br />**Modo predeterminado**:  Sí<br /><br />**Modo optimista**:  Sí<br /><br />**Modo completo**:  Sí|  
|**Generar SET NOCOUNT en**|Especifica si debe agregarse al principio del desencadenador o procedimiento convertido SET NOCOUNT ON.<br /><br />**Modo predeterminado**:  Sí<br /><br />**Modo optimista**:  Sí<br /><br />**Modo completo**:  Sí|  
  
### <a name="spatial-data-types"></a>Tipos de datos espaciales  
  
|||  
|-|-|  
|**Término**|**Definición**|  
|**Rectángulo del predeterminado {XMAX&#124;XMIN&#124;YMAX&#124;YMIN} para los índices espaciales**|Define el valor predeterminado de {XMAX&#124;XMIN&#124;YMAX&#124;YMIN} el parámetro de rectángulo utilizados en los índices espaciales.<br /><br />**Modo predeterminado**<br /><br />XMAX: 100<br /><br />XMIN: 0<br /><br />YMAX: 100<br /><br />YMIN: 0<br /><br />**Modo optimista**<br /><br />XMAX: 100<br /><br />XMIN: 0<br /><br />YMAX:  100<br /><br />YMIN: 0<br /><br />**Modo completo**<br /><br />XMAX: 100<br /><br />XMIN: 0<br /><br />YMAX: 100<br /><br />YMIN: 0|  
|**Densidad de cuadrícula predeterminada para los índices espaciales**|Define el valor predeterminado para LEVEL_1, LEVEL_2, LEVEL_3 y LEVEL_4 de densidad de cuadrícula utilizada en índices espaciales.<br /><br />**Modo predeterminado**<br /><br />LEVEL_1: Default<br /><br />LEVEL_2: Default<br /><br />LEVEL_3: Default<br /><br />LEVEL_4: Default<br /><br />**Modo optimista**<br /><br />LEVEL_1: Default<br /><br />LEVEL_2: Default<br /><br />LEVEL_3: Default<br /><br />LEVEL_4: Default<br /><br />**Modo completo**<br /><br />LEVEL_1: Default<br /><br />LEVEL_2: Default<br /><br />LEVEL_3: Default<br /><br />LEVEL_4: Default|  
  
### <a name="transactions"></a>Transactions  
  
|||  
|-|-|  
|**Término**|**Definición**|  
|**Tablas no transaccional**|Especifica si se deben marcar todas las referencias a la tabla que no admiten transacciones con mensajes de advertencia de conversión.<br /><br />**Modo predeterminado**: No<br /><br />**Modo optimista**: No<br /><br />**Modo completo**: Sí|  
|**nivel de aislamiento de transacción**|Especifica qué nivel de aislamiento de transacción se debe usar para las nuevas transacciones.<br /><br />**Modo predeterminado**:   Default<br /><br />**Modo optimista**:  Default<br /><br />**Modo completo**:   Lectura repetible|  
  
### <a name="value-control"></a>Control de valor  
  
|||  
|-|-|  
|**Término**|**Definición**|  
|**Carácter de conversión numérica**|Especifica cómo controlar la conversión implícita y explícita del tipo de datos de caracteres para los tipos de datos numéricos.<br /><br />**Modo predeterminado**:   Optimistic<br /><br />**Modo optimista**:  Optimistic<br /><br />**Modo completo**:   Preciso|  
|**Controlar valores numéricos sin signo**|Control de asignación de valores para parámetros y variables numéricas sin signo.<br /><br />**Modo predeterminado**:   No<br /><br />**Modo optimista**:  No<br /><br />**Modo completo**:   Sí|  
|**Resta de control sin signo**|Modifique los valores negativos insertados en las columnas de tabla de tipo de datos sin signo.<br /><br />**Modo predeterminado**:   Convertir ' como-es '<br /><br />**Modo optimista**:  Convertir ' como-es '<br /><br />**Modo completo**:   Marcar con una advertencia|  
|**Conversión de tipo de datos binarios**|Especifica cómo controlar las conversiones implícitas y explícitas de tipos de datos binarios.<br /><br />**Modo predeterminado**:   Optimistic<br /><br />**Modo optimista**:  Optimistic<br /><br />**Modo completo**:   Preciso|  
|**Tipo de conversión de datos de fecha y hora**|Especifica cómo controlar las conversiones implícitas y explícitas a la fecha y hora de tipo de datos.<br /><br />**Modo predeterminado**:   Emular el formato de MySQL<br /><br />**Modo optimista**:  Usar el formato de SQL Server<br /><br />**Modo completo**:   Emular el formato de MySQL|  
|**Literales numéricos con una precisión superior a 38**|Especifica cómo convertir literales numéricos con una precisión superior a 38.<br /><br />**Modo predeterminado**:   Si es posible de ida y vuelta<br /><br />**Modo optimista**:  Si es posible de ida y vuelta<br /><br />**Modo completo**:   Si es posible de ida y vuelta|  
|**Fecha cero en las columnas NOT NULL**|Especifica cómo controlar la asignación de columnas NOT NULL de la fecha cero, fecha de cero o valores de fecha y hora no válido.<br /><br />**Modo predeterminado**:   GETDATE()<br /><br />**Modo optimista**:  GETDATE()<br /><br />**Modo completo**:   GETDATE()|  
  
## <a name="see-also"></a>Vea también  
[Referencia de la interfaz de usuario &#40;MySQLToSQL&#41;](../../ssma/mysql/user-interface-reference-mysqltosql.md)  
  
