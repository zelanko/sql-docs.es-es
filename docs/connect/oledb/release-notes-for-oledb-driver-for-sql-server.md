---
title: Notas de la versión (Controlador OLE DB para SQL Server) | Microsoft Docs
ms.date: 02/12/2019
ms.prod: sql
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daveng
ms.openlocfilehash: 36dc1b7325265da6231b75e9f4db46854b0b219f
ms.sourcegitcommit: 958cffe9288cfe281280544b763c542ca4025684
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 02/23/2019
ms.locfileid: "56744365"
---
# <a name="release-notes-for-the-microsoft-ole-db-driver-for-sql-server"></a>Notas de la versión del controlador Microsoft OLE DB para SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../includes/driver_oledb_download.md)]

Esta página describe lo que se ha agregado en cada versión del controlador de Microsoft OLE DB para SQL Server.

## <a name="whats-new-in-version-1821"></a>Novedades de la versión 18.2.1

**Características agregadas:**

* Compatibilidad con la codificación UTF-8 del servidor. Para obtener más información, consulte: [compatibilidad UTF-8 en el controlador OLE DB para SQL Server](features/utf-8-support-in-oledb-driver-for-sql-server.md).
* Soporte técnico de la autenticación de Azure Active Directory. Para más información, consulte [Uso de Azure Active Directory](features/using-azure-active-directory.md).

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
