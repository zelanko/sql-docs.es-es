---
title: Extensión de Instancia administrada de Azure°SQL
titleSuffix: Azure Data Studio
description: Uso de Azure Data Studio con Instancia administrada de Azure SQL
ms.custom: seodec18
ms.date: 10/07/2019
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: jovanpop-msft
ms.author: jovanpop
manager: alanyu
ms.openlocfilehash: d443292fb091679d3d6a18d557a5a7aac464fdec
ms.sourcegitcommit: 512acc178ec33b1f0403b5b3fd90e44dbf234327
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/08/2019
ms.locfileid: "72041143"
---
# <a name="managed-instance-support-for-azure-data-studio-preview"></a>Compatibilidad de Instancia administrada para Azure Data Studio (versión preliminar)

Esta extensión le permite trabajar con [Instancia administrada de Azure SQL](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-index) en [Azure Data Studio](https://github.com/Microsoft/azuredatastudio). Esta extensión proporciona las características siguientes:

- Mostrar las propiedades de Instancia administrada (núcleos virtuales, almacenamiento usado).
- Supervisar el uso de la CPU y el almacenamiento en las últimas dos horas.
- Mostrar recomendaciones de ajustes y advertencias de configuración.
- Mostrar el estado de las réplicas de bases de datos.
- Mostrar los registros de errores con filtros.

## <a name="installations"></a>Instalaciones

Para instalar la versión oficial de la extensión de Instancia administrada, siga el procedimiento que se indica en la [documentación de Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/extensions).
En el panel Extensiones, busque la extensión "Instancia administrada" e instálela.  Recibirá notificaciones automáticamente sobre las futuras actualizaciones de la extensión.

Una vez que instale la extensión Instancia administrada, verá una pestaña `Managed Instance` en Azure Data Studio. En esta pestaña, puede encontrar información específica para Instancia administrada.

## <a name="properties"></a>Propiedades

Esta extensión le permite ver las características técnicas de su Instancia administrada y el uso de ciertos recursos.

![Propiedades de Instancia administrada](media/azure-sql-mi-extension/ads-mi-tab1.png)

En la primera hoja, puede ver los detalles siguientes:

- Las **propiedades básicas**, como el número de núcleos virtuales disponibles, memoria, almacenamiento, nivel de servicio actual y generación de hardware, y las características de I/O, como las características de I/O o rendimiento de archivo o rendimiento de escritura de registros de instancia.
- **Uso del almacenamiento SSD local**. En el nivel de servicio de uso general, solo los archivos **TEMPDB** se colocan de manera local, mientras que en el nivel crítico para la empresa, todos los archivos de base de datos se colocan en el almacenamiento SSD local. En esta sección, puede ver cuánto espacio del almacenamiento local usa la Instancia administrada.
- **Uso de Azure Premium Disk Storage**: las bases de datos de usuario y sistema en el nivel de servicio de uso general se ubican en Azure Premium Storage. Aquí puede encontrar la cantidad de datos que usó y cuál es el almacenamiento restante y el número de archivos. Esta sección está vacía en el nivel de servicio crítico para la empresa.
- El **uso de recursos** que le mostrará cuánto almacenamiento y CPU usó su instancia en las últimas dos horas. Aumente el tamaño de la instancia si ya está alcanzando el límite.

## <a name="recommendations"></a>Recomendaciones

Esta extensión proporciona algunas recomendaciones y alertas que pueden ayudarlo a optimizar la Instancia administrada.

![Recomendaciones de Instancia administrada](media/azure-sql-mi-extension/ads-mi-tab2.png)

Algunas de las recomendaciones que se muestran en esta tabla son:

- Al llegar al límite de espacio de almacenamiento: debe eliminar los datos innecesarios o aumentar el tamaño de almacenamiento de la instancias, porque las bases de datos que alcanzan el límite de almacenamiento podrían no procesar ni siquiera las consultas de lectura.
- Al llegar al límite de rendimiento de la instancia: si está cargando ~22 MB/s en GP o ~48 MB/s en BC, Instancia administrada limitará la carga para garantizar que se puedan realizar copias de seguridad.
- Presión de memoria: una duración prevista de la página baja o una gran cantidad de estadísticas de espera `PAGEIOLATCH` podrían indicar que la instancia expulsa páginas de la memoria e intenta constantemente cargar más páginas del disco.
- Límites del archivo de registro: si los registros están llegando a los [límites de I/O en el nivel de servicio de uso general](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-resource-limits#file-io-characteristics-in-general-purpose-tier), es posible que tenga que aumentar el tamaño de archivo para obtener un mejor rendimiento.
- Límites del archivo de datos: si los archivos de datos están llegando a los [límites de I/O en el nivel de servicio de uso general](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-resource-limits#file-io-characteristics-in-general-purpose-tier), es posible que tenga que aumentar el tamaño de archivo para obtener un mejor rendimiento. Este problema podría generar presión de memoria y ralentizar las copias de seguridad.
- Problemas de disponibilidad: un gran número de archivos de registro virtuales puede causar un impacto en el rendimiento y una posible recuperación de base de datos más prolongada en el nivel de servicio de uso general en caso de error en el proceso.

Debe revisar periódicamente estas recomendaciones, investigar las causas principales y llevar a cabo acciones correctivas. La extensión de instancia administrada proporciona los scripts que se pueden ejecutar para mitigar algunos de los problemas detectados.

## <a name="replicas"></a>Réplicas

La extensión de instancia administrada le permite ver el estado de las réplicas de base de datos en la Instancia administrada.

![Réplicas de instancia administrada](media/azure-sql-mi-extension/ads-mi-tab3.png)

En el nivel de servicio de uso general, cada base de datos tiene una única réplica (principal), mientras que en la instancia crítica para la empresa, cada base de datos tiene una réplica principal y tres réplicas secundarias (una se usa para cargas de trabajo de solo lectura). Aquí puede supervisar el proceso de sincronización y comprobar que todas las réplicas secundarias están sincronizadas con la réplica principal.

## <a name="logs"></a>Registros

La extensión de instancia administrada muestra las últimas entradas del registro de errores de SQL más pertinentes.

![Entradas de registro de Instancia administrada](media/azure-sql-mi-extension/ads-mi-tab4.png)

La Instancia administrada emite un gran número de entradas de registro y la mayoría de ellas son información del sistema/internas. Algunas entradas del registro muestran los nombres de las bases de datos físicas (valores `GUID`) en lugar de los nombres de las bases de datos lógicas reales.

La extensión de instancia administrada filtra las entradas de registro innecesarias en función del [método Dimitri Furman](https://techcommunity.microsoft.com/t5/DataCAT/Azure-SQL-DB-Managed-Instance-sp-readmierrorlog/ba-p/305506) y muestra los nombres de archivos lógicos reales en lugar de los nombres físicos.

## <a name="reporting-problems"></a>Informar de problemas

Si tiene problemas con la extensión de instancia administrada, informe del problema en el [proyecto de extensión de GitHub](https://github.com/JocaPC/AzureDataStudio-Managed-Instance/issues).

## <a name="maintainers"></a>Mantenedores

- [Jovan Popovic (MSFT)](https://github.com/jovanpop_msft) - [@jovanpop_msft](https://twitter.com/JovanPop_MSFT)

## <a name="code-of-conduct"></a>Código de conducta

El proyecto ha adoptado el [Código de conducta de código abierto de Microsoft][conduct-code].
Para obtener más información, vea las [Preguntas más frecuentes sobre el código de conducta][conduct-FAQ], o póngase en contacto con [opencode@microsoft.com][conduct-email] si tiene preguntas o comentarios.

[conduct-code]: http://opensource.microsoft.com/codeofconduct/
[conduct-FAQ]: http://opensource.microsoft.com/codeofconduct/faq/
[conduct-email]: mailto:opencode@microsoft.com
[conduct-md]: https://github.com/PowerShell/vscode-powershell/blob/master/CODE_OF_CONDUCT.md
