---
title: Prácticas recomendadas para el Asistente para migración de datos (SQL Server) | Documentos de Microsoft
ms.custom: ''
ms.date: 10/04/2017
ms.prod: sql-non-specified
ms.prod_service: dma
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-dma
ms.tgt_pltfrm: ''
ms.topic: article
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Best Practices
ms.assetid: ''
caps.latest.revision: ''
author: HJToland3
ms.author: jtoland
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f8842ca064494bc7ead99eb34d6ea2cc76bb2679
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="best-practices-for-running-data-migration-assistant"></a>Prácticas recomendadas para ejecutar el Asistente de migración de datos
Este artículo proporciona la siguiente información de prácticas recomendadas para la instalación, las evaluaciones y de migración.

## <a name="installation"></a>Installation

No se instale y ejecute el Asistente de migración de datos directamente en el equipo de host de SQL Server.

## <a name="assessment"></a>Evaluación de

- Ejecutar las evaluaciones en bases de datos de producción durante las horas de poca actividad.

- Realizar la **problemas de compatibilidad** y **nuevas recomendaciones de característica** evaluaciones por separado para reducir la duración de la evaluación.

## <a name="migration"></a>Migración

- Migrar un servidor durante las horas de poca actividad.

- Al migrar una base de datos, proporcionar una ubicación de recurso compartido único accesible para el servidor de origen y el servidor de destino y, si es posible evitar que una operación de copia. Una operación de copia puede producirse una demora en función del tamaño del archivo de copia de seguridad. La operación de copia también aumenta las posibilidades de una migración errores debido a un paso adicional. Cuando se proporciona una única ubicación, el Asistente de migración de datos elude la operación de copia.
 
    También asegúrese de que para proporcionar los permisos correctos a la carpeta compartida para evitar errores de migración. Los permisos correctos se especifican en la herramienta. Si una instancia de SQL Server se ejecuta con las credenciales de servicio de red, otorga los permisos correctos en la carpeta compartida a la cuenta de equipo para la instancia de SQL Server.

- Habilitar cifrar la conexión al conectarse a los servidores de origen y de destino. Uso de SSL cifrado aumenta la seguridad de los datos transmitidos a través de las redes entre el Asistente de migración de datos y la instancia de SQL Server. Esto es beneficioso especialmente al migrar los inicios de sesión SQL. Si no se usa el cifrado SSL y un atacante pone en peligro la red, los inicios de sesión SQL que se está migrados se pudieron obtener interceptar o modificación sobre la marcha por el atacante.

    Sin embargo, si todo el acceso se realiza dentro de una configuración de intranet segura, el cifrado podría no ser necesario. Habilitar el cifrado reduce el rendimiento como resultado la adicional de sobrecarga necesario para cifrar y descifrar los paquetes. Para obtener más información, consulte [cifrar conexiones a SQL Server](https://go.microsoft.com/fwlink/?linkid=832513).
