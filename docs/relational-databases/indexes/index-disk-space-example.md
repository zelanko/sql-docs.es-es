---
title: "Ejemplo de espacio en disco del índice | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-indexes
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- online index disk space
- disk space [SQL Server], indexes
- index disk space [SQL Server]
- space [SQL Server], indexes
- indexes [SQL Server], disk space requirements
- offline index disk space [SQL Server]
ms.assetid: e5c71f55-0be3-4c93-97e9-7b3455c8f581
caps.latest.revision: "30"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 34ea623f3e64833c73f23a5be78fd3cf9ef9722b
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="index-disk-space-example"></a>Ejemplo de espacio en disco del índice
  Cuando se crea, regenera o quita un índice, se necesita espacio en disco para las estructuras antiguas (origen) y nuevas (destino) en los archivos y grupos de archivos correspondientes. La asignación de la estructura antigua no se cancela hasta que no se confirma la transacción de creación del índice. También puede resultar necesario espacio en disco temporal adicional para operaciones de ordenación. Para más información, consulte [Disk Space Requirements for Index DDL Operations](../../relational-databases/indexes/disk-space-requirements-for-index-ddl-operations.md).  
  
 En este ejemplo, se determinan las necesidades de espacio en disco para crear un índice clúster.  
  
 Supongamos que se cumplen las siguientes condiciones antes de crear el índice clúster:  
  
-   La tabla existente (montón) contiene 1 millón de filas. Cada fila tiene una longitud de 200 bytes.  
  
-   El índice no clúster A contiene 1 millón de filas. Cada fila tiene una longitud de 50 bytes.  
  
-   El índice no clúster B contiene 1 millón de filas. Cada fila tiene una longitud de 80 bytes.  
  
-   La opción index create memory está establecida en 2 MB.  
  
-   Se utiliza un valor de factor de relleno de 80 para todos los índices existentes y nuevos. Esto significa que se llena el 80% de las páginas.  
  
    > [!NOTE]  
    >  Como resultado de la creación de un índice clúster, ambos índices no clúster deben regenerarse para reemplazar el indicador de filas con la clave del nuevo índice clúster.  
  
## <a name="disk-space-calculations-for-an-offline-index-operation"></a>Cálculos de espacio en disco para una operación de índice sin conexión  
 En los pasos siguientes, se calcula el espacio en disco temporal que se utilizará en la operación del índice y el espacio en disco permanente necesario para almacenar los nuevos índices. Los cálculos que se muestran son aproximados; los resultados se redondean al número superior y solo se tiene en cuenta el tamaño del nivel hoja del índice. Para indicar cálculos aproximados, se utiliza la tilde (~).  
  
1.  Determine el tamaño de las estructuras de origen.  
  
     Montón: 1 millón * 200 bytes ~ 200 MB  
  
     Índice no clúster A: 1 millón * 50 bytes / 80% ~ 63 MB  
  
     Índice no clúster B: 1 millón * 80 bytes / 80% ~ 100 MB  
  
     Tamaño total de las estructuras existentes: 363 MB  
  
2.  Determine el tamaño de las estructuras de índice de destino. Supongamos que la clave del nuevo índice agrupado tiene una longitud de 24 bytes, incluido un valor de unicidad. El indicador de filas (8 bytes de longitud) en ambos índices no clúster se reemplazará con esta clave de agrupación en clústeres.  
  
     Índice clúster: 1 millón * 200 bytes / 80% ~ 250 MB  
  
     Índice no clúster A: 1 millón * (50 – 8 + 24) bytes / 80% ~ 83 MB  
  
     Índice no clúster B: 1 millón * (80 – 8 + 24) bytes / 80% ~ 120 MB  
  
     Tamaño total de las nuevas estructuras: 453 MB  
  
     El espacio en disco necesario para las estructuras de origen y destino en toda la operación del índice es de 816 MB (363 + 453). Cuando se confirma la operación de índice, se cancela la asignación del espacio asignado a las estructuras de origen.  
  
3.  Determine el espacio en disco temporal adicional para la ordenación.  
  
     Se muestran los requisitos de espacio para ordenar en **tempdb** (con la opción SORT_IN_TEMPDB establecida en ON) y en la ubicación de destino (con la opción SORT_IN_TEMPDB establecida en OFF).  
  
    1.  Si SORT_IN_TEMPDB se ha establecido en ON, **tempdb** debe disponer de espacio en disco suficiente para incluir el índice más grande (1 millón * 200 bytes ~ 200 MB). El factor de relleno no se tiene en cuenta en la operación de ordenación.  
  
         El espacio en disco adicional (en la ubicación de **tempdb** ) es igual al valor de [Establecer la opción de configuración del servidor Memoria para creación de índices](../../database-engine/configure-windows/configure-the-index-create-memory-server-configuration-option.md) = 2 MB.  
  
         Tamaño total de espacio en disco temporal con la opción SORT_IN_TEMPDB establecida en ON ~ 202 MB.  
  
    2.  Si SORT_IN_TEMPDB se ha establecido en OFF (valor predeterminado), se utilizan para la ordenación los 250 MB de espacio en disco que ya se han tenido en cuenta para el nuevo índice en el paso 2.  
  
         El espacio en disco adicional (en la ubicación de destino) es igual al valor de [Establecer la opción de configuración del servidor Memoria para creación de índices](../../database-engine/configure-windows/configure-the-index-create-memory-server-configuration-option.md) = 2 MB.  
  
         Tamaño total de espacio en disco temporal con la opción SORT_IN_TEMPDB establecida en OFF = 2 MB.  
  
 Si se usa **tempdb**, se necesitan 1018 MB (816 + 202) para crear los índices agrupados y no agrupados. Aunque **tempdb** aumenta la cantidad de espacio en disco temporal utilizado para crear un índice, puede reducir el tiempo que tarda en crearse el índice cuando **tempdb** está en un conjunto de discos diferente al de la base de datos de usuario. Para obtener más información sobre cómo usar **tempdb**, vea [Opción SORT_IN_TEMPDB para índices](../../relational-databases/indexes/sort-in-tempdb-option-for-indexes.md).  
  
 Si no se usa **tempdb**, se necesitan 818 MB (816 + 2) para crear los índices agrupados y no agrupados.  
  
## <a name="disk-space-calculations-for-an-online-clustered-index-operation"></a>Cálculos de espacio en disco para una operación de índice clúster en línea  
 Cuando se crea, quita o regenera un índice clúster en línea, se necesita espacio en disco adicional para generar y mantener un índice de asignación temporal. Este índice de asignación temporal contiene un registro por cada fila de la tabla y su contenido es la unión de las columnas de marcadores antiguas y nuevas.  
  
 Para calcular el espacio en disco necesario para una operación de índice clúster en línea, siga los pasos indicados para una operación de índice sin conexión y agregue el resultado al resultado del paso siguiente.  
  
-   Determine el espacio para el índice de asignación temporal.  
  
     En este ejemplo, el marcador antiguo es el Id. de fila (RID) del montón (8 bytes) y el nuevo marcador es la clave de agrupación en clústeres (24 bytes incluido un **valor de unicidad**). No existen columnas superpuestas entre los marcadores antiguos y nuevos.  
  
     Tamaño del índice de asignación temporal = 1 millón * (8 bytes + 24 bytes) / 80% ~ 40 MB.  
  
     Este espacio en disco debe agregarse al espacio en disco necesario en la ubicación de destino si la opción SORT_IN_TEMPDB está establecida en OFF o en **tempdb** si SORT_IN_TEMPDB está establecida en ON.  
  
 Para obtener más información sobre el índice de asignación temporal, vea [Requisitos de espacio en disco para operaciones DDL de índice](../../relational-databases/indexes/disk-space-requirements-for-index-ddl-operations.md).  
  
## <a name="disk-space-summary"></a>Resumen de espacio en disco  
 En la tabla siguiente se resumen los resultados de los cálculos del espacio en disco.  
  
|Operación de índice|Requisitos de espacio en disco para las ubicaciones de las siguientes estructuras|  
|---------------------|---------------------------------------------------------------------------|  
|Operación de índice sin conexión con SORT_IN_TEMPDB = ON|Espacio total durante la operación: 1018 MB<br /><br /> - Tabla e índices existentes: 363 MB\*<br /><br /> -<br />                    **tempdb**: 202 MB*<br /><br /> - Nuevos índices: 453 MB<br /><br /> Espacio total necesario después de la operación: 453 MB|  
|Operación de índice sin conexión con SORT_IN_TEMPDB = OFF|Espacio total durante la operación: 816 MB<br /><br /> - Tabla e índices existentes: 363 MB*<br /><br /> - Nuevos índices: 453 MB<br /><br /> Espacio total necesario después de la operación: 453 MB|  
|Operación de índice en línea con SORT_IN_TEMPDB = ON|Espacio total durante la operación: 1058 MB<br /><br /> - Tabla e índices existentes: 363 MB\*<br /><br /> -<br />                    **tempdb** (incluye índice de asignación): 242 MB*<br /><br /> - Nuevos índices: 453 MB<br /><br /> Espacio total necesario después de la operación: 453 MB|  
|Operación de índice en línea con SORT_IN_TEMPDB = OFF|Espacio total durante la operación: 856 MB<br /><br /> - Tabla e índices existentes: 363 MB*<br /><br /> - Índice de asignación temporal: 40 MB\*<br /><br /> - Nuevos índices: 453 MB<br /><br /> Espacio total necesario después de la operación: 453 MB|  
  
 *La asignación de este espacio se cancela cuando se confirma la operación de índice.  
  
 En este ejemplo no se tiene en cuenta el espacio en disco temporal adicional que se necesita en **tempdb** para los registros de versión creados por operaciones simultáneas de actualización y eliminación del usuario.  
  
## <a name="related-content"></a>Contenido relacionado  
 [Disk Space Requirements for Index DDL Operations](../../relational-databases/indexes/disk-space-requirements-for-index-ddl-operations.md)  
  
 [Espacio en disco del registro de transacciones para operaciones de índice](../../relational-databases/indexes/transaction-log-disk-space-for-index-operations.md)  
  
  
