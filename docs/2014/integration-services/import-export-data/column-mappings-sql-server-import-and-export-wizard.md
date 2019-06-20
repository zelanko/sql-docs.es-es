---
title: Asignaciones de columnas (Asistente para importación y exportación de SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.columnmapandtransform.f1
ms.assetid: eadc54a6-f936-4ffc-91d7-fbfd2bdcab93
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 0108004bc7fb5743ab92c455f4aee99a9f3df498
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62893046"
---
# <a name="column-mappings-sql-server-import-and-export-wizard"></a>Asignaciones de columnas (Asistente para importación y exportación de SQL Server)
  Use la **asignaciones de columnas** cuadro de diálogo para editar los parámetros de transformación.  
  
> [!NOTE]  
>  No es necesario copiar todas las columnas en una tabla al seleccionar la opción de copia de tabla. Seleccione  **\<omitir >** en el **destino** columna de este cuadro de diálogo para las columnas que desea omitir.  
  
 Para obtener más información acerca de este asistente, vea [Asistente para importación y exportación de SQL Server](import-and-export-data-with-the-sql-server-import-and-export-wizard.md). Para obtener información acerca de las opciones para iniciar el asistente, así como los permisos necesarios para ejecutar el asistente correctamente, consulte [ejecutar la importación de SQL Server y el Asistente para exportación de](start-the-sql-server-import-and-export-wizard.md).  
  
 La finalidad del Asistente para importación y exportación de SQL Server es copiar datos desde un origen a un destino. El asistente también puede crear una base de datos y tablas de destino. Sin embargo, si tiene que copiar diversas bases de datos o tablas, u otros tipos de objetos de bases de datos, debe utilizar el Asistente para copiar bases de datos. Para más información, consulte [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md).  
  
## <a name="options"></a>Opciones  
 **Source**  
 Identifica la tabla, vista o consulta de origen seleccionada.  
  
 **Destino**  
 Identifica la tabla, vista o consulta de destino seleccionada.  
  
 **Crear tabla o archivo de destino**  
 Especifique si debe crearse una tabla de destino si todavía no existe.  
  
 **Eliminar filas en la tabla o archivo de destino**  
 Especifique si deben eliminarse datos de una tabla existente antes de cargar datos nuevos.  
  
 **Anexar filas a la tabla o archivo de destino**  
 Especifique si deben anexarse datos nuevos a los datos que contiene una tabla existente.  
  
 **Editar SQL**  
 Utilice la instrucción predeterminada en el **instrucción Create Table SQL** diálogo cuadro o modificarlo para sus fines. Si modifica la instrucción, también deberá realizar los cambios asociados en la asignación de tablas.  
  
 **Quitar y volver a crear la tabla de destino**  
 Elija esta opción para sobrescribir la tabla de destino. Esta opción solo está disponible si se usa el asistente para crear la tabla de destino. La tabla de destino se quita y se vuelve a crear solo si guarda el paquete que el asistente crea y, a continuación, ejecuta el paquete de nuevo.  
  
 **Habilitar la inserción de identidad**  
 Elija esta opción para poder insertar los valores de identidad existentes del origen de datos en una columna de identidad de la tabla de destino. De forma predeterminada, la columna de identidad de destino no lo permite.  
  
 **Asignaciones**  
 Muestra el modo en que cada columna del origen de datos se asigna a una columna en el destino.  
  
 Esta lista tiene las columnas siguientes:  
  
 **Source**  
 Muestre cada columna de origen para la que pueda definir parámetros de transformación.  
  
 **Destino**  
 Especifique si desea omitir una columna durante la operación de copia. Puede copiar solo un subconjunto de columnas seleccionando  **\<omitir >** en esta columna para las columnas que desea omitir. Antes de asignar columnas, debe omitir todas las columnas que no se asignarán.  
  
 **Tipo**  
 Seleccione un tipo de datos para la columna.  
  
 **Admisión de valores NULL**  
 Especifique si una columna aceptará un valor NULL.  
  
 **Tamaño**  
 Especifique el número de caracteres de la columna.  
  
 **Precisión**  
 Especifique la precisión de los datos que se muestran, haciendo referencia al número de dígitos.  
  
 **Escala**  
 Especifique la escala de los datos que se muestran, haciendo referencia al número de posiciones decimales.  
  
  
