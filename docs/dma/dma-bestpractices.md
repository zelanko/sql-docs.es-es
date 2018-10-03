---
title: Procedimientos recomendados para Data Migration Assistant (SQL Server) | Microsoft Docs
description: Aprenda las prácticas recomendadas para migrar bases de datos de SQL Server con Data Migration Assistant
ms.custom: ''
ms.date: 08/29/2018
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
manager: craigg
ms.openlocfilehash: 9a8d346e3cc4a2ddc718d9e2758ec02caa458a8f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47632712"
---
# <a name="best-practices-for-running-data-migration-assistant"></a>Procedimientos recomendados para ejecutar Data Migration Assistant
Este artículo proporciona algunos procedimientos recomendados para la instalación, evaluación y migración.

## <a name="installation"></a>Installation
No instalar y ejecutar el Asistente para migración de datos directamente en el equipo de host de SQL Server.

## <a name="assessment"></a>Evaluación de
- Ejecute las evaluaciones en bases de datos de producción durante las horas de poca actividad.
- Realizar el **problemas de compatibilidad** y **recomendación de característica nueva** evaluaciones por separado para reducir la duración de la evaluación.

## <a name="migration"></a>Migración
- Migrar un servidor durante las horas de poca actividad.

- Al migrar una base de datos, proporcionar una ubicación de recurso compartido única accesible para el servidor de origen y el servidor de destino y, si es posible evitar que una operación de copia. Una operación de copia puede producirse una demora en función del tamaño del archivo de copia de seguridad. La operación de copia también aumenta las posibilidades de que una migración se producirá un error debido a un paso adicional. Cuando se proporciona una única ubicación, Data Migration Assistant omite la operación de copia.
 
    Además, asegúrese de que para proporcionar los permisos correctos a la carpeta compartida para evitar errores de migración. Los permisos correctos se especifican en la herramienta. Si una instancia de SQL Server se ejecuta con credenciales de servicio de red, debe conceder los permisos correctos en la carpeta compartida para la cuenta de equipo para la instancia de SQL Server.

- Habilitar cifrar la conexión al conectarse a los servidores de origen y destino. Uso de SSL cifrado aumenta la seguridad de los datos transmitidos a través de las redes entre Data Migration Assistant y la instancia de SQL Server, que es útil, especialmente al migrar los inicios de sesión SQL. Si no se usa el cifrado SSL y un atacante pone en peligro la red, los inicios de sesión SQL que se está migrados se podrían obtener interceptar o sobre la marcha, el atacante puede modificar.

    Sin embargo, si todo el acceso se realiza dentro de una configuración de intranet segura, el cifrado podría no ser necesario. Habilitación del cifrado reduce el rendimiento porque la sobrecarga adicional se necesita para cifrar y descifrar los paquetes. Para obtener más información, consulte [cifrar conexiones a SQL Server](https://go.microsoft.com/fwlink/?linkid=832513).
