---
title: Notas de la versión (Controlador OLE DB para SQL Server) | Microsoft Docs
ms.date: 07/03/2018
ms.prod: sql
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daveng
ms.openlocfilehash: 01ea0242637f4dd5c813808b3b840d3a5a86df9a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47789123"
---
# <a name="release-notes-for-the-microsoft-ole-db-driver-for-sql-server"></a>Notas de la versión del controlador Microsoft OLE DB para SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../includes/driver_oledb_download.md)]

Esta página describe lo que se ha agregado en cada versión del controlador de Microsoft OLE DB para SQL Server.

## <a name="whats-new-in-version-1810"></a>Novedades de la versión 18.1.0

**Características agregadas:**

* Compatibilidad con `UseFMTONLY` palabra clave de cadena de conexión y `SSPROP_INIT_USEFMTONLY` propiedad de inicialización.
`UseFMTONLY` controla cómo se recuperan los metadatos cuando se conecta a [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] y versiones más recientes.  
Para obtener más información, vea:
  * [Uso de palabras clave de cadena de conexión con el controlador OLE DB para SQL Server](applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md)

**Errores corregidos:**

* Fijo versión incorrecta del archivo de formato BCP. Las versiones 18.0 controlador OLE DB establece incorrectamente la versión del archivo de formato BCP en 18,0 en lugar de 11.0. No se pueden leer los archivos de formato generados por las versiones 18.0 controlador OLE DB 18.1 de controlador de OLE DB. Si tiene que usar los archivos de formato generados por la versión anterior del controlador con el nuevo controlador, puede editar manualmente los archivos para cambiar la versión 11.0.

## <a name="whats-new-in-version-1802"></a>Novedades de la versión 18.0.2

**Características agregadas**:

* Compatibilidad con `MultiSubnetFailover` palabra clave de cadena de conexión y `SSPROP_INIT_MULTISUBNETFAILOVER` propiedad de inicialización.  
Para obtener más información, vea:  
  * [Controlador OLE DB para la compatibilidad de SQL Server con la alta disponibilidad y la recuperación ante desastres](features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)  
  * [Uso de palabras clave de cadena de conexión con el controlador OLE DB para SQL Server](applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md)

## <a name="see-also"></a>Vea también
[Controlador Microsoft OLE DB para SQL Server](oledb-driver-for-sql-server.md)
