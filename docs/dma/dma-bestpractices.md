---
title: Procedimientos recomendados para Data Migration Assistant
description: Conozca las prácticas recomendadas para migrar bases de datos de SQL Server con Data Migration Assistant
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
ms.openlocfilehash: f2bfbb79a8a4803bb56e3dce85f575e8cf257b4a
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/15/2020
ms.locfileid: "81388152"
---
# <a name="best-practices-for-running-data-migration-assistant"></a>Procedimientos recomendados para ejecutar Data Migration Assistant
En este artículo se proporciona información sobre prácticas recomendadas para la instalación, la evaluación y la migración.

## <a name="installation"></a>Instalación
No instale ni ejecute el Asistente para migración de datos directamente en el equipo host de SQL ServerSQL Server .

## <a name="assessment"></a>Evaluación
- Ejecute evaluaciones en bases de datos de producción durante las horas no pico.
- Realice las evaluaciones Problemas de **compatibilidad** y **Recomendaciones de nuevas características** por separado para reducir la duración de la evaluación.

## <a name="migration"></a>Migración
- Migre un servidor durante las horas no pico.

- Al migrar una base de datos, proporcione una única ubicación de recurso compartido accesible para el servidor de origen y el servidor de destino, y evite una operación de copia si es posible. Una operación de copia puede introducir retrasos en función del tamaño del archivo de copia de seguridad. La operación de copia también aumenta las posibilidades de que se produzca un error en una migración debido a un paso adicional. Cuando se proporciona una única ubicación, el Asistente para migración de datos omite la operación de copia.
 
    Además, asegúrese de proporcionar los permisos correctos a la carpeta compartida para evitar errores de migración. Los permisos correctos se especifican en la herramienta. Si una instancia de SQL ServerSQL Server se ejecuta con credenciales de servicio de red, conceda los permisos correctos en la carpeta compartida a la cuenta de equipo para la instancia de SQL ServerSQL Server .

- Habilite la conexión de cifrado al conectarse a los servidores de origen y de destino. El uso del cifrado TLS aumenta la seguridad de los datos transmitidos a través de las redes entre Data Migration Assistant y la instancia de SQL ServerSQL Server , lo que es beneficioso especialmente al migrar inicios de sesión SQL. Si no se utiliza el cifrado TLS y un atacante pone en peligro la red, los inicios de sesión SQL que se están migrando podrían ser interceptados y/o modificados sobre la marcha por el atacante.

    Sin embargo, si todo el acceso se realiza dentro de una configuración de intranet segura, el cifrado podría no ser necesario. Habilitar el cifrado ralentiza el rendimiento porque la sobrecarga adicional necesaria para cifrar y descifrar paquetes. Para obtener más información, consulte [Cifrado de conexiones a SQL Server](https://go.microsoft.com/fwlink/?linkid=832513).
    
- Compruebe si hay restricciones que no son de confianza tanto en la base de datos de origen como en la base de datos de destino antes de migrar los datos. Después de la migración, analice la base de datos de destino de nuevo para ver si alguna restricción pasó a ser de confianza como parte del movimiento de datos. Corrija las restricciones que no son de confianza según sea necesario. Si no se confían las restricciones, se pueden producir planes de ejecución deficientes y puede afectar al rendimiento.
