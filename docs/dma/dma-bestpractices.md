---
title: Procedimientos recomendados para Data Migration Assistant
description: Obtenga información sobre las prácticas recomendadas para migrar bases de datos de SQL Server con Data Migration Assistant
ms.custom: seo-lt-2019
ms.date: 03/12/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Best Practices
ms.assetid: ''
author: HJToland3
ms.author: rajpo
ms.openlocfilehash: ef953aa369e831e47d38db403b982919bd4bd830
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056554"
---
# <a name="best-practices-for-running-data-migration-assistant"></a>Prácticas recomendadas para ejecutar Data Migration Assistant
En este artículo se proporciona información sobre procedimientos recomendados para la instalación, la evaluación y la migración.

## <a name="installation"></a>Instalación
No instale ni ejecute el Data Migration Assistant directamente en la máquina host de SQL Server.

## <a name="assessment"></a>Evaluación
- Ejecute evaluaciones en las bases de datos de producción durante las horas de menor actividad.
- Realice los **problemas de compatibilidad** y las nuevas evaluaciones de **recomendaciones de características** por separado para reducir la duración de la evaluación.

## <a name="migration"></a>Migración
- Migre un servidor durante horas de poca actividad.

- Al migrar una base de datos, proporcione una única ubicación de recurso compartido a la que pueda acceder el servidor de origen y el servidor de destino, y evite una operación de copia si es posible. Una operación de copia puede presentar un retraso basado en el tamaño del archivo de copia de seguridad. La operación de copia también aumenta las posibilidades de que se produzca un error en la migración debido a un paso adicional. Cuando se proporciona una sola ubicación, Data Migration Assistant omite la operación de copia.
 
    Además, asegúrese de proporcionar los permisos correctos a la carpeta compartida para evitar errores de migración. Los permisos correctos se especifican en la herramienta. Si una instancia de SQL Server se ejecuta en credenciales de servicio de red, asigne los permisos correctos en la carpeta compartida a la cuenta de equipo para la instancia de SQL Server.

- Habilite la conexión de cifrado al conectarse a los servidores de origen y de destino. El uso del cifrado SSL aumenta la seguridad de los datos transmitidos a través de las redes entre Data Migration Assistant y la instancia de SQL Server, lo que resulta ventajoso especialmente al migrar inicios de sesión de SQL. Si no se usa el cifrado SSL y la red se ve comprometida por un atacante, el atacante podría interceptar o modificar los inicios de sesión de SQL que se van a migrar sobre la marcha.

    Sin embargo, si todo el acceso se realiza dentro de una configuración de intranet segura, el cifrado podría no ser necesario. Al habilitar el cifrado, se reduce el rendimiento, ya que la sobrecarga adicional necesaria para cifrar y descifrar los paquetes. Para obtener más información, consulte [cifrar conexiones a SQL Server](https://go.microsoft.com/fwlink/?linkid=832513).
