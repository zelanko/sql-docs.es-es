---
title: Tarea de carga de Azure SQL DW | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL12.DTS.DESIGNER.AFPDWUPTASK.F1
- SQL11.DTS.DESIGNER.AFPDWUPTASK.F1
ms.assetid: 112cf764-f85a-4c1a-b732-d299d717c0d4
author: yualan
ms.author: chugu
ms.openlocfilehash: adcc4cc06ac01ea833972ffcd7c1a5ade411bfb2
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/26/2020
ms.locfileid: "85439322"
---
# <a name="azure-sql-dw-upload-task"></a>Tarea de carga de Azure SQL DW
La **tarea de carga de Azure SQL DW** habilita un paquete SSIS para cargar datos locales en una tabla de Azure SQL Data Warehouse (DW). El formato de archivo de origen de datos que se admite actualmente es texto delimitado en codificación UTF8. El proceso de carga sigue el enfoque eficaz de polybase. En concreto, los datos primero se cargan en Azure Blob Storage y, a continuación, en Azure SQL DW. Por lo tanto, esta tarea requiere una cuenta de Azure Blob Storage.

Para agregar una **tarea de carga de Azure SQL DW**, arrástrela desde el cuadro de herramientas de SSIS y suéltela en el lienzo de diseño. A continuación, haga doble clic o clic con el botón secundario y haga clic en **Editar** para que se muestre el cuadro de diálogo de edición.

En la página **General** , configure las propiedades siguientes.

Campo|Descripción
-----|-----------
LocalDirectory|Especifica el directorio local que contiene los archivos de datos que se van a cargar.
Recursively|Especifica si los subdirectorios se deben buscar de forma recursiva.
FileName|Especifica un filtro de nombre para seleccionar archivos con un determinado patrón de nombre. Por ejemplo, MiHoja*.xsl\* incluirá archivos como MiHoja001.xsl y MiHojaABC.xslx.
RowDelimiter|Especifica los caracteres que marcan el final de cada fila.
ColumnDelimiter|Especifica uno o más caracteres que marcan el final de cada columna. Por ejemplo, &#124; (barra vertical), \t (tabulación), ' (comilla simple), " (comilla doble) y 0x5c (barra diagonal inversa).
IsFirstRowHeader|Especifica si la primera fila de cada archivo de datos contiene nombres de columna en lugar de datos reales.
AzureStorageConnection|Especifica un administrador de conexiones de Azure Storage.
BlobContainer|Especifica el nombre del contenedor de blob en el que se cargarán los datos locales para retransmitirlos a Azure DW mediante PolyBase. Si no existe ningún contenedor, se creará uno.
BlobDirectory|Especifica el directorio de blob (estructura jerárquica virtual) en el que se cargarán los datos locales para retransmitirlos a Azure DW mediante PolyBase.
RetainFiles|Especifica si se deben conservar los archivos cargados en Azure Storage.
CompressionType|Especifica el formato de compresión que se usará al cargar archivos en Azure Storage. El origen local no se verá afectado.
CompressionLevel|Especifica el nivel de compresión que se usará para el formato de compresión.
AzureDwConnection|Especifica un administrador de conexión de ADO.NET para Azure SQL DW.
TableName|Especifica el nombre de la tabla de destino. Elija un nombre de tabla existente o cree uno nuevo; para ello, elija **\<New Table ...>** .
TableDistribution|Especifica el método de distribución para la tabla nueva. Se aplica si se especifica un nuevo nombre de tabla para **TableName**.
HashColumnName|Especifica la columna usada para la distribución de la tabla hash. Se aplica si **HASH** se ha especificado para **TableDistribution**.

Se mostrará otra página **Asignaciones** en función de si quiere cargar los datos en una tabla nueva o en una existente. En el primer caso, configure las columnas de origen que se van a asignar y los nombres correspondientes en la tabla de destino que se creará. En el segundo caso, configure las relaciones de asignación entre las columnas de origen y las de destino.

En la página **Columnas** , configure las propiedades de tipos de datos para cada columna de origen.

La página **T-SQL** muestra la instrucción T-SQL usada para cargar datos de Azure Blob Storage a Azure SQL DW. La instrucción T-SQL se genera automáticamente a partir de configuraciones de otras páginas y se ejecuta como parte de la tarea. Puede editar manualmente la instrucción T-SQL generada para adaptarla a sus necesidades concretas haciendo clic en el botón **Editar** . Puede revertirla para volver a la que se genera automáticamente más tarde haciendo clic en el botón **Restablecer** .
