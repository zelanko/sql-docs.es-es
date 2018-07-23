---
title: Ventana de salida de SSMS | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Output Window [SQL Server Management Studio]
- Activity Monitor [SQL Server Management Studio]
- Object Explorer [SQL Server Management Studio]
ms.assetid: a2ce1a07-b4e2-471c-87d2-b8de5e6c6864
caps.latest.revision: 1
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6a3075f8aa917c4728ffa70a87137f5ad3e20043
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/12/2018
ms.locfileid: "38984287"
---
# <a name="output-window-in-sql-server-management-studio"></a>Ventana de salida de SQL Server Management Studio
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
La Ventana de salida se puede abrir en el menú Ver o mediante la combinación de teclas Ctrl+Alt+O. Hay varios canales de salida disponibles.

En la tabla siguiente se ofrece una visión general de los tipos de mensajes asociados a cada canal de salida.

|Canal|Descripción|
|-----------|---------------|  
|**Telemetría**|La telemetría es la secuencia de [datos de uso de la función anónima](sql-server-management-studio-ssms.md) que recopila Microsoft. Estos eventos pueden ser útiles para sus propios registros de uso de SSMS. Pueden ayudarle a identificar los nodos del Explorador de objetos que ha expandido, así como qué comandos ha ejecutado durante su sesión en SSMS con la Ventana de salida abierta.|
|**Ver**|Este canal da como resultado el texto de consulta y el tiempo transcurrido para realizar las consultas SQL necesarias para expandir nodos en el Explorador de objetos. Cada consulta registra una consulta inicial y un evento de consulta final. Cada evento tiene una marca de tiempo y el URN asociados a la entidad a la que se envía la consulta. El [URN](https://technet.microsoft.com/library/microsoft.sqlserver.management.smo.urn(v=sql.90).aspx) hace referencia al objeto de administración de SQL subyacente y consta de una jerarquía de estilo XPath. Por ejemplo, el URN de una tabla llamada "Tabla1" en la base de datos "Base de datos" del servidor "Mi servidor" sería "Server[@Name='MiServidor']/Database[@Name='BaseDeDatos'/Table[/@Name='Tabla1']".  Al expandir un nodo en el Explorador de objetos, puede realizar varias de estas consultas usando parámetros diferentes. El evento de finalización de consulta contendrá el tiempo transcurrido de la consulta junto con el texto TSQL. Es posible que esta consulta de datos le resulte útil para el análisis del rendimiento del servidor en casos en los que el Explorador de objetos parezca inusualmente lento al intentar expandir un nodo determinado. **Nota**: No todos los nodos del Explorador de objetos aportan este nivel de detalle de la consulta al expandirse.|
|**Monitor de actividad**|Este canal se inicia cuando se [abre el Monitor de actividad](https://docs.microsoft.com/sql/relational-databases/performance-monitor/activity-monitor) para un servidor. Esta secuencia contiene eventos que muestran parte del texto de la consulta y la marca de tiempo de cada consulta, mensajes de error y notificaciones del monitor para informar de que están en pausa debido a problemas de conectividad. Si el Monitor de actividad parece estar inactivo o no se puede actualizar, compruebe este canal de salida para obtener más información.|





