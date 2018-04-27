---
title: Configuración (conversión) (MySQLToSQL) del proyecto | Documentos de Microsoft
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-mysql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 7ad5fe44-6445-4ba8-a457-5af792631f11
caps.latest.revision: 19
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 47bb86d67219dd5656a6864a4603adc382a36128
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="project-settings-conversion-mysqltosql"></a>Configuración del proyecto (conversión) (MySQLToSQL)
La página de conversión de la **configuración del proyecto** cuadro de diálogo contiene la configuración que permiten personalizar cómo SSMA convierte la sintaxis de MySQL a la sintaxis de SQL Server o SQL Azure.  
  
El panel de conversión está disponible en la **configuración del proyecto** y **configuración de proyecto predeterminada** cuadros de diálogo.  
  
-   Use la **configuración de proyecto predeterminada** cuadro de diálogo para establecer las opciones de configuración para todos los proyectos. Para acceder a la configuración de conversión, en la **herramientas** menú, seleccione **la configuración predeterminada del proyecto**, seleccione el tipo de proyecto de migración para el que se requiere para ver / cambiar de configuración **versión de destino de migración** de lista desplegable, haga clic en **General** en la parte inferior del panel izquierdo y, a continuación, seleccione **conversión**.  
  
-   Para especificar la configuración para el proyecto actual, en la **herramientas** menú haga clic en **configuración del proyecto**, a continuación, haga clic en **General** en la parte inferior del panel izquierdo y, a continuación, haga clic en **conversión**.  
  
## <a name="options"></a>Opciones  
  
### <a name="collate-clause"></a>Cláusula de intercalación  
  
|||  
|-|-|  
|**Término**|**Definición**|  
|**Conversión explícita de cláusula COLLATE**|Opción de conversión de cláusula COLLATE explícita especifica cómo convertir cláusulas COLLATE explícitas en el código de MySQL. Las opciones posibles: Pasar por alto y marcar con una advertencia / generará un Error<br /><br />**Modo predeterminado**: pasar por alto y se marca con una advertencia<br /><br />**Modo optimista**: pasar por alto y se marca con una advertencia<br /><br />**Modo completo**: pasar por alto y se marca con una advertencia|  
  
### <a name="column-constraints"></a>Restricciones de columna  
  
|||  
|-|-|  
|**Término**|**Definición**|  
|**Generar restricción para las columnas de tipo de datos de enumeración**|Genera una restricción para las columnas de tipo de datos de enumeración en la tabla de SQL Server o SQL Azure, si no está presente en la tabla de MySQL. Si es así, todas las columnas convertidas de tipo de datos ENUM irá acompañadas de control del valor de restricción de comprobación.<br /><br />**Modo predeterminado**: No<br /><br />**Modo optimista**: No<br /><br />**Modo completo**: Sí|  
|**Generar restricción para las columnas de tipo de conjunto de datos**|Genera la restricción para las columnas de tipo de conjunto de datos en la tabla de SQL Server o SQL Azure, si no está presente en la tabla de MySQL. Si es así, irá todas las columnas convertidas de tipo de conjunto de datos con la restricción de comprobación de control del valor.<br /><br />**Modo predeterminado**: No<br /><br />**Modo optimista**: No<br /><br />**Modo completo**: Sí|  
|**Generar restricción para las columnas de las columnas de tipo de datos numérico sin signo**|Agregar comprobación de un valor no negativo para las columnas de tipos de datos numérico sin signo.<br /><br />**Modo predeterminado**: No<br /><br />**Modo optimista**: No<br /><br />**Modo completo**: Sí|  
|**Generar restricción para las columnas de tipo de datos de año**|Genera una restricción para las columnas de tipo de datos de año en la tabla de SQL Server o SQL Azure, si no está presente en la tabla de MySQL. En caso afirmativo, todos los convierten columnas de datos del año irá acompañado con restricción de comprobación de control del valor del tipo.<br /><br />**Modo predeterminado**: No<br /><br />**Modo optimista**: No<br /><br />**Modo completo**: Sí|  
  
### <a name="data-types"></a>Tipos de datos  
  
|||  
|-|-|  
|**Término**|**Definición**|  
|**Conversión de tipos de datos de enumeración**|Especifica cómo se debe convertir tipo de datos de MySQL ENUM como convertir a NVARCHAR o convertir a numérico<br /><br />**Modo predeterminado**: convertir a NVARCHAR<br /><br />**Modo optimista**: convertir a NVARCHAR<br /><br />**Modo completo**: convertir a NVARCHAR|  
|**Conversión de tipos de conjunto de datos**|Especifica cómo debe aplicarse el tipo de datos de MySQL establecer convertir, convertir a NVARCHAR (L) / Convert para BINARY(L)<br /><br />**Modo predeterminado**: convertir en NVARCHAR(L)<br /><br />**Modo optimista**: convertir en NVARCHAR(L)<br /><br />**Modo completo**: convertir en NVARCHAR(L)|  
  
### <a name="generic"></a>Genérico  
  
|||  
|-|-|  
|**Término**|**Definición**|  
|**Columnas sin valor predeterminado en INSERT y reemplazar**|Si 'Sí', todas las instrucciones que hacen referencia a tablas mediante motores almacenados que no sean MyISAM y InnoDb debería marcarse con mensajes de advertencia de conversión.<br /><br />**Modo predeterminado**: agregar a la lista de columnas<br /><br />**Modo optimista**: agregar a la lista de columnas<br /><br />**Modo completo**: agregar a la lista de columnas|  
|**División por cero produce de conversión**|Especifica si desea emular MySQL sin comportamiento ERROR_FOR_DIVISION_BY_ZERO o no.<br /><br />**Modo predeterminado**: Error<br /><br />**Modo optimista**: Error<br /><br />**Modo completo**: NULL|  
|**IN (operador)**|Especifica cómo convertir a operador IN de MySQL.<br /><br />**Modo predeterminado**: convertir siempre a pulgadas<br /><br />**Modo optimista**: convertir siempre a pulgadas<br /><br />**Modo completo**: expanda si es necesario|  
|**Conversión de función de MySQL**|Especifica cómo convertir las funciones estándar de MySQL.<br /><br />**Modo predeterminado**: optimista<br /><br />**Modo optimista**: optimista<br /><br />**Modo completo**: precisa|  
|**No admite los motores de almacenamiento**|Si 'Sí', todas las instrucciones que hacen referencia a tablas mediante motores almacenados que no sean MyISAM y InnoDb debería marcarse con mensajes de advertencia de conversión.<br /><br />**Modo predeterminado**: No<br /><br />**Modo optimista**: No<br /><br />**Modo completo**: Sí|  
|**Suprimir la generación de columna auxiliar ROWID**|En caso afirmativo, prohíbe la creación de la creación de la columna auxiliar de ROWD en tablas de destino. Puede afectar a la migración de algunas estructuras.<br /><br />**Modo predeterminado**: No<br /><br />**Modo optimista**: No<br /><br />**Modo completo**: No|  
|**Conversión de la instrucción TRUNCATE**|Especifica cómo convertir instrucciones TRUNCADAS.<br /><br />**Modo predeterminado**: truncar<br /><br />**Modo optimista**: truncar<br /><br />**Modo completo**: truncar|  
  
### <a name="misc"></a>Varios  
  
|||  
|-|-|  
|**Término**|**Definición**|  
|**Asignación del esquema predeterminado**|Especifica cómo asignar las bases de datos de MySQL a esquemas de SQL Server.<br /><br />**Modo predeterminado**: base de datos a la base de datos<br /><br />**Modo optimista**: base de datos a la base de datos<br /><br />**Modo completo**: base de datos a la base de datos|  
  
### <a name="procedures-and-functions"></a>Procedimientos y funciones  
  
|||  
|-|-|  
|**Término**|**Definición**|  
|**Conversión de función predeterminado**|Especifica si las funciones se predeterminada se deben convertir a funciones de T-SQL o a procedimientos almacenados.<br /><br />**Modo predeterminado**: convertir a función<br /><br />**Modo optimista**: convertir a función<br /><br />**Modo completo**: convertir a función|  
|**Generar conjunto XACT_ABORT en**|Especifica si debe agregarse al principio del desencadenador o procedimiento convertido SET XACT_ABORT ON.<br /><br />**Modo predeterminado**: Sí<br /><br />**Modo optimista**: Sí<br /><br />**Modo completo**: Sí|  
|**Generar SET NOCOUNT en**|Especifica si debe agregarse al principio del desencadenador o procedimiento convertido SET NOCOUNT ON.<br /><br />**Modo predeterminado**: Sí<br /><br />**Modo optimista**: Sí<br /><br />**Modo completo**: Sí|  
  
### <a name="spatial-data-types"></a>Tipos de datos espaciales  
  
|||  
|-|-|  
|**Término**|**Definición**|  
|**Cuadro de límite de predeterminado {XMAX&#124;XMIN&#124;YMAX&#124;YMIN} para los índices espaciales**|Define el valor predeterminado de {XMAX&#124;XMIN&#124;YMAX&#124;YMIN} parámetro del rectángulo de selección utilizadas en índices espaciales.<br /><br />**Modo predeterminado**<br /><br />XMAX: 100<br /><br />XMIN: 0<br /><br />YMAX: 100<br /><br />YMIN: 0<br /><br />**Modo optimista**<br /><br />XMAX: 100<br /><br />XMIN: 0<br /><br />YMAX: 100<br /><br />YMIN: 0<br /><br />**Modo completo**<br /><br />XMAX: 100<br /><br />XMIN: 0<br /><br />YMAX: 100<br /><br />YMIN: 0|  
|**Densidad de cuadrícula predeterminada para los índices espaciales**|Define el valor predeterminado para LEVEL_1, LEVEL_2, LEVEL_3 y LEVEL_4 de densidad de cuadrícula utilizada en índices espaciales.<br /><br />**Modo predeterminado**<br /><br />LEVEL_1: predeterminado<br /><br />LEVEL_2: predeterminado<br /><br />LEVEL_3: predeterminado<br /><br />LEVEL_4: predeterminado<br /><br />**Modo optimista**<br /><br />LEVEL_1: predeterminado<br /><br />LEVEL_2: predeterminado<br /><br />LEVEL_3: predeterminado<br /><br />LEVEL_4: predeterminado<br /><br />**Modo completo**<br /><br />LEVEL_1: predeterminado<br /><br />LEVEL_2: predeterminado<br /><br />LEVEL_3: predeterminado<br /><br />LEVEL_4: predeterminado|  
  
### <a name="transactions"></a>Transactions  
  
|||  
|-|-|  
|**Término**|**Definición**|  
|**Tablas no transaccional**|Especifica si se permite o no todas las referencias a la tabla que no son compatibles con las transacciones deben estar marcadas con mensajes de advertencia de conversión.<br /><br />**Modo predeterminado**: No<br /><br />**Modo optimista**: No<br /><br />**Modo completo**: Sí|  
|**Nivel de aislamiento de transacción**|Especifica qué nivel de aislamiento de transacción se debe usar para las nuevas transacciones.<br /><br />**Modo predeterminado**: predeterminado<br /><br />**Modo optimista**: predeterminado<br /><br />**Modo completo**: lectura repetible|  
  
### <a name="value-control"></a>Valor (control)  
  
|||  
|-|-|  
|**Término**|**Definición**|  
|**Carácter de conversión numérica**|Especifica cómo controlar la conversión implícita y explícita del tipo de datos de caracteres para los tipos de datos numéricos.<br /><br />**Modo predeterminado**: optimista<br /><br />**Modo optimista**: optimista<br /><br />**Modo completo**: precisa|  
|**Controlar valores numéricos sin signo**|Control de asignación de valores para parámetros y variables numéricas sin signo.<br /><br />**Modo predeterminado**: No<br /><br />**Modo optimista**: No<br /><br />**Modo completo**: Sí|  
|**Resta sin signo de control**|Modifique los valores negativos insertados en las columnas de tabla de tipo de datos sin signo.<br /><br />**Modo predeterminado**: convertir ' como-es "<br /><br />**Modo optimista**: convertir ' como-es "<br /><br />**Modo completo**: marca con una advertencia|  
|**Conversión a y desde el tipo de datos binarios**|Especifica cómo controlar la conversión implícita y explícita del tipo de datos binarios.<br /><br />**Modo predeterminado**: optimista<br /><br />**Modo optimista**: optimista<br /><br />**Modo completo**: precisa|  
|**Tipo de conversión de datos de fecha y hora**|Especifica cómo controlar las conversiones implícitas y explícitas en fecha/hora de tipo de datos.<br /><br />**Modo predeterminado**: formato de emular MySQL<br /><br />**Modo optimista**: formato de usar SQL Server<br /><br />**Modo completo**: formato de emular MySQL|  
|**Literales numéricos con una precisión superior a 38**|Especifica cómo convertir literales numéricos con una precisión superior a 38.<br /><br />**Modo predeterminado**: si es posible de ida y vuelta<br /><br />**Modo optimista**: si es posible de ida y vuelta<br /><br />**Modo completo**: si es posible de ida y vuelta|  
|**Fecha cero en columnas NOT NULL**|Especifica cómo controlar la asignación de columnas NOT NULL de la fecha cero, cero en la fecha o valores de fecha y hora no válido.<br /><br />**Modo predeterminado**: GETDATE()<br /><br />**Modo optimista**: GETDATE()<br /><br />**Modo completo**: GETDATE()|  
  
## <a name="see-also"></a>Vea también  
[Referencia de la interfaz de usuario &#40;MySQLToSQL&#41;](../../ssma/mysql/user-interface-reference-mysqltosql.md)  
  
